<div align="center">
  <img src="img/daynightcicle-logo.svg" alt="DayNightCicle logo" width="180" />
  <h1>&#x1F324;&#xFE0F; DayNightCicle</h1>
  <p>DayNightCicle is a lightweight Paper plugin that lets you extend day and night length in minutes via YAML and live commands.</p>
  <p><strong>Paper 1.21+ &#x2022; Java 21</strong></p>
</div>

<hr/>

<h2>&#x2728; Features</h2>
<ul>
  <li>&#x2600;&#xFE0F;&#x1F319; Set custom day and night duration in minutes.</li>
  <li>&#x1F30D; Apply to all overworlds or specific worlds.</li>
  <li>&#x2699;&#xFE0F; In-game commands to reload, check status, set values, and manage sleep overrides.</li>
  <li>&#x1F634; Sleep override list to count selected players even if other plugins ignore them.</li>
  <li>&#x1F4AC; Built-in language files (it_it, us_en).</li>
</ul>

<h2>&#x1F310; Languages</h2>
<ul>
  <li>Set <code>lang</code> in <code>config.yml</code> to <code>it_it</code> or <code>us_en</code>.</li>
  <li><code>en_us</code> is accepted and mapped to <code>us_en</code>.</li>
</ul>

<h2>&#x1F4DD; Commands</h2>
<ul>
  <li><code>/giornolungo</code> - show help.</li>
  <li><code>/giornolungo reload</code> - reload config.</li>
  <li><code>/giornolungo status</code> - show current settings.</li>
  <li><code>/giornolungo set day &lt;min&gt; night &lt;min&gt;</code> - update and save.</li>
  <li><code>/giornolungo nosleeplist</code> - show sleep override list.</li>
  <li><code>/giornolungo sleeplist add &lt;player&gt;</code> - add a player to the sleep override list.</li>
  <li><code>/giornolungo sleeplist remove &lt;player&gt;</code> - remove a player from the sleep override list.</li>
</ul>

<h2>&#x2699;&#xFE0F; Config</h2>
<pre><code>lang: it_it
cycle:
  day_minutes: 20
  night_minutes: 10
  min_minutes: 10
sleep_skip_delay_seconds: 5
worlds: []
</code></pre>

<h2>&#x1F634; Sleep Override List</h2>
<p>The plugin creates <code>sleep-override.json</code> in the plugin data folder. Players in this list will be counted even if another plugin marks them as sleep-ignored.</p>
<pre><code>{
  "players": [
    "KillerItaly"
  ]
}
</code></pre>
<p>Player names are case-insensitive. If you edit the file manually, run <code>/giornolungo reload</code> afterward.</p>

<h2>&#x1F680; Install</h2>
<ol>
  <li>Drop the jar into <code>plugins/</code>.</li>
  <li>Start the server to generate <code>plugins/DayNightCicle/config.yml</code>.</li>
  <li>Edit the config and run <code>/giornolungo reload</code>.</li>
</ol>

<h2>&#x1F517; Links</h2>
<table>
  <tr>
    <td align="center" colspan="2">
      <a href="https://davi-k-portfolio.netlify.app/" target="_blank" rel="noopener">
        <img src="../../img/avatar.png" alt="Portfolio" width="180" />
      </a>
      <div>Portfolio</div>
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="https://www.linkedin.com/in/davide-k-9a7a99375/" target="_blank" rel="noopener">
        <img src="../../img/linkedin.png" alt="LinkedIn" width="64" />
      </a>
      <div>LinkedIn</div>
    </td>
    <td align="center">
      <a href="mailto:info.davi.lav@gmail.com" target="_blank" rel="noopener">
        <img src="https://www.gstatic.com/images/branding/product/1x/gmail_2020q4_48dp.png" alt="Email" width="64" />
      </a>
      <div>Email</div>
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="https://buymeacoffee.com/infodavik" target="_blank" rel="noopener">
        <img src="../../img/bmc-button.png" alt="Buy me a beer on BuyMeACoffee" width="240" />
      </a>
      <div>Buy me a beer</div>
    </td>
    <td align="center">
      <a href="https://ko-fi.com/infodavik" target="_blank" rel="noopener">
        <img src="../../img/support_me_on_kofi_dark.webp" alt="Support me on Ko-fi" width="240" />
      </a>
      <div>Ko-fi</div>
    </td>
  </tr>
</table>




