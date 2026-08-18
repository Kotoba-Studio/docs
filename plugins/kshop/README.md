---
description: 'Hướng dẫn KShop R05 CleanMenu: cài đặt, cấu hình và vận hành.'
icon: shop
---

# KShop R05

## KShop R05 — Releases / CleanMenu

<a href="https://github.com/Kotoba-Studio/KShop/releases/" class="button primary" data-icon="download">Tải bản phát hành</a>

> Shop GUI và Economy System cho Minecraft Server.\
> **Developer:** Kotoba Studio\
> **Minecraft:** 1.21+\
> **Paper / Folia / Canvas:** Tương thích qua scheduler bridge.

### Giới thiệu và cài đặt

KShop cho phép xây dựng hệ thống shop hoàn toàn bằng YAML.

* Tạo Shop hoặc Category không cần sửa code.
* Auto Pagination và slot riêng cho từng sản phẩm.
* Item product, command product, Vault, KShards, PlayerPoints và free product.
* Dynamic Market, tax, Price Guard, Rank Shop và Discord Market Webhook.
* GUI, language, sounds, One Setup và King Setup.

#### Cài đặt

Đưa file sau vào `plugins/`, rồi khởi động server:

```
KShop-R05-Releases-CleanMenu.jar
```

KShop tạo các file chính:

```
plugins/KShop/
├── config.yml       # Cấu hình hệ thống
├── lang.yml         # Ngôn ngữ
├── shops.yml        # Layout GUI
├── sounds.yml       # Âm thanh
├── webhooks.yml     # Discord Market Webhook
├── shops/           # Shop và sản phẩm
└── ranks/           # Rank Shop
```

Menu CleanMenu mặc định:

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

Để bật lại, đặt `enabled: true`, chọn `menu-slot`, rồi chạy `/kshop reload`.

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

Tên file `ores.yml` tạo Shop ID `ores`. Chạy `/kshop reload`, rồi mở bằng `/shop ores`.

#### Pages, slot và product

R05 nhóm sản phẩm trong `pages`. Không dùng `page: 1` bên trong item.

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

Với 9 product slots và 20 sản phẩm, KShop tạo 3 trang: `9`, `9`, `2`. Sản phẩm vượt slot không tự biến mất.

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

Ưu tiên `slot: 12`. KShop vẫn hỗ trợ `slots: 12` và `slots: [12]`. Không khai slot thì KShop chọn slot trống. Trùng slot thì product sau dùng slot trống kế tiếp.

`type: item` là mặc định. Command product:

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

Dùng `command: '...'` cho một lệnh hoặc `commands` cho nhiều lệnh. Placeholder: `{player}`, `{amount}`. Đặt `permission: 'kshop.vip'` để giới hạn. Đặt `enabled: false` để tắt product.

### GUI, One và King

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

GUI sizes hợp lệ: `9`, `18`, `27`, `36`, `45`, `54`. GUI `size: 27` không dùng được `slot: 40`.

`product-slots` là vị trí sản phẩm mỗi page, không phải tổng sản phẩm tối đa.

```yaml
layouts:
  gear: [2, 3, 4, 5, 6, 9, 10, 11, 12, 13, 14, 15, 16, 17]
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

Không dùng navigation slots làm product slots.

* **One:** Layout rộng. Gear có 14 item slots. Previous `18`, Back `22`, Next `26`.
* **King:** Layout compact. Product slots `9–17`. Back `18`, Previous `19`, Next `26`.

Giải nén `KShop-R05-Setup-One-CleanMenu.zip` hoặc `KShop-R05-Setup-King-CleanMenu.zip` vào `plugins/KShop/`.

> **Cảnh báo:** Setup có thể ghi đè `shops.yml` và `shops/`. Backup shop trước. Nếu chỉ đổi layout, chỉ thay `shops.yml`.

### Economy, purchase và market

```yaml
eco: vault      # Vault Economy
eco: shards     # Alias: kshards
eco: points     # Alias: playerpoints
eco: free       # Dùng cùng price: 0
```

`price: 500` là giá mỗi base purchase. Paid product nên có `price > 0`. `amount: 16` cho 16 item mỗi lần mua cơ bản. Đặt `large-buy: true` để đổi số lượng trong Selector.

```yaml
purchase:
  steps:
    decrease: [64, 10, 1]
    increase: [1, 10, 64]
success-message:
  enabled: false
insufficient-funds-details:
  enabled: false
tax:
  enabled: true
  rate-percent: 5.0
market-economy:
  enabled: true
  impact-per-item-percent: 0.15
  maximum-multiplier: 3.0
  recovery-half-life-minutes: 90
```

Giá `1000` với tax `5%` có tổng tiền `1050`. Mua nhiều làm demand và giá tăng. Giá giảm dần về base price theo thời gian.

Đặt `market: false` cho spawner, rank, command reward và product giá cố định.

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

```
/kshop price <category> <product> <price>
/kshop amount <category> <product> <amount>
/kshop eco <category> <product> <economy>
```

Với cấu trúc `pages → items` của R05, hãy sửa `shops/<category>.yml`, rồi chạy `/kshop reload`.

```yaml
rank-shop:
  enabled: true
  style: flags
```

Mở Rank Shop bằng `/ranks` hoặc `/rankshop`. Permission: `kshop.ranks.open`. Styles: `flags`, `iris`, `minimal`, `midnight`. Đây không phải One hoặc King.

```yaml
# ranks/settings.yml
provider: auto

# Custom provider
provider: custom
custom:
  set-command: 'perm user {player} group set {rank}'
  add-command: 'perm user {player} group add {rank}'
```

Provider hỗ trợ `auto`, `luckperms`, `powerranks`, `custom`. Custom provider dùng `{player}` và `{rank}`.

### Language, sound, webhook và xử lý lỗi

```yaml
# config.yml
lang: vi_VN
# Hoặc: en_US

# sounds.yml
enabled: true
success:
  name: 'minecraft:entity.player.levelup'
  volume: 0.85
  pitch: 1.15
```

Chỉnh giá trị hiển thị trong `plugins/KShop/lang.yml`, rồi chạy `/kshop reload`. Không sửa YAML key, command, permission, placeholder, Material ID hoặc namespace.

Sound events: `open`, `open-category`, `select-product`, `amount-change`, `back`, `page`, `confirm`, `success`, `failure`, `insufficient-funds`. Đặt `name: ''` để tắt từng sound, hoặc `enabled: false` để tắt toàn bộ.

```yaml
# webhooks.yml
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

**Item không xuất hiện:** Kiểm tra `enabled: true`, `pages → 1 → items`, Material hợp lệ, `price`, `eco` và `command` hoặc `commands`. Chạy `/kshop reload` và xem console.

**Item thứ 10+ không xuất hiện:** KShop tự phân trang. Nếu vẫn thiếu, kiểm tra `product-slots`, layout riêng, navigation slots, item slots và YAML indentation.

**Category không xuất hiện:** Kiểm tra `enabled: true` và `menu-slot`. Dùng `menu-slot: -1` để tự xếp.

**Plugin bị disabled:** `/shop` không chạy chỉ là hậu quả. Tìm lỗi startup trước đó, thường gần dòng `KShop dừng an toàn vì khởi tạo thất bại`.

**Economy không hoạt động:** Kiểm tra startup có `Economy hook:`, economy trong product và plugin economy tương ứng.

#### Update KShop

1. Stop server.
2. Backup `plugins/KShop/`.
3. Thay JAR.
4. Start server.
5. Kiểm tra startup log.
6. Test `/shop`.
7. Test purchase.

Chỉ giữ **một** JAR KShop. Không để cả `KShop-old.jar` và `KShop-new.jar`.

> **Slot quyết định vị trí, không quyết định số lượng sản phẩm.**
>
> **Thêm shop là thêm một file `.yml`, không cần sửa code.**
