# Tank Card Pro – Tank Level Visualization

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://github.com/hacs/integration) [![GitHub total downloads](https://img.shields.io/github/downloads/jinx-22/tank-card-pro/total?style=flat-square&color=red)](https://github.com/jinx-22/tank-card-pro/releases/) [![GitHub release](https://img.shields.io/github/release/jinx-22/tank-card-pro?include_prereleases=&sort=semver&color=blue)](https://github.com/jinx-22/tank-card-pro/releases/) [![File size](https://img.shields.io/github/size/jinx-22/tank-card-pro/tank-card-pro.js?label=Card%20Size)](https://github.com/jinx-22/tank-card-pro) [![last commit](https://img.shields.io/github/last-commit/jinx-22/tank-card-pro)](https://github.com/jinx-22/tank-card-pro/commits/main) [![stars](https://img.shields.io/github/stars/jinx-22/tank-card-pro)](https://github.com/jinx-22/tank-card-pro/stargazers) [![Donate Bitcoin](https://img.shields.io/badge/%E2%82%BF-Bitcoin-F7931A?style=flat-square)](#bitcoin) [![Donate Lightning](https://img.shields.io/badge/%E2%9A%A1-Lightning-FFD700?style=flat-square)](#lightning)

🇬🇧 **English** · 🇩🇪 [**Deutsch**](https://github.com/jinx-22/tank-card-pro/blob/main/README_DE.md)

---

**Tank Card Pro** is a Home Assistant custom card that visualizes tank levels, total capacity and consumption.

**Tank Card Pro** is the extended edition of the free [Tank Card](https://github.com/jinx-22/tank-card) everything the basic card can do, plus the **advanced settings** (average and daily consumption, range forecasts, refill detection and costs).

**Current version: 0.9.6**

## 🆕 0.9.6

### Changed
- Minor visual refinements and UI polish.
- Improved consistency of the card's appearance.

### Fixed
- Fixed minor bugs and visual inconsistencies.
- General stability and rendering improvements.

## 🆕 0.9.5

- First release of **Tank Card Pro** with the **Advanced settings** panel: average consumption per day, consumption yesterday / today, linear and seasonal range, refill detection, cost of the consumption so far and cost of refilling – see [Advanced settings](#-advanced-settings)
- The Pro badges use short texts (“Ø/day”, “Yesterday”, “Today”) and the currency symbol of your Home Assistant system (“€ so far”, “€ refill”)
- The editor preview and the dashboard now look the same: the card uses a fixed base font (14 px / 20 px, scaled by `font_size`) instead of inheriting it from the surrounding dialog
- Badges: labels are written out and only abbreviated when a badge is too narrow; the font then shrinks down to 0.4 em. Every badge is sized individually. With large fonts or narrow cards the badges switch to one column automatically
- Badges appear in the **order in which you switch them on** (hint in the editor). Existing cards: switch a badge off and on again once to put it in order
- Warning sign **Sensor unavailable** (only when a sensor is selected, never in the card picker); the card picker shows half-filled tanks
- Individual tank names again via `entities[].name` – in the editor there is one input field per tank right below the number of tanks
- Editor: dividers between all blocks, new order in the panels **Display** and **Content** (initial fill directly after the sensor), the number fields of the sliders (card height, font size, wave interval, bubbles) can be typed freely without jumping back, automatic correction of the warning levels, help texts fall back to English
- The configuration stays tidy: default values are removed and the keys are sorted
- Notification automation: no more time lock (a drop from level 1 to level 2 is always reported), the push message of the previous level is removed from the phone, exact interval for every number of hours, values are stored in the automation and can be read back into the editor, the unit in the message text is sanitized
- Warning level 2 can no longer drop below 1 %
- German editor: “Design” instead of “Theme”

<img width="40%" height="auto" alt="Pro" src="https://github.com/user-attachments/assets/e90c872a-9728-473e-aa07-b820dce7ac00" />

---

> **Note:** After the update, hard-reload the dashboard with `Ctrl + F5` and clear the browser cache so that the editor and the card load the new version.

---

## 📖 About Tank Card Pro

Consumption sensors as well as fill-level sensors with absolute values or percentages are supported. Suitable for heating oil, water, diesel, gas, pellets, wood chips and other liquids or bulk materials – as well as free color displays.

The calculation depends on the selected sensor mode:

- **Consumption sensor:** `initial_fill - consumption`
- **Fill-level sensor (L / kg / m³):** direct sensor value
- **Fill-level sensor (%):** percentage of the total capacity

### Highlights

- One or several tanks (1–20) with automatic numbering, a shared label or individual names
- Fill level, total capacity and consumption at a glance
- Consumption and fill-level sensors (absolute or percentage)
- Tank shapes `rect`, `pool` and `capsule`
- Glass or metal tank
- Material- and color-dependent fill gradients / patterns
- Fill-level warning / signaling (glow + optional notification automation)
- Wave animation and rising bubbles (liquids)
- Units `L`, `gal`, `kg`, `m³` or custom, with automatic detection
- Configurable font size (50–200 %) and card height (250–1000 px)
- Optional Home Assistant theme
- Responsive layout (container queries)
- Visual Home Assistant editor
- English and German (follows the HA language)
- Home Assistant conformant card configuration
- Advanced settings: average and daily consumption, range, refill detection, costs

---

# 📦 Installation

## Easy installation → [Open in HACS](https://my.home-assistant.io/redirect/hacs_repository/?owner=jinx-22&repository=tank-card-pro&category=plugin)

## HACS

1. Open **HACS**
2. Select **Frontend**
3. Search for **Tank Card Pro**
4. Install the card
5. Reload Home Assistant or the browser

## Manual

1. Download `tank-card-pro.js`
2. Copy it to `/config/www/community/tank-card-pro/`
3. Add the following resource under **Settings → Dashboards → Resources**:

   `/local/community/tank-card-pro/tank-card-pro.js`

   Type: **JavaScript module**

Then reload the browser, e.g. with **Ctrl + F5**.

---

# ⚙️ Example configuration

```yaml
type: custom:tank-card-pro
title: Tank Card Pro
tank_count: 3
tank_capacity: 1500
initial_fill: 4500
sensor_mode: consumption
consumption_sensor: sensor.heating_oil_consumption_total
content_type: heating_oil
tank_form: rect
tank_style: metal
tank_label: Tank
entities:
  - name: Tank North
  - name: Tank South
  - name: Reserve
show_consumption: true
show_max: true
warn_1: true
warn_1_level: 20
warn_2: true
warn_2_level: 10
warn_glow: true
```

All options that are not listed use their default value. The visual editor only writes values that differ from the defaults.

---

# 📋 Configuration options

| Option               | Default                      | Type    | Description |
|----------------------|------------------------------|---------|-------------|
| `type`               | `custom:tank-card-pro`            | string  | Card type |
| `title`              | `Tank Card Pro`                   | string  | Card title |
| `show_title`         | `true`                       | boolean | Show the title |
| `tank_count`         | `3`                          | number  | Number of tanks (1–20) |
| `tank_capacity`      | `1500`                       | number  | Capacity per tank (in the measuring unit) |
| `initial_fill`       | `tank_count × tank_capacity` | number  | Initial fill of the whole system (empty = full) |
| `sensor_mode`        | `consumption`                | string  | `consumption`, `fill_level_l` or `fill_level_percent` |
| `consumption_sensor` | `""`                         | string  | Consumption sensor (only for `consumption`) |
| `level_sensor`       | `""`                         | string  | Fill-level sensor (both level modes) |
| `unit`               | `auto`                       | string  | `auto`, `L`, `gal`, `m3`, `kg` or a custom unit (e.g. `t`). `auto` uses the unit of the sensor, otherwise the unit system of Home Assistant (`L` / `gal`) |
| `decimals`           | automatic                    | number  | Decimal places (0–5). Empty = 2 for `m³` / `t`, otherwise 0 |
| `tank_form`          | `rect`                       | string  | `rect`, `pool` or `capsule` |
| `tank_style`         | `metal`                      | string  | `metal` or `glass` |
| `gas_tank`           | `false`                      | boolean | Legs and dome (only metal + capsule + 1 tank) |
| `show_unittank`      | `true`                       | boolean | Show the amount per tank in the fill |
| `show_tank_label`    | `true`                       | boolean | Show the tank label |
| `tank_label`         | `Tank`                       | string  | Shared name of the tanks (numbering is added automatically) |
| `entities`           | –                            | list    | Individual tank names: `- name: …` per tank (first entry = tank 1). Tanks without a name use `tank_label` + number (one input field per tank in the editor) |
| `show_max`           | `true`                       | boolean | Show “Max:” |
| `show_current`       | `true`                       | boolean | Show “Current:” |
| `show_fill_level`    | `true`                       | boolean | Show “Level:” |
| `show_consumption`   | `true`                       | boolean | Show “Consumption:” |
| `show_avg`           | `false`                      | boolean | Average consumption per day |
| `show_yesterday`     | `false`                      | boolean | Consumption yesterday |
| `show_today`         | `false`                      | boolean | Consumption today |
| `calc_linear`        | `false`                      | boolean | Linear range |
| `calc_linear_format` | `date`                       | string  | `date`, `days` or `weeks` |
| `calc_seasonal`      | `false`                      | boolean | Seasonal range (at least 300 days of data) |
| `calc_seasonal_format` | `date`                     | string  | `date`, `days` or `weeks` |
| `detect_refill`      | `false`                      | boolean | Show the date of the last refill |
| `refill_threshold`   | `10`                         | number  | A rise of at least this share of the total capacity (%) counts as refill (1–99) |
| `cost_used`          | `false`                      | boolean | Cost of the consumption so far |
| `cost_used_price`    | –                            | number  | Price you paid (empty = no badge) |
| `cost_used_per`      | `l100`                       | string  | Unit of the price: `l100` (100 L), `l`, `gal`, `kg`, `t` or `m3` – depending on the unit |
| `cost_refill`        | `false`                      | boolean | Cost of refilling |
| `refill_to_pct`      | `100`                        | number  | Fill the tank up to this level (%) |
| `cost_refill_price`  | –                            | number  | Current price (empty = no badge) |
| `cost_refill_per`    | `l100`                       | string  | Unit of the price, like `cost_used_per` |
| `content_type`       | `heating_oil`                | string  | Material / color (see below) |
| `custom_color`       | `[33, 150, 243]`             | list    | RGB `[r, g, b]` (only for `content_type: custom`) |
| `liquid_style`       | `classic`                    | string  | `classic` (previous look) or `new` |
| `animation`          | `false`                      | boolean | Wave animation (liquids only) |
| `animation_interval` | `30`                         | number  | Wave interval in seconds (5–60) |
| `bubbles`            | `false`                      | boolean | Rising bubbles (liquids only) |
| `bubble_amount`      | `3`                          | number  | Amount of bubbles (1–8) |
| `warn_1`             | `false`                      | boolean | Enable warning level 1 (orange) |
| `warn_1_level`       | `20`                         | number  | Warning level 1 below this fill level (%), 1–99 |
| `warn_2`             | `false`                      | boolean | Enable warning level 2 (red) |
| `warn_2_level`       | `10`                         | number  | Warning level 2 below this fill level (%), 1–99 |
| `warn_glow`          | `false`                      | boolean | Signal the warning levels visually (glow and fog) |
| `warn_auto`          | `false`                      | boolean | Notification automation (created in the editor, see below) |
| `warn_notify`        | `true`                       | boolean | Home Assistant notification (via the automation) |
| `warn_mobile`        | `false`                      | boolean | Mobile app push notification (via the automation) |
| `warn_repeat`        | `1`                          | number  | Repeat the notification every … (0–100, 0 = no repeat) |
| `warn_repeat_unit`   | `d`                          | string  | `h` (hours) or `d` (days) |
| `warn_time`          | `"14:00:00"`                 | string  | Time of the repeat (only for `warn_repeat_unit: d`) |
| `theme`              | `""`                         | string  | Optional HA theme |
| `font_size`          | `100`                        | number  | Font size in percent (50–200) |
| `card_height`        | `350`                        | number  | Card height in pixels (250–1000). In the sections view the layout tab takes precedence |

**Order of the badges:** the badges (`show_max`, `show_current`, `show_fill_level`, `show_consumption` and the advanced ones) appear in the order of their keys in the configuration. In the editor that is the order in which you switch them on; in YAML you can simply move the lines.

> **Removed since v0.4.0:** `bg_color`. The background follows the Home Assistant theme.

> **Removed since v0.9.2:** hex values for `custom_color` (use `[r, g, b]`) and `%` / `em` / `px` for `font_size` (use a number).

---

# 📊 Sensor modes

### Consumption sensor

```yaml
sensor_mode: consumption
consumption_sensor: sensor.heating_oil_consumption_total
```

Current level:

`current_level = initial_fill - consumption`  
(limited to 0 … total capacity)

### Absolute fill level

```yaml
sensor_mode: fill_level_l
level_sensor: sensor.heating_oil_level
```

The sensor value is used directly as the current level (limited to 0 … total capacity).

### Percentage fill level

```yaml
sensor_mode: fill_level_percent
level_sensor: sensor.heating_oil_level_percent
```

The sensor value (0–100 %) refers to the total capacity:

`total_capacity = tank_count × tank_capacity`  
`current_level = total_capacity × percentage / 100`

If the selected sensor is unavailable, the card shows the last known value (or the initial fill) together with the warning sign **Sensor unavailable**. Without a selected sensor the tanks show the initial fill.

---

# 📏 Units

With `unit: auto` the card takes the unit of the selected sensor (`unit_of_measurement`). If the sensor has no unit (or reports `%`), the unit system of Home Assistant decides (`L` or `gal`). Alternatively choose `L`, `gal`, `m3`, `kg` or enter a custom unit such as `t`.

`tank_capacity` and `initial_fill` are entered in the same measuring unit. By default amounts are shown without decimal places, `m³` and `t` with two. `decimals` (0–5) changes that.

---

# 🛢️ Tank shapes

- `rect` – rectangular tank (cuboid)
- `pool` – cylindrical / rounded tank
- `capsule` – capsule tank

**Tank type**

- `metal` – metal tank
- `glass` – glass tank

**Gas tank**

- `gas_tank: true` – legs and dome (only with `tank_style: metal`, `tank_form: capsule` and exactly one tank)

---

# 🧪 Supported materials & colors

**Materials / bulk goods**

- `heating_oil` – heating oil
- `water` – water
- `diesel` – diesel
- `gas` – gas
- `pellets` – pellets
- `wood_chips` – wood chips
- `custom` – free color via `custom_color`

**Liquid style**

- `classic` – previous look (light at the bottom)
- `new` – new look (light at the top)

> Pellets and wood chips have no wave and no bubbles (bulk goods).

---

# 🚨 Fill-level warnings & notifications

Tank Card Pro supports two configurable warning levels:

- **Warning level 1:** orange
- **Warning level 2:** red

Both levels are off by default and can be enabled independently. For each level you set the fill level in percent below which the warning is triggered (default: 20 % and 10 %). If both levels are active, level 2 is always below level 1 – the editor corrects the values when you leave the field. A hysteresis of 0.5 percentage points prevents the levels from flickering near a threshold.

### Visual signaling

`warn_glow: true` makes the tanks pulse orange (level 1) or red (level 2), with a fading fog behind them. Level 2 pulses faster. With “reduce motion” enabled in the system a static glow is shown instead.

When you enable the first warning level in the editor, `warn_glow` and `warn_notify` are switched on automatically (you can switch them off again).

### Notification automation

A card only runs while a dashboard is open. Notifications are therefore sent by a Home Assistant **automation** that the card editor creates for you:

1. Enable at least one warning level and select a sensor.
2. Switch on `warn_auto` and choose the channels:

   - `warn_notify: true` – Home Assistant notification (bell in the sidebar, also visible on the phone)
   - `warn_mobile: true` – push message to all devices with the Home Assistant Companion app (tapping opens the dashboard)
3. Optionally set `warn_repeat` and `warn_repeat_unit`. As long as the fill level stays below the threshold, the notification is repeated at this interval: with `d` daily at `warn_time`, with `h` every n hours (divisors of 24 follow the clock, e.g. 0:00, 6:00, 12:00, 18:00; all other values count exactly n hours). `0` = no repeat.
4. Click **Create automation**.

The editor shows whether the automation is up to date. Changes to the card settings only apply after **Update automation**; **Read values from automation** takes the stored values back into the editor; **Delete automation** removes it. The automation is named “<card title> Notification”. Please change settings only in the card editor, manual changes are overwritten. Administrator rights are required.

A message is sent whenever the level changes (also when it drops from level 1 to level 2). The message of the previous level is removed, on the phone as well. When the tank is refilled and the level is above the threshold again, the notifications are removed automatically.

The automation of this card is called `tank_card_pro_<sensor>`, the one of the basic card `tank_card_<sensor>` – both editions can be used side by side. Cards with the same sensor share one automation.

---

# 🧮 Advanced settings

The panel **Advanced settings** adds more badges. They appear in the order in which you switch them on. All calculations that need a history use the **long-term statistics** of Home Assistant (hourly values) for older days and the recorder history for the last two days. The data is refreshed every hour and shortly after midnight; the recorder must be enabled.

| Badge | Option | What it shows |
|-------|--------|---------------|
| Average usage per day | `show_avg` | Mean daily consumption of the last 365 days (fewer if the sensor has a shorter history). Days with a refill or a sensor reset are replaced by the mean of the nearest valid days before and after – a refill never counts against the consumption |
| Consumption yesterday | `show_yesterday` | Consumption from 0:00 to 24:00 of yesterday. Rises of at least `refill_threshold` are treated as refill and ignored |
| Consumption today | `show_today` | Consumption since 0:00, refills excluded as above |
| Range (linear) | `calc_linear` | Remaining time at the average consumption trend of the last 365 days. Best result with 365 days of data. Shown as date, days or weeks (`calc_linear_format`) |
| Range (seasonal) | `calc_seasonal` | Remaining time based on the consumption pattern of the year (heating season). Needs at least 300 days of data, missing days up to 365 are filled with the average (`calc_seasonal_format`) |
| Refilled | `detect_refill` | Date of the last refill, found in the sensor history. A rise of at least `refill_threshold` % of the total capacity counts as refill; slow refilling in many small steps is merged into one refill. Resetting a consumption sensor looks like a refill |
| Cost so far | `cost_used` | Consumed amount × price. Enter the price of your last order (`cost_used_price`) and the unit it refers to (`cost_used_per`) |
| Refill cost | `cost_refill` | Order quantity × price. The order quantity is what is missing up to the fill target `refill_to_pct` (default 100 %); in the editor you can also enter the **order quantity** directly. Enter the current price (`cost_refill_price`, `cost_refill_per`) |

Sensors without long-term statistics only provide the days the recorder keeps (10 days by default). The averages are then based on these days, the seasonal range shows “Not enough data”.

```yaml
type: custom:tank-card-pro
sensor_mode: consumption
consumption_sensor: sensor.heating_oil_consumption_total
tank_count: 3
tank_capacity: 1500
initial_fill: 4500
show_consumption: true
show_avg: true
show_yesterday: true
calc_linear: true
calc_linear_format: date
detect_refill: true
refill_threshold: 10
cost_refill: true
cost_refill_price: 1.05
cost_refill_per: l
```

---

# 📸 Screenshot

<img width="40%" height="auto" alt="New-look" src="https://github.com/user-attachments/assets/fdb74b57-51d6-444a-9698-ff5592e45c80" />

---

# 🐛 Issues & Feature Requests

Please provide the following information:

- Home Assistant version
- Tank Card Pro version
- Current configuration
- Relevant error messages
- Short description of the problem

Please remove any personal or sensitive information from configurations and logs.

Create a [GitHub Issue](https://github.com/jinx-22/tank-card-pro/issues).

---

# 🧡 Support & Donations

<div align="center">

### <a id="lightning"></a>Lightning

<img width="32" alt="Lightning" src="https://github.com/user-attachments/assets/0bff59d2-7986-46cf-9d39-17fe0dbb128a" />

`usefulplay52@walletofsatoshi.com`

<img height="300" alt="Lightning - Wallet of Satoshi" src="https://github.com/user-attachments/assets/65cc18d9-05d1-4a00-8ccc-9922fdb54baf" />

### <a id="bitcoin"></a>Bitcoin

<img width="32" alt="Bitcoin" src="https://github.com/user-attachments/assets/f74cad36-8c05-4a33-89cd-b998075af33b" />

`bc1qkz7mtp23cmshxnru96lzgeayu0urlysvqk5vry`

<img height="300" alt="Bitcoin donation" src="https://github.com/user-attachments/assets/196f68e4-b0e8-4f27-bded-8c4fe13b9d45" />

</div>

Thank you for your support — a free ⭐ helps others discover the project:

[![stars](https://img.shields.io/github/stars/jinx-22/tank-card-pro)](https://github.com/jinx-22/tank-card-pro/stargazers)

---
# 📜 License

**Apache-2.0**

---

Made with ❤️ for Home Assistant
