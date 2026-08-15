---
description: Teleport Service, Spawn, Homes, Warps, TPA và Random Teleport.
icon: person-walking-arrow-right
---

# Di chuyển

## Di chuyển

### Teleport Service

Home, Warp, Spawn, TPA và nhiều flow dùng teleport service chung.

```yaml
teleport:
  warmup-seconds: 5
  cancel-on-move: true
  cancel-distance: 0.20
```

Sound start, countdown, success, cancelled và failed có cấu hình riêng. Mỗi sound hỗ trợ `enabled`, `sound`, `volume` và `pitch`.

`kcore.teleport.bypass-warmup` bỏ qua thời gian chờ.

### Spawn

```
/spawn
/spawn now
/setspawn
/setspawn confirm
```

`/spawn` mở GUI khi `spawn.gui-on-command: true`. `/spawn now` bắt đầu teleport ngay. `/setspawn` mở xác nhận khi `setspawn-confirm-gui: true`. `/setspawn confirm` ghi vị trí ngay.

Cần `kcore.spawn` để dùng Spawn. Cần `kcore.admin.setspawn` để đặt Spawn.

### Homes

```
/home [name]
/homes
/sethome [name]
/delhome <name>
```

```yaml
homes:
  default-limit: 3
  maximum-limit: 10
  default-name: home
  gui-on-no-args: true
```

Tên home chỉ nhận `A-Z`, `a-z`, `0-9`, `_` và `-`. Tên dài tối đa 24 ký tự.

Giới hạn resolve qua permission legacy và `policy.yml`. Node legacy gồm `kcore.homes.3`, `kcore.homes.5` và `kcore.homes.10`.

Policy mặc định cấp 3 homes cho `default`. Các rank `kplus` đến `kinfinity` nhận 5 đến 10 homes. Donut layout dùng slot `11-15` cho home.

Cần `kcore.home`, `kcore.sethome` và `kcore.delhome`.

### Warps

```
/warp [name]
/warps
/setwarp <name>
/delwarp <name>
```

`/warp` không có argument có thể mở GUI qua `warps.gui-on-no-args: true`. Policy có thể thay đổi warmup theo rank.

Cần `kcore.warp`. Tạo và xóa warp cần `kcore.admin.warp`.

### TPA

```
/tpa [player]
/tpahere [player]
/tpaccept [player]
/tpadeny [player]
/tpacancel
/tpaauto [on|off]
/tpatoggle [on|off]
/confirmmenu <on|off>
/acceptmenu <on|off>
```

Alias: `/tphere`, `/tpyes`, `/tpdeny` và `/tpno`.

```yaml
tpa:
  gui:
    enabled: true
    sender-confirm: true
    receiver-popup: true
  request-timeout-seconds: 60
  send-cooldown-seconds: 5
  max-incoming-requests: 8
  warmup-seconds: 5
  cancel-on-move: true
  gui-on-no-args: true
  request-gui-on-multiple: true
```

KCore lưu outgoing/incoming request, timeout, cooldown, token sequence và GUI. Người gửi có thể xác nhận trước khi request được tạo. Khi receiver accept, request được consume trước teleport warmup.

Setting `tpa-auto` tự nhận request. `teleport-requests` và `teleport-here-requests` quyết định có nhận request. `tpa-confirm-menu` và `tpa-accept-menu` điều khiển GUI.

Node: `kcore.tpa`, `kcore.tpahere`, `kcore.tpaccept`, `kcore.tpadeny`, `kcore.tpacancel`, `kcore.tpaauto`, `kcore.confirmmenu`, `kcore.acceptmenu`, `kcore.tpa.bypass-cooldown`, `kcore.tpa.bypass-disabled`.

### RTP Engine

```
/rtp
/rtp overworld
/rtp nether
/rtp the_end
/randomtp
/wild
```

`modules/rtp.yml` giới hạn concurrent search, queue và snapshot scan.

```yaml
engine:
  max-concurrent-searches: 3
  queue-limit: 100
  attempts-per-search: 48
  search-timeout-seconds: 18
  snapshot-scan-threads: 1
  generate-new-chunks: true
  prefer-generated-chunks: true
```

RTP chọn X/Z ngẫu nhiên, scan `ChunkSnapshot`, tìm điểm an toàn, warmup rồi kiểm tra live-world lần cuối. KCore chỉ charge sau warmup và validation cuối. Hủy trước đó không mất phí.

```yaml
warmup:
  seconds: 5
  cancel-on-move: true
  cancel-distance: 0.25
  horizontal-only: false
  cancel-on-damage: true
  cancel-on-world-change: true
cooldown:
  seconds: 300
  persist: true
cost:
  enabled: false
  provider: balance
  amount: 1000
```

Provider cost: `balance`, `shards`, `vault`, `kessentials`, `playerpoints`, `kshards` hoặc `solarshards`. `refund-on-cancel` và `refund-on-failed-teleport` mặc định bật.

LuckPerms profile và meta có thể override cooldown, warmup, provider và cost. Meta keys: `kcore-rtp-cooldown`, `kcore-rtp-warmup`, `kcore-rtp-cost`, `kcore-rtp-cost-provider`, `kcore-rtp-free`.

Safety mặc định chặn nước, lava, fire, powder snow, cobweb, cactus, berry bush, campfire và magma block. Arrival bảo vệ fall damage 8 giây.

Cần `kcore.rtp`. Các bypass: `kcore.rtp.bypass-cooldown`, `kcore.rtp.bypass-cost`. World node: `kcore.rtp.world.overworld`, `kcore.rtp.world.nether`, `kcore.rtp.world.the_end`.
