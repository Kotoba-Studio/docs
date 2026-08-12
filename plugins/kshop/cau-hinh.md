---
description: Shop style, economy, item và các tùy chọn giao dịch.
icon: gear
---

# Cấu hình

## Cấu hình KShop

### Config chính

```yaml
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

price:
  guard:
    enabled: true
```

### Giao diện và ngôn ngữ

Style shop: `one`, `king`, `ecosword`, `chillsmp`, `custom`, `modern`, `minimal`, `midnight`, `pastel`, `emerald`.

Đặt `lang: vi_VN` hoặc `lang: en_US`. Sau đó chạy `/kshop reload`.

KShop tải language remote và cache file active tại `plugins/KShop/lang.yml`. JAR có fallback `vi_VN` và `en_US`.

Dùng token language trong title và lore:

```
{lang:ui.product.price}
{lang:ui.selector.confirm}
{lang:rank.title}
```

### Item thường

```yaml
items:
  stone:
    type: item
    page: 1
    slot: 9
    eco: vault
    price: 5
    amount: 1
    display:
      material: STONE
      name: '&fStone'
      lore: ['', '{lang:ui.product.price}']
```

`price` là giá của một bundle. `amount` là số item trong bundle.

`eco` được chọn trên từng item. Giá trị hỗ trợ: `vault`, `points`, `shards`, `free`.

`playerpoints` là alias của `points`. `kshards` là alias của `shards`.

PlayerPoints và KShards dùng số nguyên. Một shop có thể trộn nhiều currency.

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

### Âm thanh

`sounds.yml` điều khiển feedback âm thanh. R02-v6 dùng `minecraft:ui.button.click` cho các thao tác menu.

Để `confirm.name` trống. KShop chỉ phát success hoặc failure sau khi transaction hoàn tất.
