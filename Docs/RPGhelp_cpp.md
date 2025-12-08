# 🎮  RPG (C++) - Estratti

Utility per output colorato e logica di gioco (console). Snippet brevi e subito riusabili.

---

## 👀 Lunghezza visibile ignorando ANSI
- 📏 Conta i caratteri senza considerare le sequenze colore.
```cpp
static size_t visibleLen(const std::string& s) {
    size_t vis = 0;
    for (size_t i = 0; i < s.size();) {
        unsigned char c = static_cast<unsigned char>(s[i]);
        if (c == 0x1B && i + 1 < s.size() && s[i + 1] == '[') {
            size_t j = i + 2;
            while (j < s.size() && s[j] != 'm') j++;
            if (j < s.size()) j++;
            i = j;
        } else { ++vis; ++i; }
    }
    return vis;
}
```

---

## ✂️ Troncamento di stringhe colorate senza bleed
- 🧹 Ferma alla lunghezza visibile richiesta e aggiunge reset finale per non contaminare le righe successive.
```cpp
static std::string truncateVisible(const std::string& s, size_t maxVis) {
    if (visibleLen(s) <= maxVis) return s;
    std::string out; size_t vis = 0;
    for (size_t i = 0; i < s.size() && vis < maxVis;) {
        unsigned char c = static_cast<unsigned char>(s[i]);
        if (c == 0x1B && i + 1 < s.size() && s[i + 1] == '[') {
            size_t j = i + 2;
            while (j < s.size() && s[j] != 'm') j++;
            if (j < s.size()) j++;
            out.append(s, i, j - i);
            i = j;
        } else {
            out.push_back(s[i]); ++i; ++vis;
        }
    }
    out += ansi::reset;
    return out;
}
```

---

## 🧱 Righe box con padding corretto
- 📐 Usa le funzioni sopra per mantenere i bordi allineati in presenza di colori.
```cpp
static void boxLine(const std::string& text) {
    std::string s = text;
    size_t maxVis = UI_WIDTH - 2;
    if (visibleLen(s) > maxVis) s = truncateVisible(s, maxVis);
    size_t pad = (maxVis > visibleLen(s)) ? (maxVis - visibleLen(s)) : 0;
    std::cout << '|' << s << std::string(pad, ' ') << "|\n";
}
```

---

## ⚔️ Avvio combattimento turn-based
- 🎲 Entry point che lancia un encounter con mostri preimpostati (supporta torcia spenta, buio, priorità nemici).
```cpp
bool startCombat(Character& hero,
                 Inventory& inv,
                 const std::vector<std::string>& monsterNames,
                 bool torchLit,
                 bool inDark,
                 bool enemyPriority);
```

---

## 🔥 Danni arma ed elementali
- 🪓 Calcola danno arma principale e bonus elementali (fuoco/ghiaccio/fulmine/ombra/sacro).
```cpp
static int getWeaponDamage(const Inventory& inv, bool torchLit) {
    json items = itemsdb::loadItems();
    if (!items.is_object() || items.empty()) return 0;
    std::string mainHand = (inv.items.size() >= 1) ? inv.items[0] : std::string();
    if (mainHand.empty()) return 0;
    int dmg = 0;
    if (items.contains(mainHand) && items[mainHand].contains("stats")) {
        const auto& st = items[mainHand]["stats"];
        if (mainHand == "torcia") { if (!torchLit) return 0; }
        if (st.contains("danno")) dmg += st["danno"].get<int>();
    }
    return dmg;
}
```
```cpp
static int getWeaponElementDamage(const Inventory& inv, bool torchLit, const char* key) {
    json items = itemsdb::loadItems();
    if (!items.is_object() || items.empty()) return 0;
    std::string mainHand = (inv.items.size() >= 1) ? inv.items[0] : std::string();
    if (mainHand.empty()) return 0;
    if (!items.contains(mainHand) || !items[mainHand].contains("stats")) return 0;
    const auto& st = items[mainHand]["stats"];
    if (std::string(key) == "danni_da_fuoco" && mainHand == "torcia" && !torchLit) return 0;
    if (st.contains(key)) return st[key].get<int>();
    return 0;
}
```

---

## 🏰 Descrizioni stanze dinamiche
- 🗺️ Carica stanze da JSON e restituisce descrizioni variando per oscurità/luce disponibile.
```cpp
struct Room {
    std::string name;
    int oscurita;
    std::string nearDesc; // descrizione delle vicinanze
    std::string farDesc;  // descrizione delle zone più distanti
};

bool loadRooms(const std::string& path, std::unordered_map<std::string, Room>& out);
std::string describeRoom(const Room& r, int luceDisponibile);
```
