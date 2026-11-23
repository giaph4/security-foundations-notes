# Home Lab

> Mục tiêu: dựng lại được toàn bộ lab trong ≤ 1 ngày (nhờ tài liệu + IaC/Ansible) và luôn có snapshot sạch.

| File | Nội dung |
| --- | --- |
| [so-do-mang.md](so-do-mang.md) | Sơ đồ mạng, dải IP, VLAN |
| [kiem-ke-vm.md](kiem-ke-vm.md) | Danh sách VM, cấu hình, tài khoản lab (**không** ghi mật khẩu thật) |
| [nhat-ky-dung-lab.md](nhat-ky-dung-lab.md) | Từng bước dựng, lỗi gặp, cách sửa |
| [snapshot-log.md](snapshot-log.md) | Snapshot đã tạo & mục đích |
| [ke-hoach-nang-cap.md](ke-hoach-nang-cap.md) | Giai đoạn nào thêm gì vào lab |

## Kiến trúc chuẩn (roadmap)

PC 32 GB RAM (hoặc cloud credit) + Proxmox/VMware → pfSense/OPNsense, AD domain (1 DC + 2 client), Kali, Wazuh/ELK, Security Onion, vài máy vulnerable.
