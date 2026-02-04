<div align="center">
  <img src="img/daynightcicle.png" alt="DayNightCicle logo" width="180" />
  <h1>&#x1F324;&#xFE0F; DayNightCicle</h1>
  <p>DayNightCicle is a lightweight Paper plugin that lets you extend day and night length in minutes via YAML and live commands with integrated AFK system.</p>
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
  <li>&#x1F9D8; Integrated AFK system with configurable behaviors and sleep counting.</li>
  <li>&#x1F6E1;&#xFE0F; Smart movement detection (ignores mob pushing, phantom attacks).</li>
  <li>&#x1F3F7;&#xFE0F; Customizable AFK display with prefix/suffix options.</li>
</ul>

<h2>&#x1F310; Languages</h2>
<ul>
  <li>Set <code>lang</code> in <code>config.yml</code> to <code>it_it</code> or <code>us_en</code>.</li>
  <li><code>en_us</code> is accepted and mapped to <code>us_en</code>.</li>
</ul>

<h2>&#x1F4DD; Commands</h2>
<ul>
  <li><code>/daynightcicle</code> or <code>/dnc</code> - show help.</li>
  <li><code>/daynightcicle reload</code> - reload config.</li>
  <li><code>/daynightcicle status</code> - show current settings and AFK players.</li>
  <li><code>/daynightcicle set day &lt;min&gt; night &lt;min&gt;</code> - update and save.</li>
  <li><code>/daynightcicle nosleeplist</code> - show sleep override list.</li>
  <li><code>/daynightcicle sleeplist add &lt;player&gt;</code> - add a player to the sleep override list.</li>
  <li><code>/daynightcicle sleeplist remove &lt;player&gt;</code> - remove a player from the sleep override list.</li>
  <li><code>/afk</code> - toggle AFK status manually.</li>
</ul>

<h2>&#x2699;&#xFE0F; Config</h2>
<pre><code>lang: it_it
cycle:
  day_minutes: 20
  night_minutes: 10
  min_minutes: 10
sleep_skip_delay_seconds: 5
afk_timeout_minutes: 5
afk:
  remove_on_move: true
  remove_on_chat: true
  remove_on_interact: true
  invulnerable: false
  can_be_moved: true
  ignored_by_mobs: false
  counts_for_sleep: true
  can_pickup_items: false
  frozen: false
  display_text: "AFK"
  use_prefix: false
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
<p>Player names are case-insensitive. If you edit the file manually, run <code>/daynightcicle reload</code> afterward.</p>

<h2>&#x1F9D8; AFK System</h2>
<p>The plugin includes a comprehensive AFK system that integrates with the sleep mechanics:</p>
<ul>
  <li><strong>Smart Detection</strong>: Distinguishes between player movement and mob pushing</li>
  <li><strong>Configurable Triggers</strong>: Movement, chat, interaction detection</li>
  <li><strong>Sleep Integration</strong>: AFK players can count as "sleeping" for night skip</li>
  <li><strong>Display Options</strong>: Customizable prefix/suffix in tab list</li>
  <li><strong>Protection Features</strong>: Invulnerability, mob targeting, item pickup control</li>
</ul>

<h2>&#x1F680; Install</h2>
<ol>
  <li>Drop the jar into <code>plugins/</code>.</li>
  <li>Start the server to generate <code>plugins/DayNightCicle/config.yml</code>.</li>
  <li>Edit the config and run <code>/daynightcicle reload</code>.</li>
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









