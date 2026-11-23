# Theo dõi tiến độ toàn lộ trình

> Cập nhật mỗi Chủ nhật. Tick `[x]` khi **đã có bằng chứng** (file/ảnh/commit) chứ không phải "cảm giác đã hiểu".

## Tổng quan

| Giai đoạn | Thời lượng | Bắt đầu | Kết thúc | Số chương xong | Gate |
| --- | --- | --- | --- | --- | --- |
| [0–1 Nền tảng IT](../gd0-1-nen-tang-it/README.md) | 3–4 tháng |  |  | 0/21 | ⬜ |
| [2 Security Foundations](../gd2-security-foundations/README.md) | 2–3 tháng |  |  | 0/18 | ⬜ |
| [3 Blue Team](../gd3-blue-team/README.md) | 4–5 tháng |  |  | 0/16 | ⬜ |
| [4 Red Team](../gd4-red-team/README.md) | 4–5 tháng |  |  | 0/15 | ⬜ |
| [5 Chuyên sâu](../gd5-chuyen-sau/README.md) | 4–6 tháng |  |  | 0/18 | ⬜ |
| [6 Liên tục](../gd6-thich-ung-lien-tuc/README.md) | Suốt đời |  |  | 0/15 | ⬜ |

## Gate từng giai đoạn

### [GĐ 0–1](../gd0-1-nen-tang-it/README.md)
- [ ] Tự dựng home lab: 1 Linux server, 1 Windows Server (AD domain), 1 Windows client, pfSense/OPNsense làm firewall
- [ ] Giải thích được mọi gói tin trong 1 PCAP ngắn
- [ ] Hoàn thành Bandit level 0–20
- [ ] Viết script Python quét port + parse log SSH đăng nhập thất bại

### [GĐ 2](../gd2-security-foundations/README.md)
- [ ] Viết risk register 15–20 rủi ro cho 1 đồ án của bản thân
- [ ] Threat model STRIDE có DFD cho cùng hệ thống đó
- [ ] Map được 10 control CIS vào các rủi ro đã xác định
- [ ] (Tuỳ chọn) Thi CompTIA Security+

### [GĐ 3](../gd3-blue-team/README.md)
- [ ] Triển khai Wazuh hoặc ELK + Sysmon trong home lab, thu log từ 3 máy
- [ ] Viết 10 Sigma rule, test bằng Atomic Red Team, ghi lại kết quả detect/miss
- [ ] Viết 3 IR playbook và 1 postmortem cho một sự cố giả lập
- [ ] Hoàn thành 10 challenge trên CyberDefenders/BTLO
- [ ] (Tuỳ chọn) Chứng chỉ BTL1, CySA+ hoặc TryHackMe SAL1

### [GĐ 4](../gd4-red-team/README.md)
- [ ] Hoàn thành toàn bộ lab Apprentice + Practitioner của PortSwigger cho 8 nhóm lỗ hổng chính
- [ ] Root 30+ máy HTB/THM (ít nhất 10 Windows/AD)
- [ ] Pentest trọn vẹn 1 đồ án của bản thân và viết báo cáo 15–25 trang
- [ ] (Tuỳ chọn) eJPT → PNPT/CPTS → OSCP

### [GĐ 5](../gd5-chuyen-sau/README.md)
- [ ] Dự án 1: CI/CD pipeline DevSecOps hoàn chỉnh cho 1 đồ án Java, có security gate chặn build
- [ ] Dự án 2: Kiến trúc cloud an toàn bằng Terraform + báo cáo CSPM trước/sau
- [ ] Dự án 3: Home SOC hoàn chỉnh với dashboard + 20 detection rule có tài liệu
- [ ] Blog/GitHub: 10 bài write-up hoặc nghiên cứu

### [GĐ 6](../gd6-thich-ung-lien-tuc/README.md)
- [ ] Có quy trình cập nhật hàng tuần chạy ổn định ≥ 8 tuần liên tục
- [ ] Đã xử lý ≥ 1 CVE/chiến dịch thật theo quy trình 6 bước + Flash Alert
- [ ] Hoàn thành checklist sẵn sàng ứng tuyển vị trí đầu tiên

## Mốc quan trọng

- [ ] Home lab chạy được (sau GĐ 0–1)
- [ ] Risk register + threat model đầu tiên (GĐ 2)
- [ ] 10 Sigma rule đầu tiên (GĐ 3)
- [ ] Báo cáo pentest đầu tiên (GĐ 4)
- [ ] Chọn chuyên ngành (đầu GĐ 5): ______________________
- [ ] Chứng chỉ entry đầu tiên: ______________________ (ngày thi: ____)
- [ ] Portfolio GitHub công khai
- [ ] Nộp đơn vị trí đầu tiên

## Biểu đồ giờ học

| Tháng | Tổng giờ lý thuyết | Tổng giờ lab | Số write-up | Ghi chú |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |
