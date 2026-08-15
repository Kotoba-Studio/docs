---
description: PlaceholderAPI, Currency Bridge và Custom Menu Engine.
icon: puzzle-piece
---

# Framework và menu

## Framework và menu

### Placeholder System

KCore hỗ trợ internal placeholder và PlaceholderAPI expansion `%kcore_*%`.

```
%kcore_version%       → R01
%kcore_build%         → v9
%kcore_style%         → style hiện tại
%kcore_home_count%    → số home
%kcore_homes%         → số home
%kcore_balance%       → balance đầy đủ
%kcore_balance_short% → balance rút gọn
%kcore_shards%        → shards đầy đủ
%kcore_shards_short%  → shards rút gọn
%kcore_tpa_auto%      → true/false
```

Dynamic setting dùng `%kcore_setting_<setting_id>%`. KCore đổi underscore thành hyphen trước khi lookup.

```
%kcore_setting_public_chat%
%kcore_setting_teleport_requests%
%kcore_setting_tpa_confirm_menu%
%kcore_setting_night_vision%
%kcore_setting_player_time%
```

Mode trả về chữ thường. Menu context hỗ trợ `{player}`, `{uuid}`, `{world}`, `{x}`, `{y}`, `{z}`, `{args}`, `{arg_count}`, `{arg_1}` và các argument tiếp theo.

Nếu PlaceholderAPI tồn tại, KCore parse PAPI placeholder trong menu text.

```yaml
placeholders:
  balance-cache-seconds: 5
  max-cache-entries: 1024
```

Economy và shards placeholder trả cache rồi refresh async. Chúng không block server tick.

### Currency Bridge

```yaml
currencies:
  balance:
    provider: auto
    symbol: "₫"
  shards:
    provider: auto
    symbol: "✦"
```

Provider ID được hỗ trợ: `balance`, `shards`, `vault`, `kessentials`, `playerpoints`, `kshards` và `solarshards`.

Bridge phục vụ placeholder, leaderboard, profile, RTP cost và refund.

### Custom Menu Engine

Menu nằm tại `plugins/KCore/menus/*.yml`. Built-in gồm `main.yml` và `example-pro.yml`.

```
/kmenu open <menu> [args...]
/kmenu menu <menu> [args...]
/kmenu reload
/kmenu list
/kmenu validate
```

KCore có thể đăng ký `open-commands` vào Bukkit command map.

```yaml
id: example
enabled: true
title: "<#d8c8ff>Example"
rows: 5
permission: kcore.menu
update-interval-ticks: 40
open-commands:
  - example
```

Dùng `size: 45` thay cho `rows: 5` nếu muốn. `open-requirements`, `open-deny-actions`, `open-actions` và `close-actions` điều khiển lifecycle.

Filler hỗ trợ `material`, `name` và các item flag. Item nhận `slot`, `slots` hoặc `slot-range`. Field thường dùng: `material`, `amount`, `name`, `lore`, `head-owner`, `custom-model-data`, `glow`, `item-flags`, `hide-attributes` và `priority`.

Click group gồm `left`, `right`, `middle`, `shift-left`, `shift-right` và `any`. Loader vẫn nhận direct form như `left-click-actions`.

Action hỗ trợ `[message]`, `[actionbar]`, `[title]`, `[sound]`, `[player]`, `[console]`, `[broadcast]`, `[open]`, `[refresh]`, `[close]` và `[delay]`.

```yaml
actions:
  left:
    - "[sound] minecraft:ui.button.click 0.8 1.1"
    - "[message] <#bfe8d0>Hello {player}!"
    - "[delay] 10"
    - "[player] profile"
  right:
    - "[refresh]"
```

Title action dùng payload `title|subtitle|fade-in|stay|fade-out`.

Requirement hỗ trợ permission, world, string comparison và number comparison. Operators gồm `equals`, `not-equals`, `contains`, `starts-with`, `ends-with`, `regex`, `>`, `>=`, `<` và `<=`.

```yaml
click-requirements:
  requirements:
    use-permission:
      type: permission
      permission: kcore.menu
click-deny-actions:
  - "[message] <#ffb8c2>Bạn không thể sử dụng nút này."
```

```yaml
menus:
  enable-open-commands: true
  click-cooldown-ms: 120
  minimum-update-interval-ticks: 20
  max-runtime-warnings: 256
```

Minimum interval chặn refresh mỗi tick. Click cooldown giảm double-click spam. Warning set có giới hạn tránh memory growth.

Cần `kcore.menu`. Quản trị menu cần `kcore.menu.admin`.
