---
description: Player Settings, Profile, Leaderboards, Vaults và styles tích hợp.
icon: user-gear
---

# Người chơi và giao diện

## Người chơi và giao diện

### Player Settings

Mở GUI bằng `/settings` hoặc `/setting`. KCore lưu setting theo từng người chơi qua IO executor riêng.

Boolean mặc định:

```
bounty-alerts, public-chat, payments, scoreboard
teleport-requests, teleport-here-requests, kill-messages, private-chat
tpa-confirm-menu, tpa-accept-menu, mob-spawn, action-bar
totem-effects, crystal-effects, order-notifications, quick-buy-sound
night-vision, tpa-auto, phantom
```

Mặc định `night-vision` và `tpa-auto` tắt. Các setting khác mặc định bật.

`player-time` cycle `SERVER → DAY → NIGHT`. `player-weather` cycle `SERVER → CLEAR → RAIN`.

KCore áp dụng trực tiếp chat filtering, TPA policy, auto accept, night vision, time, weather, phantom và mob spawn. `order-notifications` và `quick-buy-sound` là integration flag cho plugin khác.

```yaml
settings:
  mob-spawn:
    radius-blocks: 100.0
```

Mob spawn opt-out không đổi gamerule. KCore chặn NATURAL, PATROL, RAID, REINFORCEMENTS, VILLAGE\_INVASION, JOCKEY, MOUNT và TRAP trong bán kính quanh player opt-out.

Khi player tắt phantom, KCore chặn spawn, target và damage liên quan player đó. Cần `kcore.settings`.

### Profile và achievement

```
/profile
/myprofile
```

Profile có thể hiện player head, rank, balance, shards, kills, deaths, homes, home policy, TPA policy và achievements.

```yaml
profile:
  achievements:
    rich-balance: 1000000
    shards: 1000
```

Achievement UI cũng hiển thị progression home. Cần `kcore.profile`.

### Leaderboards

```
/baltop
/balancetop
/shardstop
/shardtop
```

```yaml
currencies:
  leaderboard:
    entries-per-page: 28
    fetch-limit: 300
    cache-seconds: 300
    scan-limit: 300
    scan-batch-size: 32
```

KCore cung cấp balance top và shards top. GUI có account card, điều hướng trang, cache và provider scan async. Cần `kcore.baltop` hoặc `kcore.shardstop`.

### Player Vaults

```
/pv [number]
/vault
/playervault
```

```yaml
enabled: true
max-vaults: 15
default-vaults: 1
size: 54
open-cooldown-millis: 500
```

Giới hạn theo node `kcore.vaults.1`, `.3`, `.5`, `.10` và `.15`. Mở vault cần `kcore.vault`.

```yaml
anti-loss:
  atomic-save: true
  session-lock: true
  crash-journal: true
  journal-min-interval-millis: 750
  block-drop-while-open: true
  block-pickup-while-open: true
  block-commands-while-open: true
  force-player-save-on-close: true
```

Vault không thể mở trong hai session. KCore có thể chặn drop, pickup và command khi vault mở. Default command whitelist gồm `/msg`, `/tell`, `/w`, `/reply` và `/r`.

Crash journal hỗ trợ recovery và debug. Save dùng atomic, session-safe flow.

### Styles tích hợp

Theme nằm tại `styles/<style>.yml`. Nhóm GUI có `home`, `warp`, `settings`, `spawn`, `setspawn`, `tpa`, `leaderboard`, `vault`, `profile` và `rtp`.

Style file điều khiển title, size, filler, slot, material, item name, lore, trạng thái on/off, navigation, TPA layout và profile cards.

{% hint style="info" %}
Chỉnh style file khi muốn thay đổi giao diện toàn server. Cách này sạch hơn hard-code message.
{% endhint %}
