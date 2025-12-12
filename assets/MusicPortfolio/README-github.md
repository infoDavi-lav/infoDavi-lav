<h1 align="center">Portfolio Musicista / Producer</h1>
<p align="center">Landing/portfolio premium pensata per mostrare musica, servizi e contatti con un look moderno.</p>

---

## Perche conviene
- Presentazione immediata: hero con bio sintetica, CTA doppia e highlight brano demo.
- Pensato per vendere: vetrina servizi e testimonianze progettate per ispirare fiducia.
- Adattabile a ogni brand: 4 palette pronte, tipografia curata, layout responsive.
- Privacy-aware: embed esterni caricati solo dopo consenso ai cookie.
- Facile da riempire: dati organizzati in array PHP, pronti per i tuoi contenuti reali.

## Cosa c'e dentro
- `index.php`: struttura completa con blocchi dati (`$artist`, `$cta`, `$social`, `$testimonials`, `$services`, `$embeds`, `$gallery`, `$meta`, `$contact`).
- `Portfolio.css`: stile base; `palette-*.css`: quattro varianti cromatiche gia pronte.
- `Immagini/`: placeholder per hero e galleria + favicon.
- `.htaccess`: caching statici e protezione cartella immagini.

## Sezioni principali
- Hero con bio breve, tag competenze e pulsanti contatto/ascolto.
- Blocchi streaming (Spotify/YouTube) con placeholder e consenso cookie integrato.
- Griglia competenze e servizi di esempio gia impostate per copy commerciale.
- Testimonianze e galleria per social proof e atmosfera visiva.
- Footer completo con contatti e social pronti per essere personalizzati.

## Mini grafica HTML (senza JS)
Snippet pronto da incollare in una pagina statica; include stile inline e zero dipendenze.

```html
<div class="mini-portfolio">
  <div class="mini-left">
    <small class="pill">Portfolio demo</small>
    <h2>Artista Esempio</h2>
    <p class="tag">Ruolo o stile - Bio sintetica di esempio pronta per essere sostituita.</p>
    <div class="tags">
      <span>Servizio 1</span><span>Servizio 2</span><span>Servizio 3</span>
    </div>
    <div class="actions">
      <a class="btn" href="#">Ascolta</a>
      <a class="btn ghost" href="#">Contatta</a>
    </div>
  </div>
  <div class="mini-right">
    <div class="card">
      <div class="wave"></div>
      <div class="track">
        <strong>Brano demo</strong>
        <span>Genere - Mood</span>
      </div>
      <button type="button">Play</button>
    </div>
  </div>
</div>
<style>
.mini-portfolio{display:grid;grid-template-columns:1.1fr 0.9fr;gap:24px;max-width:880px;margin:32px auto;padding:24px;border-radius:16px;background:linear-gradient(135deg,#101722,#1e2a3d);color:#e8edf5;font-family:"Segoe UI",sans-serif;box-shadow:0 20px 60px rgba(0,0,0,.25);}
.mini-left h2{margin:8px 0 6px;font-size:28px;letter-spacing:-0.02em;}
.mini-left .tag{margin:0 0 14px;color:#b7c3d4;line-height:1.5;}
.pill{display:inline-block;padding:6px 10px;border-radius:999px;border:1px solid #314666;color:#a7b7ce;background:rgba(255,255,255,.04);font-size:12px;letter-spacing:.02em;}
.tags{display:flex;flex-wrap:wrap;gap:8px;margin:0 0 14px;}
.tags span{padding:6px 10px;border-radius:10px;background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.08);font-size:12px;}
.actions{display:flex;gap:10px;align-items:center;}
.btn{display:inline-flex;align-items:center;justify-content:center;padding:10px 14px;border-radius:10px;border:1px solid #4bb4ff;background:#4bb4ff;color:#0c1522;font-weight:700;text-decoration:none;min-width:110px;}
.btn.ghost{background:transparent;border-color:#4bb4ff;color:#dbe8f8;}
.mini-right{display:flex;align-items:center;justify-content:center;}
.card{width:100%;max-width:320px;padding:18px;border-radius:14px;background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.08);box-shadow:0 8px 28px rgba(0,0,0,.25);}
.wave{height:70px;margin-bottom:14px;border-radius:10px;background:repeating-linear-gradient(90deg,rgba(75,180,255,.4) 0,rgba(75,180,255,.4) 12px,rgba(75,180,255,.2) 12px,rgba(75,180,255,.2) 24px);}
.track{display:flex;flex-direction:column;gap:4px;margin-bottom:14px;}
.track strong{font-size:16px;}
.track span{color:#b7c3d4;font-size:13px;}
.card button{width:100%;padding:10px;border-radius:10px;border:1px solid #4bb4ff;background:transparent;color:#dbe8f8;font-weight:700;cursor:pointer;}
.card button:hover{background:rgba(75,180,255,.1);}
@media (max-width:720px){.mini-portfolio{grid-template-columns:1fr;padding:18px;}.mini-right{order:-1;}}
</style>
```

## Ti serve su misura?
Template ideale per artisti, producer, studi e label che vogliono una presenza premium senza ripartire da zero. Scrivimi per una versione brandizzata o per integrare sezioni extra (pricing, case study, form contatto, integrazioni playlist).
