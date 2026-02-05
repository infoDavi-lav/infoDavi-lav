<div align="center">
<img src="img/Utility.png" alt="UtilitiesPack logo" width="180" />
<h1>&#x1F6E0;&#xFE0F; UtilitiesPack</h1>
<p>A lightweight utility pack for Paper 1.21.1 with quality-of-life features for staff and players.</p>
<p><strong>Paper 1.21.1 &#x2022; Java 21+</strong></p>
</div>

---

## ✨ Features

### 🔧 Core Features

- **AutoWorkbench**: Virtual crafting table with `SHIFT + right click` on crafting table (hand or inventory)
- **FakeQuit / Ghost Mode**: `/fakequit` hides you from tab and players, optional vanilla join/quit messages
- **AnvilUnlimited**: Removes "Too Expensive!" cost limit; optional PacketEvents bypass + actionbar warning
- **DeathLocation**: Stores last death in SQLite (async), `/deathloc` shows your last death
- **Death Locator Compass**: `/deathlocator` gives a compass pointing to your last death location
- **Handcuffs**: Chainmail chestplate with Curse of Binding that blocks commands while worn

### 🆕 V3 New Features

- **Spawn Teleport**: `/spawn` teleports to world spawn
- **Home System**: `/sethome`, `/home`, `/delhome` with multiple homes support
- **Automatic Bed Home**: Sleeping in a bed sets a 'bed' home automatically (silent mode)
- **Teleport Requests**: `/tpa`, `/tpaccept`, `/tpdeny` for player-to-player teleportation
- **Kit System**: `/kit`, `/createkit`, `/delkit`, `/configkit` for customizable item kits
- **Coordinate Teleport**: `/tppos` for cross-dimensional teleportation
- **Dynamic Command Registration**: Prevents conflicts with other plugins like EssentialsX

---

## ✅ Requirements

- **Paper** 1.21.1
- **Java** 21+
- **PacketEvents** (optional, only for `anvil_unlimited.creative_bypass`)

---

## 📥 Installation

1. Put `UtilitiesPack.jar` into `plugins/`
2. Start or restart the server
3. Edit `plugins/UtilitiesPack/config.yml` if needed
4. Languages live in `plugins/UtilitiesPack/lang`

---

## 📢 Commands

| Command               | Aliases         | Description                     |
| --------------------- | --------------- | ------------------------------- |
| `/utilitiespack`      | `/up`           | Main command                    |
| `/up reload`          |                 | Reload config                   |
| `/fakequit`           |                 | Toggle ghost mode               |
| `/deathloc [player]`  |                 | Show last death (self or other) |
| `/deathlocator`       | `/deathcompass` | Give Death Locator compass      |
| `/handcuffs [player]` | `/manette`      | Give handcuffs                  |

### 🆕 V3 Commands

| Command                                           | Description                             |
| ------------------------------------------------- | --------------------------------------- |
| `/spawn`                                          | Teleport to world spawn                 |
| `/home [name]`                                    | Teleport to home or list homes          |
| `/sethome <name>`                                 | Set a home                              |
| `/delhome <name>`                                 | Delete a home                           |
| `/tpa <player>`                                   | Send teleport request                   |
| `/tpaccept`                                       | Accept teleport request                 |
| `/tpdeny`                                         | Deny teleport request                   |
| `/kit [name]`                                     | Use a kit or list available kits        |
| `/createkit <name>`                               | Create kit from current inventory       |
| `/delkit <name>`                                  | Delete a kit                            |
| `/configkit <name>`                               | Configure kit settings                  |
| `/tppos <x> <y> <z> [world]`                      | Teleport to coordinates                 |
| `/tppos [player/@s/@p/@a/@r] <x> <y> <z> [world]` | Teleport player/selector to coordinates |

---

## 🔑 Permissions

### Core Permissions

| Permission                      | Description              | Default |
| ------------------------------- | ------------------------ | ------- |
| `utilitiespack.reload`          | Reload config            | op      |
| `utilities.fakequit`            | Use /fakequit            | op      |
| `utilities.deathloc.self`       | Use /deathloc (self)     | false   |
| `utilities.deathloc.other`      | Use /deathloc \<player\> | op      |
| `utilities.deathloc.notify`     | Death message on death   | false   |
| `utilities.deathloc.self.click` | Clickable coords (self)  | false   |
| `utilities.deathloc.compass`    | Use /deathlocator        | false   |
| `utilities.handcuffs.give`      | Give handcuffs           | op      |
| `utilities.handcuffs.apply`     | Apply handcuffs          | op      |
| `utilities.handcuffs.remove`    | Remove handcuffs         | op      |

### 🆕 V3 Permissions

| Permission                  | Description                  | Default |
| --------------------------- | ---------------------------- | ------- |
| `utilities.spawn`           | Use /spawn                   | true    |
| `utilities.home.list`       | List own homes               | true    |
| `utilities.home.teleport`   | Teleport to own homes        | true    |
| `utilities.home.set`        | Set homes                    | true    |
| `utilities.home.delete`     | Delete homes                 | true    |
| `utilities.home.limit.X`    | Home limit (X = 1,3,5,10...) | false   |
| `utilities.home.others`     | Teleport to others' homes    | op      |
| `utilities.home.bed`        | Auto-set bed home            | true    |
| `utilities.tpa.send`        | Send teleport requests       | true    |
| `utilities.tpa.accept`      | Accept teleport requests     | true    |
| `utilities.tpa.deny`        | Deny teleport requests       | true    |
| `utilities.kit.use`         | Use kits                     | true    |
| `utilities.kit.create`      | Create kits                  | op      |
| `utilities.kit.delete`      | Delete kits                  | op      |
| `utilities.kit.admin`       | Configure kits               | op      |
| `utilities.teleport.coords` | Use /tppos                   | op      |

---

## 🛡️ LuckPerms Usage

Permissions are standard Bukkit nodes from the table above. Use LuckPerms to grant them to groups or players.

### Basic Commands

```bash
/lp group <group> permission set <perm> true
/lp user <player> permission set <perm> true
/lp group <group> permission unset <perm>
```

### Examples

**Everyone can remove handcuffs:**

```bash
/lp group default permission set utilities.handcuffs.remove true
```

**VIP (deathloc + compass only):**

```bash
/lp group vip permission set utilities.deathloc.self true
/lp group vip permission set utilities.deathloc.compass true
```

**Optional:**

```bash
/lp group vip permission set utilities.deathloc.self.click true
/lp group vip permission set utilities.deathloc.notify true
```

---

## ⚙️ Configuration

Main sections (see full file in `plugins/UtilitiesPack/config.yml`):

```yaml
prefix: "<gradient:#2b0a3d:#6a0dad>[UtilitiesPack]</gradient>"

lang:
  default: it_it
  use_player_locale: true
  use_config_overrides: false

autoworkbench:
  enabled: true
  inventory_click: RIGHT

fakequit:
  enabled: true
  show_to_ops: true
  send_fake_join: true
  use_vanilla_messages: true

anvil_unlimited:
  enabled: true
  mode: UNCAP
  set_value: 60
  creative_bypass: false
  debug: false
  actionbar_enabled: true
  actionbar_cooldown_ms: 800
  repair_cost_tag_cap: true
  repair_cost_tag_limit: 39

deathloc:
  enabled: true
  database: "deathlocations.db"
  notify_on_death: true

handcuffs:
  enabled: true
  block_commands: true
  remove_mode: SHIFT

# V3 New Features
spawn:
  enabled: true
  cooldown_seconds: 5

homes:
  enabled: true
  database: "homes.db"
  default_limit: 3
  cooldown_seconds: 3

teleport:
  enabled: true
  cooldown_seconds: 5

kits:
  enabled: true
  database: "kits.db"
  default_cooldown_hours: 24

# Commands to disable (prevents registration conflicts with other plugins)
disabled_commands:
  - "spawn" # Disable if using EssentialsX spawn
  - "home" # Disable if using EssentialsX homes
  - "sethome" # Disable if using EssentialsX homes
  - "delhome" # Disable if using EssentialsX homes
  - "tpa" # Disable if using EssentialsX teleport
  - "tpaccept" # Disable if using EssentialsX teleport
  - "tpdeny" # Disable if using EssentialsX teleport
  - "kit" # Disable if using EssentialsX kits
  - "createkit" # Disable if using other kit plugins
  - "delkit" # Disable if using other kit plugins
  - "configkit" # Disable if using other kit plugins
```

---

## 🌐 Languages

**Supported:** `it_it`, `en_us`, `ru_ru`

Auto locale per player when enabled.

---

## 🔩 AnvilUnlimited Notes

- `anvil_unlimited.creative_bypass` uses PacketEvents to allow costs above 39 while keeping the real cost
- With bypass on, Java clients do not show the red "Too Expensive" text; use the actionbar message instead
- Bedrock clients via Geyser can still show "Too Expensive" due to client UI limits
- Actionbar text key: `anvil_too_expensive_actionbar` (supports `{cost}`), override via `lang/*.yml` or `messages.*`

---

## 💾 Database

- **DeathLocation** uses SQLite (async). File set by `deathloc.database`
- **V3 Home System** uses SQLite (async). File set by `homes.database`
- **V3 Kit System** uses SQLite (async). File set by `kits.database`

---

## 👻 Ghost Mode Details

- ✅ Hidden from tab and in-game for normal players
- ✅ Optional visibility for ops
- ✅ Vanilla localized join/quit messages (yellow)
- ✅ Mobs do not target ghost players
- ✅ Metadata `vanished`/`vanish`/`ghost` set for TAB integrations

---

## 🛡️ Handcuffs Details

**Item:** Chainmail chestplate with Curse of Binding

### Usage

- **Apply:** Right click a player while holding the item
- **Remove:** SHIFT or sprint (CTRL) + right click by authorized player (configurable)
- **Creative:** Can drag the chestplate into inventory if permitted

### Restrictions While Worn

- ❌ Cannot attack
- ❌ Cannot trade
- ❌ Cannot open doors/containers
- ❌ Cannot interact with entities/blocks

### Allowed While Worn

- ✅ Eating
- ✅ Picking up items
- ✅ Dropping items

---

## 🏠 V3 Home System

- Set homes with `/sethome <name>` at your current location
- Teleport to homes with `/home <name>` or list all with `/home`
- Delete homes with `/delhome <name>`
- Home limits controlled by permissions: `utilities.home.limit.X` (X = number)
- Default limit configurable in config.yml
- Cooldown system prevents spam
- SQLite database for persistent storage

---

## ✈️ V3 Teleport System

- Send teleport requests with `/tpa <player>`
- Accept requests with `/tpaccept`, deny with `/tpdeny`
- Requests auto-expire after 60 seconds
- Cooldown system prevents spam
- Only one pending request per player at a time

---

## 📦 V3 Kit System

### Features

- Create kits from your inventory with `/createkit <name>`
- Give kits to players with `/kit <name>` or list all with `/kit`
- Delete kits with `/delkit <name>`

### Configuration

Configure kit settings with `/configkit <name>`:

- `cooldown <hours>` - Set cooldown in hours (default: 24)
- `onetime <true/false>` - Set if kit can only be claimed once
- `enabled <true/false>` - Enable/disable the kit
- `info` - Show all kit settings

### Storage

- SQLite database for persistent storage
- Individual kit configuration (cooldown, one-time use, enabled status)
- Admin permissions required for kit management

---

## 📍 V3 Spawn System

- `/spawn` teleports to world spawn location
- Configurable cooldown system
- Works with any world's spawn point

---

## 🛏️ V3 Bed Home System

- Sleeping in a bed automatically sets a 'bed' home at that location
- Silent mode: `bed_home_silent: true` disables messages
- Protected: 'bed' home cannot be deleted with `/delhome bed`
- Requires `utilities.home.bed` permission (default: true)
- Only works when home system is enabled

---

## ✈️ V3 Coordinate Teleport

### Features

- `/tppos <x> <y> <z> [world]` for cross-dimensional teleportation
- `/tppos [player/@s/@p/@a/@r] <x> <y> <z> [world]` for teleporting others

### Selector Support

- `@s` (self)
- `@p` (nearest)
- `@a` (all)
- `@r` (random)

### Examples

```bash
/tppos 100 64 200
/tppos @a 0 64 0 world_nether
```

### Notes

- **Command block compatible**: `@p` finds nearest player to the command block
- Perfect for RP events and automated teleportation systems
- Supports teleport timer and delay system
- Requires `utilities.teleport.coords` permission (default: op)

---

## ⚙️ V3 Dynamic Command System

- Commands are registered dynamically to prevent conflicts
- Use `disabled_commands` list in config.yml to disable specific commands
- Perfect compatibility with EssentialsX and other plugins
- **Example:** Add `"home"` to disabled_commands to use EssentialsX homes instead

---

## 📄 License

All rights reserved unless stated otherwise by the author.

---

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
