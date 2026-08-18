---
description: Hướng dẫn cài đặt, cấu hình và vận hành KShop R05 CleanMenu.
---

# KShop R05

## KShop R05 — Releases / CleanMenu

> **KShop R05 — Releases / CleanMenu**\
> Shop GUI và Economy System cho Minecraft Server.\
> **Developer:** Kotoba Studio\
> **Minecraft:** 1.21+\
> **Paper / Folia / Canvas:** Tương thích qua scheduler bridge.

### Giới thiệu và cài đặt

#### KShop là gì?

KShop là plugin Shop GUI. Bạn xây dựng toàn bộ cửa hàng bằng YAML.

**Tính năng chính**

* Tạo shop và category không cần sửa code.
* Tự động phân trang và hỗ trợ slot riêng từng sản phẩm.
* Hỗ trợ item product, command product, Vault, KShards, PlayerPoints và free product.
* Dynamic Market, tax, Price Guard và Rank Shop.
* GUI, ngôn ngữ, âm thanh và Discord Market Webhook tùy chỉnh.
* One Setup và King Setup riêng.

#### Cài đặt

Đưa file sau vào thư mục `plugins/`, rồi khởi động server:

```
KShop-R05-Releases-CleanMenu.jar
```

KShop tạo cấu trúc sau:

```
plugins/KShop/
├── config.yml
├── lang.yml
├── shops.yml
├── sounds.yml
├── webhooks.yml
├── shops/
│   ├── blocks.yml
│   ├── farm.yml
│   ├── food.yml
│   ├── gear.yml
│   ├── shards.yml
│   ├── redstone.yml
│   ├── nether.yml
│   ├── end.yml
│   └── utility.yml
└── ranks/
    ├── settings.yml
    └── styles/
```

* `config.yml` — Cấu hình hệ thống.
* `shops.yml` — Layout GUI.
* `shops/*.yml` — Shop và sản phẩm.
* `lang.yml` — Ngôn ngữ.
* `sounds.yml` — Âm thanh.
* `webhooks.yml` — Discord Market Webhook.
* `ranks/` — Rank Shop.

#### Menu mặc định

CleanMenu đặt các category tại slot `10` đến `16`:

```
10 → Farm       11 → Food       12 → Gear
13 → Shards     14 → Redstone   15 → Nether
16 → End
```

`Blocks` và `Utility` bị tắt mặc định:

```yaml
enabled: false
menu-slot: -1
```

Để bật lại, đặt `enabled: true`, chọn `menu-slot`, rồi chạy:

```
/kshop reload
```

### Tạo shop, page và product

#### Tạo shop mới

Tạo `plugins/KShop/shops/ores.yml`:

```yaml
enabled: true
title: '&bᴏʀᴇs'
icon: DIAMOND_ORE
menu-slot: 17

pages:
  1:
    items:
      coal:
        eco: vault
        slot: 9
        material: COAL
        price: 20
        amount: 1

      iron:
        eco: vault
        slot: 10
        material: IRON_INGOT
        price: 50
        amount: 1
```

Tên file `ores.yml` là Shop ID `ores`. Reload, rồi mở shop bằng:

```
/kshop reload
/shop ores
```

#### Tạo page

Schema R05 nhóm sản phẩm trong `pages`. Không đặt `page: 1` trong từng item.

```yaml
pages:
  1:
    items:
      diamond:
        eco: vault
        material: DIAMOND
        price: 500
  2:
    items:
      emerald:
        eco: vault
        material: EMERALD
        price: 350
```

#### Auto Pagination

Nếu King có 9 product slots và shop có 20 sản phẩm, KShop tạo:

```
Page 1 → 9
Page 2 → 9
Page 3 → 2
```

Sản phẩm vượt quá số slot không tự biến mất.

#### Product cơ bản

```yaml
diamond:
  enabled: true
  eco: vault
  slot: 12
  material: DIAMOND
  price: 500
  amount: 1
  name: '&bᴅɪᴀᴍᴏɴᴅ'
  lore:
    - '&7ɢɪá: &f500'
  large-buy: true
  market: true
  permission: ''
```

#### Slot riêng từng item

Khuyến nghị dùng `slot`. KShop vẫn tương thích với `slots`.

```yaml
slot: 12
```

```yaml
slots: 12
# Hoặc
slots: [12]
```

Không khai báo slot thì KShop chọn slot trống từ layout hiện tại. Hai item trùng slot sẽ được xếp vào product slot trống kế tiếp.

#### Item và command product

`type: item` là mặc định và có thể bỏ:

```yaml
diamond:
  type: item
  eco: vault
  material: DIAMOND
  price: 500
  amount: 1
```

Command product dùng một hoặc nhiều lệnh:

```yaml
zombie_spawner:
  type: command
  eco: shards
  slot: 10
  price: 15000
  amount: 1
  large-buy: false
  market: false
  display:
    material: SPAWNER
    name: '&dᴢᴏᴍʙɪᴇ sᴘᴀᴡɴᴇʀ'
  commands:
    - 'smartspawner give {player} zombie {amount}'
```

Hỗ trợ placeholder `{player}` và `{amount}`. Dùng `command: '...'` cho một lệnh, hoặc `commands` cho nhiều lệnh.

Đặt `permission: 'kshop.vip'` để giới hạn product. Dùng `permission: ''` để không giới hạn. Đặt `enabled: false` để tắt sản phẩm.

### GUI, slot, One và King

#### Layout `shops.yml`

```yaml
root:
  title: '&8ᴇᴄᴏɴᴏᴍʏ sᴛᴏʀᴇ'
  size: 27
  category-slots: [10, 11, 12, 13, 14, 15, 16]

category:
  title: '&8{category}'
  size: 27
  product-slots: [9, 10, 11, 12, 13, 14, 15, 16, 17]
```

Inventory size hợp lệ: `9`, `18`, `27`, `36`, `45`, `54`. GUI có `size: 27` không thể dùng `slot: 40`.

`product-slots` là số vị trí sản phẩm **trên mỗi page**. Đây không phải tổng số sản phẩm tối đa của shop.

#### Layout riêng, navigation và selector

Đặt layout riêng cho category trong `layouts`:

```yaml
layouts:
  gear: [2, 3, 4, 5, 6, 9, 10, 11, 12, 13, 14, 15, 16, 17]
```

Gear có 14 slots mỗi page. Các category khác vẫn dùng layout mặc định.

```yaml
navigation:
  previous:
    slot: 18
    material: ARROW
  back:
    slot: 22
    material: RED_STAINED_GLASS_PANE
  next:
    slot: 26
    material: ARROW

selector:
  title: '&8ᴍᴜᴀ {product}'
  size: 27
  product-slot: 13
  amount-slots: [9, 10, 11, 15, 16, 17]
  back:
    slot: 21
  confirm:
    slot: 23
```

Navigation slots được dành riêng. Không dùng chúng làm product slots.

#### One và King Setup

* **One** ưu tiên layout rộng. Gear có 14 item slots. Navigation: Previous `18`, Back `22`, Next `26`.
* **King** dùng layout compact. Product slots `9–17`. Navigation: Back `18`, Previous `19`, Next `26`.

Giải nén `KShop-R05-Setup-One-CleanMenu.zip` hoặc `KShop-R05-Setup-King-CleanMenu.zip` vào `plugins/KShop/`.

> **Cảnh báo:** Setup có thể ghi đè `shops.yml` và `shops/`. Hãy backup shop trước. Nếu chỉ đổi layout, chỉ thay `shops.yml`.

### Economy, purchase và market

#### Economy và số lượng

```yaml
eco: vault      # Vault Economy
eco: shards     # Alias: kshards
eco: points     # Alias: playerpoints
eco: free       # Dùng cùng price: 0
```

`price: 500` đặt giá mỗi base purchase. Paid product nên có `price > 0`. `amount: 16` cho người chơi 16 item mỗi lần mua cơ bản.

Đặt `large-buy: true` để người chơi đổi số lượng trong Selector. Dùng `false` để tắt.

```yaml
purchase:
  steps:
    decrease: [64, 10, 1]
    increase: [1, 10, 64]

success-message:
  enabled: false

insufficient-funds-details:
  enabled: false
```

#### Tax, Dynamic Market và Price Guard

```yaml
tax:
  enabled: true
  rate-percent: 5.0

market-economy:
  enabled: true
  impact-per-item-percent: 0.15
  maximum-multiplier: 3.0
  recovery-half-life-minutes: 90
```

Với giá `1000` và tax `5%`, tổng tiền là `1050`. Mua nhiều làm demand và giá tăng. Giá giảm dần về base price theo thời gian.

Đặt `market: false` cho spawner, rank, command reward và các giá cố định.

```
/kshop market reset
/kshop market reset all
/kshop market reset gear.golden_apple
```

```yaml
price:
  guard:
    enabled: true
    fail-closed: true
    margin-percent: 5.0
    crafting:
      enabled: true
      floors:
        REDSTONE_BLOCK: 20.0
        POTATO: 5.0
```

Price Guard hạn chế cấu hình giá có thể tạo economy exploit.

### Commands, permissions và Rank Shop

#### Commands

```
/shop
/shop gear
/shop farm
/shop shards

/kshop
/kshop status
/kshop reload
/kshop open <category>
```

Permission:

```
kshop.open
kshop.ranks.open
kshop.admin
kshop.admin.status
kshop.admin.reload
kshop.admin.style
kshop.admin.open
kshop.admin.edit
kshop.admin.market
```

`kshop.admin` mặc định dành cho OP.

Các editor command có sẵn:

```
/kshop price <category> <product> <price>
/kshop amount <category> <product> <amount>
/kshop eco <category> <product> <economy>
```

Với cấu trúc `pages → items` của R05, cách quản trị đáng tin cậy nhất vẫn là sửa `shops/<category>.yml`, rồi chạy `/kshop reload`.

#### Rank Shop

```yaml
rank-shop:
  enabled: true
  style: flags
```

Mở Rank Shop bằng `/ranks` hoặc `/rankshop`. Permission là `kshop.ranks.open`.

Styles: `flags`, `iris`, `minimal`, `midnight`. Đây không phải One hoặc King. One/King dùng cho Shop chính.

Trong `ranks/settings.yml`:

```yaml
provider: auto
```

Provider hỗ trợ: `auto`, `luckperms`, `powerranks`, `custom`.

```yaml
provider: custom
custom:
  set-command: 'perm user {player} group set {rank}'
  add-command: 'perm user {player} group add {rank}'
```

Custom provider hỗ trợ `{player}` và `{rank}`.

### Language, sound, webhook và khắc phục lỗi

#### Language và sounds

```yaml
# config.yml
lang: vi_VN
# Hoặc: en_US
```

Runtime language file là `plugins/KShop/lang.yml`. Sau khi đổi ngôn ngữ, chạy `/kshop reload`.

Bạn có thể thay đổi giá trị hiển thị trong `lang.yml`. Không sửa YAML key, command, permission, placeholder, Material ID hoặc namespace.

```yaml
# sounds.yml
enabled: true

success:
  name: 'minecraft:entity.player.levelup'
  volume: 0.85
  pitch: 1.15
```

Events gồm `open`, `open-category`, `select-product`, `amount-change`, `back`, `page`, `confirm`, `success`, `failure` và `insufficient-funds`.

Đặt `name: ''` để tắt một sound. Đặt `enabled: false` để tắt toàn bộ.

#### Discord Market Webhook

```yaml
market:
  enabled: true
  url: 'YOUR_WEBHOOK'
  minimum-change-percent: 2.5
  cooldown-seconds: 300
  notify-increase: true
  notify-recovery: true
```

Bật webhook cùng `market-economy.enabled: true`.

#### Khắc phục lỗi

**Item không xuất hiện**

1. Kiểm tra `enabled: true` và cấu trúc `pages → 1 → items`.
2. Kiểm tra Material hợp lệ, ví dụ `material: DIAMOND`. Không dùng `AIR`.
3. Kiểm tra `price` và `eco`. Command product cần `command` hoặc `commands`.
4. Chạy `/kshop reload` và xem console.

**Item thứ 10+ không xuất hiện**

KShop tự phân trang. Với King, 14 items tạo 9 items ở Page 1 và 5 items ở Page 2. Nếu vẫn thiếu, kiểm tra `product-slots`, layout riêng category, navigation slot, item slot và YAML indentation.

**Category không xuất hiện**

Kiểm tra `enabled: true` và `menu-slot`. Dùng `menu-slot: -1` để tự xếp.

**Plugin bị disabled**

Lỗi `/shop` không chạy chỉ là hậu quả. Tìm lỗi startup trước đó, thường gần dòng:

```
KShop dừng an toàn vì khởi tạo thất bại
```

**Economy không hoạt động**

Kiểm tra startup có `Economy hook:`. Sau đó kiểm tra `eco: vault`, `eco: shards` hoặc `eco: points`, cùng plugin economy tương ứng.

#### Update KShop

1. Stop server.
2. Backup `plugins/KShop/`.
3. Thay JAR.
4. Start server.
5. Kiểm tra startup log.
6. Test `/shop`.
7. Test purchase.

Chỉ giữ **một** JAR KShop. Không giữ cả `KShop-old.jar` và `KShop-new.jar`.

> **Slot quyết định vị trí, không quyết định số lượng sản phẩm.**
>
> **Thêm shop là thêm một file `.yml`, không cần sửa code.**

Ví dụ: tạo `shops/potions.yml`, chạy `/kshop reload`, rồi shop mới hoạt động.
