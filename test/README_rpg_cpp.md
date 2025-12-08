# 🎮 Console RPG (C++) - Estratti

Utility per mostrare output colorato in console mantenendo l'allineamento; pronti per un README GitHub.

---

## 👀 Lunghezza visibile ignorando ANSI (`main.cpp`)
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

## ✂️ Troncamento di stringhe colorate senza bleed (`main.cpp`)
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

## 🧱 Righe box con padding corretto (`main.cpp`)
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
