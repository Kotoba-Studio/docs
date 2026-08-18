---
description: Cấu hình KShop R05 CleanMenu, products, economy, GUI và Rank Shop.
icon: gear
---

# Cấu hình

## Cấu hình KShop R05 — CleanMenu

> R05 không dùng `styles/one/` hoặc `styles/king/` cho Shop chính.\
> One và King là **Setup Pack ZIP** chứa `shops.yml` và `shops/`.

### Cấu trúc R05

```
plugins/KShop/
├── config.yml
├── shops.yml
├── shops/*.yml
├── lang.yml
├── sounds.yml
├── webhooks.yml
└── ranks/
    ├── settings.yml
    └── styles/
```

KShop R05 tự quét `shops/*.yml`. Tên `shops/ores.yml` tạo category ID `ores`.

### Config chính

```yaml
config-version: 19

lang: vi_VN

purchase:
  steps:
    decrease: [64, 10, 1]
    increase: [1, 10, 64]
  keep-menu-open: true
  quote-expire-seconds: 15
  queue-capacity: 16
  success-message:
    enabled: false
  insufficient-funds-details:
    enabled: false

rank-shop:
  enabled: false
  style: flags

tax:
  enabled: false
  rate-percent: 5.0

market-economy:
  enabled: false
  impact-per-item-percent: 0.15
  maximum-multiplier: 3.0
  recovery-half-life-minutes: 90
  save-delay-millis: 1000
  maximum-state-entries: 5000

price:
  decimals: 2
  guard:
    enabled: true
    fail-closed: true
    margin-percent: 5.0
    crafting:
      enabled: true
      floors: {}
```

`quote-expire-seconds` làm mới quote cũ. `queue-capacity` giảm double purchase. `fail-closed: true` phù hợp production.

### Layout `shops.yml`

```yaml
root:
  title: '&8ᴇᴄᴏɴᴏᴍʏ sᴛᴏʀᴇ'
  size: 27
  category-slots: [10, 11, 12, 13, 14, 15, 16]
category:
  title: '&8{category}'
  size: 27
  product-slots: [9, 10, 11, 12, 13, 14, 15, 16, 17]
  layouts:
    gear: [2, 3, 4, 5, 6, 9, 10, 11, 12, 13, 14, 15, 16, 17]
  navigation:
    previous: { slot: 18, material: ARROW }
    back: { slot: 22, material: RED_STAINED_GLASS_PANE }
    next: { slot: 26, material: ARROW }
selector:
  title: '&8ᴍᴜᴀ {product}'
  size: 27
  product-slot: 13
  amount-slots: [9, 10, 11, 15, 16, 17]
  back: { slot: 21 }
  confirm: { slot: 23 }
```

Inventory hợp lệ: `9`, `18`, `27`, `36`, `45`, `54`. Slot bắt đầu từ `0`. Navigation slots không dùng làm product slots.

### Category, pages và product

Tạo `plugins/KShop/shops/ores.yml`:

```yaml
enabled: true
title: '&bᴏʀᴇs'
size: 27
icon: DIAMOND_ORE
menu-slot: 17
pages:
  1:
    items:
      diamond:
        eco: vault
        slot: 12
        material: DIAMOND
        price: 500
        amount: 1
        large-buy: true
        market: true
        permission: ''
```

Không đặt `page:` trong product. KShop tự phân trang khi số item vượt `product-slots`. `slot` là vị trí ưu tiên. Không khai `slot` thì KShop tự xếp. `slots: 12` và `slots: [12]` vẫn tương thích.

`eco` hỗ trợ `vault`, `shards` (`kshards`), `points` (`playerpoints`) và `free`. Dùng `eco: free` cùng `price: 0`. Paid product cần `price > 0`.

```yaml
zombie_spawner:
  type: command
  eco: shards
  price: 15000
  amount: 1
  large-buy: false
  market: false
  display:
    material: SPAWNER
    name: '&dZombie Spawner'
  commands:
    - 'smartspawner give {player} zombie {amount}'
```

Command product dùng `command` hoặc `commands`. Placeholder: `{player}`, `{amount}`. Material phải hợp lệ và không dùng `AIR`.

### One, King, Rank Shop và integrations

One có layout Gear 14 slots. King có 9 slots mỗi page. Cài bằng `KShop-R05-Setup-One-CleanMenu.zip` hoặc `KShop-R05-Setup-King-CleanMenu.zip`.

> Setup ZIP là full setup. Backup `shops.yml` và `shops/` trước khi ghi đè. Restart là cách an toàn nhất.

```yaml
rank-shop:
  enabled: true
  style: flags
```

Rank styles: `flags`, `iris`, `minimal`, `midnight`. Đây không phải One/King.

```yaml
# ranks/settings.yml
provider: custom
custom:
  set-command: 'perm user {player} group set {rank}'
  add-command: 'perm user {player} group add {rank}'
```

Provider: `auto`, `luckperms`, `powerranks`, `custom`. Mở bằng `/ranks` hoặc `/rankshop`.

### Language, sound, webhook và vận hành

Đặt `lang: vi_VN` hoặc `lang: en_US`. Chỉ sửa value trong `lang.yml`. Không sửa YAML key, placeholder, command, permission hoặc Material ID.

`sounds.yml` hỗ trợ `open`, `open-category`, `select-product`, `amount-change`, `back`, `page`, `confirm`, `success`, `failure`, `insufficient-funds`. Đặt `name: ''` để tắt một sound.

```yaml
market:
  enabled: true
  url: 'YOUR_WEBHOOK'
  minimum-change-percent: 2.5
  cooldown-seconds: 300
  notify-increase: true
  notify-recovery: true
```

Webhook cần Dynamic Market đang bật. Reset Market bằng `/kshop market reset all` hoặc `/kshop market reset gear.golden_apple`.

Sau khi chỉnh YAML, chạy `/kshop reload` và kiểm tra console. Với thay One/King, restart server.

> **Slot quyết định vị trí, không quyết định số lượng sản phẩm.**
