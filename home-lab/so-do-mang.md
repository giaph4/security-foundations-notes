# Sơ đồ mạng home lab

> Vẽ bằng Mermaid (xem trực tiếp trong VS Code/Obsidian) hoặc draw.io rồi lưu ảnh vào `anh/`.

```mermaid
flowchart LR
    Internet((Internet)) --- FW[pfSense / OPNsense]
    FW --- LAN[LAN 10.10.10.0/24]
    FW --- DMZ[DMZ 10.10.20.0/24]
    LAN --- DC[Windows Server - DC]
    LAN --- WIN[Windows client]
    LAN --- SIEM[Wazuh / ELK]
    DMZ --- VULN[Máy vulnerable]
    KALI[Kali] --- LAN
```

| Mạng | Dải IP | Mục đích | Cách ly |
| --- | --- | --- | --- |
| LAN | 10.10.10.0/24 | Máy nội bộ giả lập | Internal |
| DMZ | 10.10.20.0/24 | Dịch vụ lộ ra ngoài | Internal |
| Attack | 10.10.30.0/24 | Kali / tool tấn công | Host-only |

> Sơ đồ trên chỉ là gợi ý — sửa lại theo lab thật của bạn.
