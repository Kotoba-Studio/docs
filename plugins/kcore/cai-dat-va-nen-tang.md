---
description: Cài KCore, chọn dependency và thiết lập cấu hình chung.
icon: download
---

# Cài đặt và nền tảng

## Cài đặt và nền tảng

### Cài lần đầu

{% stepper %}
{% step %}
#### Cài JAR

Tắt máy chủ. Đặt JAR KCore vào thư mục `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

KCore tạo các resource mặc định trong `plugins/KCore/`.
{% endstep %}

{% step %}
#### Chỉnh cấu hình

Cấu hình provider, module và style. Restart hoặc chạy `/kcore reload` khi phù hợp.
{% endstep %}
{% endstepper %}

### File được tạo

```
plugins/KCore/
├─ config.yml
├─ data.yml
├─ menus/
│  ├─ main.yml
│  └─ example-pro.yml
├─ modules/
│  ├─ policy.yml
│  ├─ rtp.yml
│  ├─ vault.yml
│  ├─ kwl.yml
│  ├─ kwb.yml
│  └─ anti-lag-machine.yml
└─ styles/
   ├─ donut.yml
   └─ other.yml
```

KCore migrate schema cũ và một số legacy module file.

{% hint style="warning" %}
Backup toàn bộ `plugins/KCore/` trước khi nâng cấp. Menu, style và module file đều là cấu hình runtime.
{% endhint %}

### Dependency và tích hợp

KCore khai báo soft-dependency với LuckPerms, Vault, VaultUnlocked, VaultUnlockedAPI, PlayerPoints, KShards, SolarShards, PlaceholderAPI và KTeams.

Khi `provider: auto`, balance ưu tiên `KEssentials → Vault/VaultUnlocked → PlayerPoints`. Shards ưu tiên `KShards → SolarShards → PlayerPoints → Vault`.

Nếu không có provider phù hợp, tính năng cần currency trả về `unavailable`.

### Cấu hình chung

`config.yml` điều khiển command override, font, style và module.

```yaml
commands:
  force-override: true
font:
  auto-convert: true
style: donut
```

`force-override` cho phép KCore sở hữu command EcoSMP dùng chung. `auto-convert` chỉ chuyển text hiển thị. Command, permission, placeholder và MiniMessage tag vẫn được giữ nguyên.

Style tích hợp gồm `donut` và `other`.

```yaml
modules:
  homes: true
  warps: true
  settings: true
  tpa: true
  menus: true
  placeholders: true
  leaderboards: true
  vaults: true
  rtp: true
  kwl: false
  kwb: false
  anti-lag-machine: false
  profile: true
```

### LuckPerms Policy Service

`modules/policy.yml` là utility layer dùng chung. Module chỉ bị ảnh hưởng khi nó đọc policy.

Profile có `priority` cao nhất sẽ thắng. Policy hỗ trợ LuckPerms group kế thừa. Snapshot LuckPerms được cache mặc định `2000ms`.

* **Home:** `max-homes` và `warmup-seconds`.
* **Warp và Spawn:** `warmup-seconds`.
* **TPA:** `send-cooldown-seconds` và `warmup-seconds`.

Rank chain mặc định là `kplus → kpro → kmaster → klegend → kgod → kinfinity`. Rank cao hơn có thể có warmup và cooldown thấp hơn.

### Reload và kiểm tra

Dùng `/kcore reload` cho thay đổi runtime thông thường. Restart hoàn toàn khi đổi JAR, dependency, command override hoặc module quan trọng.

`/kcore status` hiển thị module, provider, scheduler và storage. `/kcore doctor` kiểm tra runtime linkage quan trọng.
