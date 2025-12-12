<h1 align="center">🎸 Portfolio Musicista / Producer</h1>
<p align="center">Landing/portfolio premium per musicisti e producer: hero d’impatto, embed Spotify/YouTube, servizi, galleria, testimonianze e CTA contatto.</p>

---

<h3>✨ Perché è utile</h3>
<ul>
  <li>Mostra subito chi sei: hero + tagline + CTA verso contatto/ascolto.</li>
  <li>Vetrina servizi e testimonianze per aumentare fiducia e conversioni.</li>
  <li>Embed streaming (Spotify/YouTube) con gestione cookie e fallback galleria.</li>
  <li>Palette switchabile (4 temi) per adattarlo a brand e mood diversi.</li>
  <li>Footer contatti completo (email, telefono/WhatsApp, social) già pronto.</li>
</ul>

<h3>📂 Cosa include</h3>
<ul>
  <li><code>index.php</code> con dati in array (<code>$artist</code>, <code>$cta</code>, <code>$social</code>, <code>$testimonials</code>, <code>$contact</code>, <code>$meta</code>, <code>$gallery</code>, <code>$embeds</code>, <code>$services</code>).</li>
  <li><code>Portfolio.css</code> stile base chiaro.</li>
  <li><code>palette-*.css</code>: luxury, minimal, stage, neutral (importane uno dopo il CSS principale).</li>
  <li><code>Immagini/</code>: hero/galleria + favicon.</li>
  <li><code>.htaccess</code>: cache asset e blocco esecuzione/listing in <code>Immagini</code>.</li>
</ul>

<h3>⚡ Come provarlo</h3>
<ol>
  <li>Servi la cartella <code>Portfolio-Musica/</code> (es. <code>php -S localhost:8000</code>).</li>
  <li>Nel &lt;head&gt; importa <code>Portfolio.css</code> e, se vuoi, una sola palette:
    <pre><code>&lt;link rel="stylesheet" href="Portfolio.css"&gt;
&lt;link rel="stylesheet" href="palette-luxury.css"&gt;</code></pre>
  </li>
  <li>Sostituisci le immagini in <code>Immagini/</code> (hero 4:5, gallery 16:9) e le favicon (<code>favicon.ico</code>, <code>favicon.png</code>, <code>favicon-180.png</code>).</li>
</ol>

<h3>🛠️ Personalizza in 5 minuti</h3>
<ul>
  <li>Aggiorna in <code>index.php</code>: artista/tagline/bio, contatti, social, meta (toglici il commento), servizi, embed, galleria.</li>
  <li>Lascia vuoto <code>$testimonials</code> se non vuoi mostrare la sezione.</li>
  <li>Ogni palette sovrascrive solo le variabili CSS: puoi aggiungerne altre duplicando un file <code>palette-*.css</code>.</li>
</ul>

<h3>ℹ️ Note tecniche</h3>
<ul>
  <li>Lazy loading su immagini/galleria; CTA contatti evidenziate on-click.</li>
  <li>Embed caricati solo dopo consenso cookie; valuta tracklist locale come fallback.</li>
  <li>.htaccess richiede <code>AllowOverride All</code> su Apache per applicare cache/protezione.</li>
</ul>

<h3>🚀 Vuoi acquistarlo o averlo su misura?</h3>
<p>Se ti piace il template e vuoi usarlo subito o personalizzarlo sul tuo brand, contattami: posso adattare palette, tipografia, sezioni extra (case study, prezzi, form contatto) e integrare i tuoi asset. Apri una issue o scrivimi e ti rispondo con demo, tempi e prezzo.</p>
