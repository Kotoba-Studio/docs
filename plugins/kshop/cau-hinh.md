---
description: Shop style, economy, item và các tùy chọn giao dịch.
icon: gear
---

# Cấu hình

## Cấu hình KShop

### Config chính

```yaml
style: one

rank-shop:
  enabled: false
  style: flags
  currency: points

tax:
  enabled: false

market-economy:
  enabled: false

price:
  guard:
    enabled: true
```

### Cấu trúc shop

```
plugins/KShop/
├── config.yml
├── sounds.yml
├── webhooks.yml
├── styles/<style>/shops.yml
├── styles/<style>/shops/*.yml
└── rank-shop/styles/<style>/
```

### Item thường

```yaml
items:
  stone:
    material: STONE
    page: 1
    slot: 9
    eco: vault
    price: 5
    amount: 1
    large-buy: true
```

`price` là giá mua của KShop. Bảng Prices của KWorth là giá bán. Không dùng trực tiếp giá đó làm giá mua.

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

Các giá trị `eco` hỗ trợ: `vault`, `shards`, `points`, `free`.
