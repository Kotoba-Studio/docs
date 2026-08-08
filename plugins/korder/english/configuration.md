---
description: Language, interface, economy, webhook, and order settings.
icon: gear
---

# Configuration

## Configuration

<a href="../cau-hinh.md" class="button secondary">Tiếng Việt</a> <a href="configuration.md" class="button primary">English</a>

Main configuration file: `plugins/KOrder/config.yml`.

### Language

```yaml
language: vi_VN
```

Available locales: `vi_VN`, `en_US`, `es_ES`, `pt_BR`, and `de_DE`.

### Interface

```yaml
gui:
  style: modern
```

Available styles: `modern`, `king`, `custom`.

### Economy

```yaml
economy:
  bridge: auto
```

| Mode               | Description                                   |
| ------------------ | --------------------------------------------- |
| `auto`             | VaultUnlocked → Vault → PlayerPoints          |
| `vaultunlocked`    | VaultUnlocked v2 only                         |
| `vault`            | Any economy provider registered through Vault |
| `playerpoints`     | Direct PlayerPoints integration               |
| `coinsengine`      | CoinsEngine through its Vault provider        |
| `excellenteconomy` | ExcellentEconomy through its Vault provider   |

### Discord Webhook

```yaml
discord-webhook:
  enabled: false
  url: ''
  username: KOrder
  events:
    - order-created
    - order-increased
    - order-delivered
    - order-completed
    - order-cancelled
    - order-expired
    - transaction-warning
```

Test the webhook with `/korder admin webhook test`.

### Orders

```yaml
orders:
  default-limit: 3
  expiry-days: 7
  min-amount: 1
  max-amount: 2304
  allow-own-delivery: false
  exact-item-from-hand: true
```
