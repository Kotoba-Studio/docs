---
description: Sell/Worth R02-v5 với GUI, SellTool, market và crash recovery.
icon: coins
---

# KWorth

## KWorth R02-v5

<a href="https://github.com/Kotoba-Studio/KWorth/releases/" class="button primary" data-icon="download">Tải bản phát hành</a>

KWorth là plugin Sell/Worth có Sell GUI, SellTool, giá động và recovery an toàn.

### Điểm nổi bật

* `/sell` GUI với nhiều style và tùy chọn xác nhận bán.
* SellTool theo container, inventory, bộ lọc và scanner.
* Giá `prices.yml`, progression cá nhân và market tùy chọn.
* Vault, VaultUnlocked, ExcellentEconomy, CoinsEngine và KShards.
* Journal fail-closed chống hoàn item khi trạng thái giao dịch chưa rõ.
* PlaceholderAPI, webhook và virtual price lore tùy chọn.

### Cài đặt nhanh

{% stepper %}
{% step %}
#### Cài plugin

Tắt máy chủ, rồi đặt `KWorth-R02-v5.jar` vào `plugins/`.
{% endstep %}

{% step %}
#### Khởi động máy chủ

Khởi động để KWorth tạo `plugins/KWorth/`.
{% endstep %}

{% step %}
#### Cấu hình

Chọn provider và cấu hình giá. Chạy `/kworth status` để xác nhận tích hợp.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Không xóa `data/transaction-journal.yml` khi chưa đối chiếu transaction và economy log.
{% endhint %}

### Khả năng tương thích

* Java phù hợp phiên bản server Minecraft 1.21.x.
* Paper hoặc Folia tương thích.
* PacketEvents chỉ cần khi bật virtual item price lore.

### Liên kết

* [Discord](https://dsc.gg/k-studio)
* [GitHub](https://github.com/Kotoba-Studio)
