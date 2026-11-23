# Giai đoạn 0–1: Nền tảng IT

> **Thời lượng:** 3–4 tháng · **Trọng tâm:** Networking, Linux/Windows, Python/Bash
> **Trạng thái giai đoạn:** ⬜ Chưa bắt đầu · 🟨 Đang học · ✅ Đạt gate

📖 Giáo trình chi tiết: [Giáo trình Giai đoạn 0–1 Nền tảng IT cho An ninh mạng](../giao-trinh/Gi%C3%A1o%20tr%C3%ACnh%20Giai%20%C4%91o%E1%BA%A1n%200%E2%80%931%20N%E1%BB%81n%20t%E1%BA%A3ng%20IT%20cho%20An%20ninh%20m%E1%BA%A1ng.md)
🗺 Roadmap tổng: [Roadmap An ninh mạng & An toàn thông tin](../roadmap/Roadmap%20An%20ninh%20m%E1%BA%A1ng%20%26%20An%20to%C3%A0n%20th%C3%B4ng%20tin.md)

> Không thể bảo vệ thứ mình không hiểu: 70% công việc bảo mật là hiểu sâu mạng và hệ điều hành.


## Bản đồ module & chương

| Module | Chương | Thời gian | Trạng thái |
| --- | --- | --- | --- |
| **[1. Networking](m1-networking/README.md)** | 5 chương | Tuần 1–5 | ⬜ |
| | [1.1 Mô hình OSI và TCP/IP](m1-networking/1.1-mo-hinh-osi-va-tcp-ip.md) | Tuần 1 | ⬜ |
| | [1.2 IP Addressing & Subnetting](m1-networking/1.2-ip-addressing-subnetting.md) | Tuần 1–2 | ⬜ |
| | [1.3 Giao thức cốt lõi](m1-networking/1.3-giao-thuc-cot-loi.md) | Tuần 2–3 | ⬜ |
| | [1.4 Thiết bị, Routing & Kiến trúc mạng](m1-networking/1.4-thiet-bi-routing-kien-truc-mang.md) | Tuần 3–4 | ⬜ |
| | [1.5 Phân tích traffic với Wireshark & công cụ mạng](m1-networking/1.5-phan-tich-traffic-voi-wireshark-cong-cu-mang.md) | Tuần 4–5 | ⬜ |
| **[2. Linux](m2-linux/README.md)** | 4 chương | Tuần 6–8 | ⬜ |
| | [2.1 Shell & Filesystem](m2-linux/2.1-shell-filesystem.md) | Tuần 6 | ⬜ |
| | [2.2 User, Group & Permission](m2-linux/2.2-user-group-permission.md) | Tuần 6–7 | ⬜ |
| | [2.3 Process, Service & Package](m2-linux/2.3-process-service-package.md) | Tuần 7 | ⬜ |
| | [2.4 Networking, Log & Firewall trên Linux](m2-linux/2.4-networking-log-firewall-tren-linux.md) | Tuần 8 | ⬜ |
| **[3. Windows & Active Directory](m3-windows-active-directory/README.md)** | 4 chương | Tuần 9–11 | ⬜ |
| | [3.1 Kiến trúc Windows](m3-windows-active-directory/3.1-kien-truc-windows.md) | Tuần 9 | ⬜ |
| | [3.2 PowerShell](m3-windows-active-directory/3.2-powershell.md) | Tuần 9–10 | ⬜ |
| | [3.3 Windows Event Log & Sysmon](m3-windows-active-directory/3.3-windows-event-log-sysmon.md) | Tuần 10 | ⬜ |
| | [3.4 Active Directory](m3-windows-active-directory/3.4-active-directory.md) | Tuần 10–11 | ⬜ |
| **[4. Ảo hóa, Docker & Home Lab](m4-ao-hoa-docker-home-lab/README.md)** | 4 chương | Bắt đầu tuần 1, hoàn thiện tuần 12 | ⬜ |
| | [4.1 Kiến thức ảo hóa](m4-ao-hoa-docker-home-lab/4.1-kien-thuc-ao-hoa.md) | Tuần 1+ | ⬜ |
| | [4.2 Docker cơ bản](m4-ao-hoa-docker-home-lab/4.2-docker-co-ban.md) | Tuần 1+ | ⬜ |
| | [4.3 Kiến trúc home lab chuẩn](m4-ao-hoa-docker-home-lab/4.3-kien-truc-home-lab-chuan.md) | Tuần 12 | ⬜ |
| | [4.4 Các bước dựng lab](m4-ao-hoa-docker-home-lab/4.4-cac-buoc-dung-lab.md) | Tuần 12 | ⬜ |
| **[5. Lập trình & Scripting](m5-lap-trinh-scripting/README.md)** | 4 chương | Tuần 13–15 | ⬜ |
| | [5.1 Python cho bảo mật](m5-lap-trinh-scripting/5.1-python-cho-bao-mat.md) | Tuần 13–14 | ⬜ |
| | [5.2 Bash scripting](m5-lap-trinh-scripting/5.2-bash-scripting.md) | Tuần 14 | ⬜ |
| | [5.3 PowerShell scripting](m5-lap-trinh-scripting/5.3-powershell-scripting.md) | Tuần 14–15 | ⬜ |
| | [5.4 Công cụ hỗ trợ](m5-lap-trinh-scripting/5.4-cong-cu-ho-tro.md) | Tuần 15 | ⬜ |

## Gate — tiêu chí để đi tiếp

> Chỉ chuyển giai đoạn khi **tất cả** ô được tick **và** có bằng chứng (link tới file/commit/ảnh).

- [ ] Tự dựng home lab: 1 Linux server, 1 Windows Server (AD domain), 1 Windows client, pfSense/OPNsense làm firewall
- [ ] Giải thích được mọi gói tin trong 1 PCAP ngắn
- [ ] Hoàn thành Bandit level 0–20
- [ ] Viết script Python quét port + parse log SSH đăng nhập thất bại

## Sản phẩm của giai đoạn (deliverables)

- [Tiến độ OverTheWire Bandit](san-pham/bandit-tien-do.md)
- [Phân tích PCAP](san-pham/phan-tich-pcap.md)
- [Script Python: quét port + parse log SSH](san-pham/script-portscan-ssh-log.md)
- [Hồ sơ home lab (gate)](san-pham/ho-so-home-lab.md)

## Nguồn học gợi ý

- Professor Messer (Network+), Cisco Networking Academy, *Computer Networking: A Top-Down Approach*
- OverTheWire **Bandit**, TryHackMe *Pre Security* / *Cyber Security 101*
- *Automate the Boring Stuff with Python*, *Black Hat Python*

## Nhật ký giai đoạn

| Tuần | Làm được gì | Vướng ở đâu | Việc tuần sau |
| --- | --- | --- | --- |
|  |  |  |  |

## Tổng kết cuối giai đoạn (viết khi đạt gate)

- Điều mình hiểu sâu nhất: …
- Điều còn yếu cần quay lại: …
- Ngày đạt gate: ____/____/____
