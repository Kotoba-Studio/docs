---
description: Client/mod detection dựa trên fingerprint cho máy chủ Minecraft.
icon: shield-halved
---

# KShield

## KShield R01-v3

<a href="https://github.com/Kotoba-Studio/KShield/releases" class="button primary" data-icon="download">Tải bản mới nhất</a>

KShield phát hiện client và mod qua fingerprint. Plugin phù hợp cho máy chủ đông người.

### Điểm nổi bật

* Phát hiện translation key, plugin channel và payload.
* PlaceholderAPI với namespace `%kshield_*%`.
* Probe plan dùng chung và packet hot path tối ưu.
* Hỗ trợ `vi_VN` và `en_US`.
* Validator cấu hình trước khi reload.

### Yêu cầu

* Paper, Folia, Canvas hoặc fork tương thích.
* PacketEvents là dependency bắt buộc.
* Java theo yêu cầu của phiên bản máy chủ.

### Lệnh chính

```
/kshield inspect <player>
/kshield rules
/kshield testmod <mod>
/kshield reload
```

{% hint style="warning" %}
Fingerprint đơn lẻ không phải bằng chứng tuyệt đối để auto-ban. Hãy kiểm tra evidence trước khi áp dụng punishment.
{% endhint %}

### Liên kết

* [Tải bản phát hành mới nhất](https://github.com/Kotoba-Studio/KShield/releases)
* [Discord](https://dsc.gg/k-studio)
* [GitHub](https://github.com/Kotoba-Studio)
