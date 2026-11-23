# Script Python: quét port + parse log SSH

> **Giai đoạn:** GĐ 0–1 · Trạng thái: ⬜ chưa · 🟨 đang · ✅ xong

Gate: script quét port **và** script parse log SSH đăng nhập thất bại.

## Yêu cầu
- [ ] `portscan.py`: nhận host + dải port, timeout, in kết quả
- [ ] `ssh_fail_parser.py`: đọc `/var/log/auth.log`, đếm theo IP nguồn, in top N
- [ ] README + ví dụ chạy
- [ ] Đẩy lên GitHub

## Thiết kế
…

## Kết quả chạy
```text
```

## Cải tiến tiếp
- Thêm cảnh báo khi > N lần thất bại/phút, xuất JSON
