---
description: Cấp và tùy chỉnh công cụ bán nhanh.
icon: wand-magic-sparkles
---

# SellTool

## SellTool

SellTool giúp người chơi bán vật phẩm nhanh.

### Cấp SellTool

```
/selltool give <player> <tool> [uses]
```

Ví dụ:

```
/selltool give EmaVietNam axe 100
```

### Tool mặc định

* `stick` — Sell Stick.
* `axe` — Netherite Axe có enchant.
* `wand` — Sell Wand.

Bạn có thể chỉnh material, tên, lore, enchant và số lượt dùng trong `selltool.yml`.

{% hint style="info" %}
SellTool dùng signature, nonce và generation để hạn chế sao chép hoặc dupe tool.
{% endhint %}
