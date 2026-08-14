---
description: Shop style, economy, item và các tùy chọn giao dịch.
icon: gear
---

# Cấu hình

## Cấu hình KShop R03

### Config chính

```yaml
config-version: 15
style: one

lang: vi_VN

purchase:
  steps:
    decrease: [64, 10, 1]
    increase: [1, 10, 64]
  keep-menu-open: true
  quote-expire-seconds: 15
  queue-capacity: 16

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
    margin-percent: 5.0
    crafting:
      enabled: true
      floors: {}
```

### Giao diện và ngôn ngữ

Style shop: `one`, `king`, `ecosword`, `chillsmp`, `custom`, `modern`, `minimal`, `midnight`, `pastel`, `emerald`.

Đặt `lang: vi_VN` hoặc `lang: en_US`. Sau đó chạy `/kshop reload`.

R03 có fallback `vi_VN` và `en_US`.

Dùng token language trong title và lore:

```
{lang:ui.product.price}
{lang:ui.selector.confirm}
{lang:rank.title}
```

### Sản phẩm item

```yaml
items:
  stone:
    type: item
    page: 1
    slot: 9
    eco: vault
    price: 5
    amount: 1
    material: STONE
    name: ''
    lore: ['', '{lang:ui.product.price}']
```

`price` là giá của một bundle. `amount` là số item trong bundle.

`eco` được chọn trên từng item. Giá trị hỗ trợ: `vault`, `points`, `shards`, `free`.

`playerpoints` là alias của `points`. `kshards` là alias của `shards`.

PlayerPoints và KShards dùng số nguyên. Một shop có thể trộn nhiều currency.

Đặt `name: ''` để giữ tên item Minecraft theo ngôn ngữ client.

#### Category và product

Mỗi style có file root `styles/<style>/shops.yml` và category tại:

```
styles/<style>/shops/<category>.yml
```

```yaml
title: '&aFood'
size: 27
icon: GLOW_BERRIES
menu-slot: 11
items:
  bread:
    type: item
    eco: vault
    large-buy: true
    material: BREAD
    page: 1
    slot: 9
    price: 48
    amount: 1
    name: ''
    permission: ''
    market: false
```

`menu-slot: -1` không đặt vị trí cố định. Slot inventory bắt đầu từ `0`.

`permission: kshop.vip` giới hạn quyền mua product. `market: true` đưa product vào Dynamic Market.

#### Command product

```yaml
zombie_spawner:
  type: command
  eco: shards
  price: 15000
  amount: 1
  large-buy: false
  page: 1
  slot: 9
  display:
    material: SPAWNER
    name: '&aZombie Spawner'
  commands:
    - 'smartspawner give {player} zombie {amount}'
```

`display` chỉ là icon GUI. Command là phần thưởng thực tế.

Dùng `command:` cho một lệnh hoặc `commands:` cho nhiều lệnh. Placeholder gồm `{player}`, `{amount}` và `{product}`.

#### Quy tắc YAML

* Dùng spaces, không dùng tab.
* Material phải hợp lệ.
* Không trùng product ID trong một category.
* Sản phẩm trả phí cần giá dương.
* Slot phải thuộc inventory đã chọn.

### Command product

```yaml
items:
  zombie_spawner:
    type: command
    slot: 10
    eco: shards
    price: 15000
    display:
      material: SPAWNER
      name: 'Zombie Spawner'
    commands:
      - 'smartspawner give {player} zombie {amount}'
```

Các placeholder command gồm `{player}`, `{amount}` và `{product}`.

### Rank Shop

Bật Rank Shop và chọn style:

```yml
rank-shop:
  enabled: true
  style: flags
```

Style rank: `flags`, `iris`, `minimal`, `midnight`.

Chỉnh provider tại `plugins/KShop/ranks/settings.yml`:

```yml
provider: auto # auto | luckperms | powerranks | custom

custom:
  set-command: ''
  add-command: ''
```

`auto` ưu tiên provider tương thích. Rank item dùng `kshoprank set {player} <rank>` hoặc `kshoprank add {player} <rank>`.

Rank Shop mở bằng `/ranks` hoặc `/rankshop`. Quyền cần thiết là `kshop.ranks.open`.

Hãy kiểm tra currency, provider, rank upgrade và trường hợp thiếu tiền trước khi mở cho người chơi.

### Style, ngôn ngữ và âm thanh

Style shop có sẵn: `one`, `king`, `ecosword`, `chillsmp`, `custom`, `modern`, `minimal`, `midnight`, `pastel`, `emerald`.

Đổi style bằng `/kshop style modern`. Root layout dùng các key `root.title`, `root.size`, `root.categories` và `root.category-slots`.

Slot Bukkit bắt đầu từ `0`. Inventory 27 slot dùng `0` đến `26`.

Language có `vi_VN` và `en_US`. Giữ nguyên key và placeholder khi dịch.

`sounds.yml` hỗ trợ `open`, `open-category`, `select-product`, `amount-change`, `back`, `page`, `confirm`, `success`, `failure` và `insufficient-funds`.

### Giá, tax và market

`price.decimals` điều khiển định dạng giá. `price.guard` là lớp kiểm tra chống định giá thấp tùy chọn.

Tax tính trên subtotal. Market chỉ hoạt động khi `market-economy.enabled: true` và sản phẩm có `market: true`.

Với `tax.rate-percent: 5.0`, subtotal `200` có tax `10` và tổng `210`.

### Mẫu nhanh

```yaml
starter_food:
  type: item
  eco: free
  large-buy: false
  material: BREAD
  page: 1
  slot: 12
  price: 0
  amount: 16
  name: '&aStarter Bread'
```

Dùng `eco: free` cho product miễn phí. Không dùng `eco: vault` với `price: 0`.

Đặt `confirm.name` trống để chỉ phát kết quả cuối. Dùng sound ID vanilla như `minecraft:ui.button.click`.
