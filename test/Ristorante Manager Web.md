# 🍝 Ristorante Manager - Estratti Codice

Selezione di blocchi pronti da mostrare su GitHub (PHP/JS), con pillole di contesto e snippet in blocchi testo.

---

## 🛡️ Rate limit anti brute force 
- 🚦 Conta i tentativi per IP, applica un ban temporaneo e registra su file di log.
```php
function rl_on_failure(string $scope, string $ip, int $maxAttempts, int $windowSeconds, int $banSeconds): array {
    $now = time();
    [$path, $data] = rl_load($scope);
    $entry = rl_normalize($data[$ip] ?? ['first' => $now, 'fails' => 0, 'banUntil' => 0], $now, $windowSeconds);

    $entry['fails']++;
    $remaining = max(0, $maxAttempts - $entry['fails']);
    $blocked = false; $retryAt = 0;
    if ($entry['fails'] >= $maxAttempts) {
        $entry['banUntil'] = $now + $banSeconds;
        $blocked = true; $retryAt = $entry['banUntil'];
        $entry['fails'] = 0; $entry['first'] = $now; $remaining = 0;
    }

    $data[$ip] = $entry; rl_save($path, $data);
    return ['blocked' => $blocked, 'retryAt' => $retryAt, 'remaining' => $remaining];
}
```

---

## 🔄 Overlay JSON -> SQLite trasparente 
- 🗂️ L'app pensa di leggere/scrivere JSON, ma i percorsi chiave vengono reindirizzati al DB per coerenza live.
```php
function json_store_virtual_read(string $path, $default = null): array {
    $cleanPath = str_replace('\\', '/', $path);
    $menuPath  = str_replace('\\', '/', DATA_DIR . '/menu.json');
    $coverPath = str_replace('\\', '/', DATA_DIR . '/covers.json');
    $tablesPath = str_replace('\\', '/', DATA_DIR . '/tables.json');
    $menuMetaPath = str_replace('\\', '/', DATA_DIR . '/menu_meta.json');
    $tablesMetaPath = str_replace('\\', '/', DATA_DIR . '/tables_meta.json');

    if ($cleanPath === $menuPath) { return ['handled' => true, 'data' => sqlite_load_menu()]; }
    if ($cleanPath === $coverPath) { return ['handled' => true, 'data' => ['coverPrice' => sqlite_cover_price()]]; }
    if ($cleanPath === $menuMetaPath) { return ['handled' => true, 'data' => sqlite_menu_meta()]; }
    if ($cleanPath === $tablesMetaPath) { return ['handled' => true, 'data' => sqlite_tables_meta()]; }
    if ($cleanPath === $tablesPath) { return ['handled' => true, 'data' => sqlite_load_tables()]; }
    if (preg_match('~table_(\\d+)\\.json$~', $cleanPath, $m)) { return ['handled' => true, 'data' => sqlite_load_tab((int)$m[1])]; }
    if (preg_match('~carrello_tavolo_(\\d+)\\.json$~', $cleanPath, $m)) { return ['handled' => true, 'data' => sqlite_load_cart((int)$m[1])]; }
    return ['handled' => false, 'data' => $default];
}

function json_store_virtual_write(string $path, $data): array {
    $cleanPath = str_replace('\\', '/', $path);
    $menuPath = str_replace('\\', '/', DATA_DIR . '/menu.json');
    $coverPath = str_replace('\\', '/', DATA_DIR . '/covers.json');
    $tablesPath = str_replace('\\', '/', DATA_DIR . '/tables.json');
    $menuMetaPath = str_replace('\\', '/', DATA_DIR . '/menu_meta.json');
    $tablesMetaPath = str_replace('\\', '/', DATA_DIR . '/tables_meta.json');

    if ($cleanPath === $menuPath) { return ['handled' => true, 'ok' => sqlite_save_menu(is_array($data) ? $data : [])]; }
    if ($cleanPath === $coverPath) { if (is_array($data) && isset($data['coverPrice'])) { sqlite_set_cover_price((float)$data['coverPrice']); sqlite_touch_tables_meta(); sqlite_touch_menu_meta(); } return ['handled' => true, 'ok' => true]; }
    if ($cleanPath === $menuMetaPath) { if (is_array($data) && isset($data['updatedAt'])) { sqlite_set_setting('menu_updated_at', $data['updatedAt']); } else { sqlite_touch_menu_meta(); } return ['handled' => true, 'ok' => true]; }
    if ($cleanPath === $tablesMetaPath) { if (is_array($data) && isset($data['updatedAt'])) { sqlite_set_setting('tables_updated_at', $data); } else { sqlite_touch_tables_meta(); } return ['handled' => true, 'ok' => true]; }
    if ($cleanPath === $tablesPath) { return ['handled' => true, 'ok' => sqlite_save_tables(is_array($data) ? $data : [])]; }
    if (preg_match('~table_(\\d+)\\.json$~', $cleanPath, $m)) { if (is_array($data)) { sqlite_save_tab((int)$m[1], $data); } return ['handled' => true, 'ok' => true]; }
    if (preg_match('~carrello_tavolo_(\\d+)\\.json$~', $cleanPath, $m)) { if (is_array($data)) { sqlite_save_cart((int)$m[1], $data); } return ['handled' => true, 'ok' => true]; }
    return ['handled' => false, 'ok' => false];
}
```

---

## 🧳 Migrazione da JSON legacy a SQLite 
- 🚚 Riempie il DB vuoto importando menu, coperto, tavoli, tabs e carrelli esistenti su disco.
```php
function sqlite_import_legacy_if_needed(PDO $pdo): void {
    $hasCats = (int)$pdo->query('SELECT COUNT(*) FROM categories')->fetchColumn();
    $hasTables = (int)$pdo->query('SELECT COUNT(*) FROM restaurant_tables')->fetchColumn();
    $hasTabs = (int)$pdo->query('SELECT COUNT(*) FROM tabs')->fetchColumn();

    if ($hasCats === 0 && is_readable(DATA_DIR . '/menu.json')) {
        $raw = @file_get_contents(DATA_DIR . '/menu.json');
        $parsed = json_decode((string)$raw, true);
        if (is_array($parsed)) { sqlite_save_menu($parsed); }
    }
    if (sqlite_get_setting('cover_price', null) === null && is_readable(DATA_DIR . '/covers.json')) {
        $raw = @file_get_contents(DATA_DIR . '/covers.json');
        $parsed = json_decode((string)$raw, true);
        if (is_array($parsed) && isset($parsed['coverPrice'])) { sqlite_set_cover_price((float)$parsed['coverPrice']); }
    }
    if ($hasTables === 0 && is_readable(DATA_DIR . '/tables.json')) {
        $raw = @file_get_contents(DATA_DIR . '/tables.json');
        $parsed = json_decode((string)$raw, true);
        if (is_array($parsed)) { sqlite_save_tables($parsed); }
    }
    if ($hasTabs === 0 && is_dir(TABS_DIR)) {
        $files = glob(TABS_DIR . '/table_*.json') ?: [];
        foreach ($files as $file) {
            if (!preg_match('~table_(\d+)\.json$~', $file, $m)) { continue; }
            $tid = (int)$m[1];
            $raw = @file_get_contents($file);
            $parsed = json_decode((string)$raw, true);
            if (is_array($parsed)) { sqlite_save_tab($tid, $parsed); }
        }
    }
    $cartFiles = glob(CARTS_DIR . '/carrello_tavolo_*.json') ?: [];
    foreach ($cartFiles as $file) {
        if (!preg_match('~carrello_tavolo_(\d+)\.json$~', $file, $m)) { continue; }
        $tid = (int)$m[1];
        $raw = @file_get_contents($file);
        $parsed = json_decode((string)$raw, true);
        if (is_array($parsed)) { sqlite_save_cart($tid, $parsed); }
    }
}
```

---

## 💾 Backup e pulizia 
- ⏱️ `backup_db_daily()` viene schedulato da CLI; `backup_prune.php` rimuove vecchi dump e registra l'esito.
```php
$keepDays = (int)(getenv('RISTO_BACKUP_KEEP_DAYS') ?: 30);
if ($keepDays < 1) { $keepDays = 30; }
...
if (is_dir($dir)) {
    foreach (glob($dir . '/db_*.sqlite*') ?: [] as $file) {
        $mtime = (int)@filemtime($file);
        if ($mtime > 0 && $mtime < $now - ($keepDays * 86400)) {
            if (@unlink($file)) { $removed++; }
        } else {
            $kept++;
        }
    }
}
if (function_exists('app_log')) {
    app_log('backup_prune', ['keepDays' => $keepDays, 'removed' => $removed, 'kept' => $kept]);
}
```

---

## 📦 Export CSV/ZIP portabile 
- 🧭 Genera CSV con header dinamici e BOM UTF-8; se `ZipArchive` non c'e', streamma uno ZIP minimale.
```php
function build_csv_from_data($data, string $type): string {
    $fp = fopen('php://temp', 'r+'); if ($fp === false) return '';
    if ($type === 'calendar') {
        fputcsv($fp, ['date','text']);
        if (is_array($data)) foreach ($data as $k=>$v) { $text = is_array($v)? json_encode($v, JSON_UNESCAPED_UNICODE): (string)$v; fputcsv($fp, [$k,$text]); }
        rewind($fp); $csv=stream_get_contents($fp); fclose($fp); return "\xEF\xBB\xBF".($csv?:'');
    }
    if (is_array($data) && array_keys($data) === range(0, count($data)-1)) {
        $headers=[]; foreach ($data as $row) if (is_array($row)) foreach ($row as $k=>$_) $headers[$k]=true; $headers=array_keys($headers);
        if ($headers) { fputcsv($fp,$headers); foreach($data as $row){ $line=[]; foreach($headers as $h){ $val=is_array($row)&&array_key_exists($h,$row)?$row[$h]:''; if(is_array($val)||is_object($val)) $val=json_encode($val, JSON_UNESCAPED_UNICODE); $line[]=$val; } fputcsv($fp,$line);} }
        else { fputcsv($fp,['value']); foreach($data as $v){ if(is_array($v)||is_object($v)) $v=json_encode($v, JSON_UNESCAPED_UNICODE); fputcsv($fp,[$v]); } }
        rewind($fp); $csv=stream_get_contents($fp); fclose($fp); return "\xEF\xBB\xBF".($csv?:'');
    }
    fputcsv($fp,['key','value']); if (is_array($data)) foreach($data as $k=>$v){ if(is_array($v)||is_object($v)) $v=json_encode($v, JSON_UNESCAPED_UNICODE); fputcsv($fp,[$k,$v]); }
    rewind($fp); $csv=stream_get_contents($fp); fclose($fp); return "\xEF\xBB\xBF".($csv?:'');
}
```
```php
class SimpleZip {
    private array $entries = [];
    private int $offset = 0;

    public function add(string $name, string $data): void {
        $name = str_replace('\\', '/', $name);
        $time = $this->dosTime(); $date = $this->dosDate(); $crc  = crc32($data);
        $clen = strlen($data); $ulen = $clen;
        $lfh = pack('VvvvvvVVVvv', 0x04034b50, 20, 0, 0, $time, $date, $crc, $clen, $ulen, strlen($name), 0);
        $this->entries[] = ['name'=>$name,'crc'=>$crc,'clen'=>$clen,'ulen'=>$ulen,'time'=>$time,'date'=>$date,'offset'=>$this->offset];
        $this->offset += strlen($lfh) + strlen($name) + $clen;
        echo $lfh . $name . $data;
    }

    public function finish(string $filename): void {
        $cd = '';
        foreach ($this->entries as $e) {
            $cdh = pack('VvvvvvvVVVvvvvvVV', 0x02014b50, 0, 20, 0, 0, $e['time'], $e['date'], $e['crc'], $e['clen'], $e['ulen'], strlen($e['name']), 0, 0, 0, 0, $e['offset']);
            $cd .= $cdh . $e['name'];
        }
        $eocd = pack('VvvvvVVv', 0x06054b50, 0, 0, count($this->entries), count($this->entries), strlen($cd), $this->offset, 0);
        echo $cd . $eocd;
    }

    private function dosTime(): int { $t=getdate(); return (($t['hours']&0x1F)<<11) | (($t['minutes']&0x3F)<<5) | (($t['seconds']/2)&0x1F); }
    private function dosDate(): int { $t=getdate(); return (((($t['year']-1980)&0x7F)<<9) | (($t['mon']&0x0F)<<5) | ($t['mday']&0x1F)); }
}
```

---

## 🍳 Cucina: note normalizzate e gruppi per mandata 
- 🧾 Ripulisce le note (NBSP, spazi multipli) e aggrega ordini per batch + nota per evitare duplicati.
```php
function normalize_note(string $s): string {
    $s = html_entity_decode($s, ENT_QUOTES | ENT_HTML5, 'UTF-8');
    $s = str_replace("\xC2\xA0", ' ', $s);
    $s = preg_replace('/\s+/u', ' ', $s) ?? $s;
    return trim($s);
}
...
foreach ($openTableIds as $tableId) {
    $tab = sqlite_load_tab($tableId);
    $byBatch = [];
    foreach (($tab['items'] ?? []) as $it) {
        $id   = (string)($it['id'] ?? ($it['name'] ?? ''));
        $name = (string)($it['name'] ?? $id);
        $qty  = max(1, (int)($it['qty'] ?? 1));
        $noteKey = normalize_note((string)($it['note'] ?? ''));
        $batch = (int)($it['batch'] ?? 1);
        $status = (string)($it['status'] ?? 'pending');

        if (!isset($byBatch[$batch])) { $byBatch[$batch] = ['groups'=>[], 'totPending'=>0, 'totSent'=>0]; }
        $k = $id . '|' . $noteKey;
        if (!isset($byBatch[$batch]['groups'][$k])) {
            $byBatch[$batch]['groups'][$k] = ['id'=>$id, 'name'=>$name, 'note'=>$noteKey, 'pending'=>0, 'sent'=>0];
        }
        if ($status === 'sent') { $byBatch[$batch]['groups'][$k]['sent'] += $qty; $byBatch[$batch]['totSent'] += $qty; }
        else { $byBatch[$batch]['groups'][$k]['pending'] += $qty; $byBatch[$batch]['totPending'] += $qty; }
    }
}
```

