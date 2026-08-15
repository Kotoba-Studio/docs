---
description: Phạm vi tích hợp Java được công bố cho KShop R04 HotFix.
icon: brackets-curly
---

# Java API

## Tích hợp Java

KShop R04 HotFix không công bố Java API ổn định.

Không dùng package, class hoặc dependency nội bộ như một API contract.

### Tích hợp an toàn

Khai báo KShop là dependency khi plugin của bạn cần plugin này hoạt động trước.

Tích hợp qua command hoặc cấu hình khi phù hợp. Kiểm tra release notes trước khi gọi API nội bộ.

{% hint style="warning" %}
Không bind vào config, transaction, market hoặc economy nội bộ. Các thành phần này không phải stable API.
{% endhint %}
