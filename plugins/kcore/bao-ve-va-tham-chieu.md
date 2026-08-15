---
description: KWL, KWB, AntiLagMachine, lệnh quản trị, quyền hạn và Folia notes.
icon: shield-halved
---

# Bảo vệ và tham chiếu

## Bảo vệ và tham chiếu

### KWL — Command Firewall

`modules/kwl.yml` tắt mặc định.

```yaml
enabled: false
whitelist:
  allow-namespaced-commands: false
protection:
  hide-command-tree: true
  filter-tab-complete: true
```

KWL whitelist root command cho player. Module có thể cấm namespaced command, ẩn command tree và lọc tab completion. Sensitive default gồm `pl`, `plugins`, `ver`, `version`, `about`, `help`, `?` và `paper`.

Dùng `/kwl status` hoặc `/kwl reload`. Cần `kwl.admin`. `kwl.bypass` bỏ qua firewall.

{% hint style="warning" %}
Thêm đủ command đang dùng vào whitelist trước khi bật KWL. Nếu không, player có thể bị chặn command hợp lệ.
{% endhint %}

### KWB — Crystal, Anchor và Minecart Guard

`modules/kwb.yml` tắt mặc định.

```yaml
enabled: false
block:
  end-crystal: true
  respawn-anchor: true
  all-crystal-spawns: true
  anchor-interaction: true
minecart:
  enabled: true
  max-per-chunk: 16
bypass:
  enabled: false
  permission: kwb.bypass
```

Dùng `/kwb status` và `/kwb reload`. `kwb.bypass` chỉ hoạt động khi bypass bật.

### AntiLagMachine

`modules/anti-lag-machine.yml` tắt mặc định. Scope hiện tại chỉ bao gồm boat/entity abuse và snow golem abuse.

```yaml
boat:
  max-per-chunk: 48
  local-radius: 3.0
  local-limit: 14
  window-ms: 3000
  max-created: 18
  trigger-local: 24
  trigger-chunk: 64
  max-remove-per-trigger: 8
  protect-occupied: true
  protect-named: true
```

Boat có người lái hoặc có tên có thể được bảo vệ khi cleanup.

```yaml
snow-golem:
  block-snowballs: true
  max-per-chunk: 48
  local-radius: 8.0
  local-limit: 24
snow-trail:
  enabled: true
  block-all: false
  max-forms-per-second-per-chunk: 80
notifications:
  enabled: true
  console: true
  admins: true
  cooldown-seconds: 10
```

Chỉ projectile Snow Golem bị chặn. Snowball của player không bị target. KCore theo dõi snowball, snow layer, snowmen và boat bị block hoặc cleanup.

Admin notification cần `kcore.antilag.notify`.

### Lệnh quản trị

```
/kcore status
/kcore reload
/kcore doctor
/kcore antilag
/kcore setspawn ...
/kcore setwarp ...
/kcore delwarp ...
/kcore menu <id>
```

`status` hiển thị trạng thái module và provider. `doctor` kiểm tra inventory, config, event, scheduler, currency hook, placeholder, menu, vault, RTP và settings.

KCore fail-safe disable khi startup linkage quan trọng lỗi.

Permission quản trị: `kcore.admin`, `kcore.admin.reload`, `kcore.admin.status`, `kcore.admin.setspawn`, `kcore.admin.warp` và `kcore.menu.admin`.

### Command và quyền người chơi

```
/spawn                 kcore.spawn
/home, /homes           kcore.home
/sethome                kcore.sethome
/delhome                kcore.delhome
/warp, /warps           kcore.warp
/settings, /setting     kcore.settings
/tpa                    kcore.tpa
/tpahere                kcore.tpahere
/tpaccept               kcore.tpaccept
/tpadeny                kcore.tpadeny
/tpacancel              kcore.tpacancel
/tpaauto                kcore.tpaauto
/confirmmenu            kcore.confirmmenu
/acceptmenu             kcore.acceptmenu
/baltop                 kcore.baltop
/shardstop              kcore.shardstop
/pv                     kcore.vault
/rtp                    kcore.rtp
/profile                kcore.profile
/kmenu                  kcore.menu
```

TPA alias: `/tphere`, `/tpyes`, `/tpdeny` và `/tpno`. RTP alias: `/randomtp`, `/wild`. Vault alias: `/vault`, `/playervault`. Profile alias: `/myprofile`.

Các bypass gồm `kcore.tpa.bypass-cooldown`, `kcore.tpa.bypass-disabled`, `kcore.rtp.bypass-cooldown`, `kcore.rtp.bypass-cost` và `kcore.teleport.bypass-warmup`.

Home limit dùng `kcore.homes.3`, `.5`, `.10`. Vault limit dùng `kcore.vaults.1`, `.3`, `.5`, `.10`, `.15`. RTP rank cooldown dùng `kcore.rtp.cooldown.kplus` đến `.kinfinity`.

### Folia và hiệu năng

KCore dùng scheduler bridge để đảm bảo entity và world access chạy đúng scheduler. Không gọi live Bukkit API từ worker thread.

Currency refresh, leaderboard fetch, Vault IO, Settings persistence và RTP snapshot scan chạy async. RTP giới hạn concurrent search. Menu có minimum refresh interval. AntiLagMachine dùng chunk và local counter.

### Production baseline

Bật homes, warps, settings, TPA, menus, placeholders, leaderboards, vaults, RTP và profile.

Bật `kwb` khi cần cấm crystal hoặc anchor. Bật AntiLagMachine khi có abuse thực tế. Bật KWL cuối cùng, sau khi hoàn thiện whitelist.

Hỗ trợ: [Kotoba Studio Discord](https://dsc.gg/k-studio).
