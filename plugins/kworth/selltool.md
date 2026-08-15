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
/selltool give EmaVietNam sell-stick 100
```

### Tool mặc định

* `sell-stick` — bán toàn bộ item hợp lệ trong container.
* `farming-wand`, `mining-wand`, `mob-drop-wand`, `fishing-wand` — bán theo category.
* `sell-bag` — bán inventory người chơi. `value-scanner` chỉ xem giá trị.
* `area-wand` tắt mặc định. Tool chỉ quét chunk đã load.

`selltool.yml` đặt action, material, uses, cooldown, permission, name, lore và whitelist category. Không phát tool bằng `/give` vanilla.

{% hint style="info" %}
Không đổi ID tool đã phát rộng rãi khi chưa có migration. Test quyền claim và WorldGuard trước production.
{% endhint %}
