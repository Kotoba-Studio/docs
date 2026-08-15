---
description: Core utilities R01-v9 gồm spawn, home, warp, TPA, vault và RTP.
icon: cubes
---

# KCore

## KCore R01-v9

KCore cung cấp các tiện ích nền tảng cho máy chủ Minecraft. Plugin gồm spawn, home, warp, TPA, settings, menu, leaderboard, vault, RTP và profile.

### Điểm nổi bật

* TPA có menu xác nhận và menu nhận request trong `/settings`.
* `/spawn` dùng giao diện gọn. Menu không còn nút Barrier hủy.
* Custom menu hỗ trợ điều kiện, action và PlaceholderAPI.
* RTP, player vault, leaderboard và module bảo vệ tùy chọn.

### Cài đặt nhanh

{% stepper %}
{% step %}
#### Cài plugin

Tắt máy chủ. Đặt `KCore-R01-v9.jar` vào `plugins/`.
{% endstep %}

{% step %}
#### Khởi động một lần

Khởi động để tạo `plugins/KCore/`. Giữ duy nhất một JAR KCore.
{% endstep %}

{% step %}
#### Kiểm tra

Chạy `/kcore status`. Cấu hình provider balance và shards trước khi bật leaderboard.
{% endstep %}
{% endstepper %}

### Lệnh

* **Di chuyển:** `/spawn [now]`, `/home [name]`, `/homes`, `/sethome`, `/delhome`, `/warp`, `/warps`, `/rtp [world]`.
* **TPA:** `/tpa`, `/tpahere`, `/tpaccept`, `/tpadeny`, `/tpacancel`, `/tpaauto`, `/tpatoggle`, `/confirmmenu`, `/acceptmenu`.
* **Tiện ích:** `/settings`, `/baltop`, `/shardstop`, `/pv`, `/profile`, `/kmenu <id>`.

Quản trị viên dùng `/setspawn`, `/setwarp`, `/delwarp`, `/kcore reload`, `/kcore status`, `/kcore doctor`, `/kmenu`, `/kwl` và `/kwb`.

### Quyền chính

Cấp node theo tính năng: `kcore.spawn`, `kcore.home`, `kcore.sethome`, `kcore.delhome`, `kcore.warp`, `kcore.tpa`, `kcore.tpahere`, `kcore.settings`, `kcore.rtp`, `kcore.vault` và `kcore.profile`.

Dùng node quản trị riêng: `kcore.admin.setspawn`, `kcore.admin.warp`, `kcore.admin.reload`, `kcore.admin.status` và `kcore.menu.admin`. Giới hạn home dùng `kcore.homes.<n>`. Vault dùng `kcore.vaults.<n>`.

### TPA và Settings

`settings.defaults` trong `config.yml` đặt giá trị mặc định toàn server.

* `tpa-confirm-menu`: Hiện xác nhận trước khi gửi TPA.
* `tpa-accept-menu`: Hiện popup accept hoặc deny cho người nhận.

Thiết lập người chơi được lưu riêng. Chúng không thay đổi giá trị mặc định server.

### Cấu hình, menu và module

`config.yml` điều khiển `commands.force-override`, style, module, teleport, home, spawn, TPA và currency. `modules/rtp.yml` cùng `modules/vault.yml` chứa cấu hình riêng.

Menu nằm tại `menus/<id>.yml`. Chạy `/kmenu validate` trước khi mở cho người chơi. Không đưa input người chơi vào action `[console]`.

Module mặc định bật: homes, warps, settings, TPA, menus, placeholders, leaderboards, vaults, RTP và profile. `kwl`, `kwb` và anti-lag-machine tắt mặc định.

LuckPerms, Vault, KShards, PlayerPoints, PlaceholderAPI và KTeams là soft-dependency. KCore load trước Essentials khi `commands.force-override` bật.

Placeholder: `%kcore_version%`, `%kcore_build%`, `%kcore_balance%`, `%kcore_shards%`, `%kcore_homes%` và `%kcore_setting_<setting>%`. Ví dụ: `%kcore_setting_tpa_confirm_menu%`.

{% hint style="warning" %}
Dùng `/kcore reload` cho thay đổi thông thường. Restart đầy đủ khi đổi JAR, dependency, command override hoặc module quan trọng.
{% endhint %}

Hỗ trợ: [Kotoba Studio Discord](https://dsc.gg/k-studio).
