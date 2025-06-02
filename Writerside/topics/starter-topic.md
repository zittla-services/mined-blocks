# MinedBlocks - Plugin Design Document

## ✨ Purpose

A Spigot plugin that tracks the number of specific blocks mined or harvested by players, including logs, ores, and crops/plants. It also provides aggregated statistics and PlaceholderAPI placeholders for integration with scoreboard plugins.

---

## 📊 Block Categories to Track

### 1. **Logs** (All types)
> Includes: Individual tracking + Combined total under `logs_total`

### 2. **Ores** (All variants counted as one)
> Includes: Individual tracking + Combined total under `ores_total`

### 3. **Crops/Plants** (Only fully grown)

> Includes: Individual tracking + Combined total under `plants_total`

---

## 🔎 Detection Logic

* Listen to `BlockBreakEvent`
* Check if the block is in the tracked list
* For crops/plants: Check block maturity
* Increment player-specific count for that block
* Update aggregate category count (logs, ores, plants)

---

## 📂 Data Storage Format

* One file per player (e.g., `playerUUID.yml`) or use SQLite database
* Example YAML structure:

```yaml
logs:
  oak_log: 50
  all_logs: 300
ores:
  diamond_ore: 10
  all_ores: 80
plants:
  wheat: 20
  all_plants: 65
```

---

## 🔹 Placeholders via PlaceholderAPI

General format:

```
%minedblocks_<category>_<block>%
```

### Examples:

* `%minedblocks_log_oak_log%`

---

## 📊 Scoreboard Integration

Supports any scoreboard plugin compatible with PlaceholderAPI.
---

## 🛠️ Configuration Options (config.yml)

```yaml
save-interval: 600 # seconds
track-deepslate-variants: true
track-only-mature-plants: true
```

---

## 📖 Development Phases

1. Register core block break detection
2. Implement player data save/load system
3. Aggregate category counts
4. PlaceholderAPI integration
5. Optional: stat reset, reload command
6. Documentation and testing
