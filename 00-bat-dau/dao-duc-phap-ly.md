# Đạo đức & pháp lý — ĐỌC TRƯỚC KHI THỰC HÀNH

## Quy tắc bất di bất dịch

1. **Chỉ test trên hệ thống của chính mình** (home lab) hoặc nền tảng cho phép rõ ràng (THM, HTB, PortSwigger, OverTheWire, VulnHub, DVWA, Juice Shop, CTF đang mở).
2. **Không bao giờ** quét/tấn công website, mạng trường, mạng công ty, wifi hàng xóm… khi chưa có **ủy quyền bằng văn bản**.
3. **Bug bounty/VDP:** đọc kỹ *scope* và *policy*; chỉ test tài sản trong scope; dừng ngay khi chạm tới dữ liệu người khác.
4. **Mã độc mẫu:** chỉ chạy trong VM cách ly, không bridge mạng, snapshot trước, không mang ra ngoài.
5. **Dữ liệu thật** (của bạn bè, công ty, thực tập): không đưa vào ghi chú/write-up; ẩn danh hoá.
6. **Responsible disclosure:** nếu vô tình phát hiện lỗ hổng ở hệ thống thật → báo cho chủ hệ thống/CERT, đừng khai thác tiếp, đừng công khai.
7. Luật liên quan tại Việt Nam (kiểm tra bản hiện hành): Luật An ninh mạng, Luật An toàn thông tin mạng, Bộ luật Hình sự (các tội liên quan mạng) và quy định bảo vệ dữ liệu cá nhân.

## Checklist trước mỗi buổi lab tấn công

- [ ] Mục tiêu là máy lab / nền tảng hợp lệ của mình?
- [ ] Mạng lab đã cách ly (host-only/internal)?
- [ ] Đã snapshot?
- [ ] Mình biết lệnh sắp chạy làm gì (không copy-paste mù)?

## Khi viết write-up công khai

- Không đăng flag/đáp án của **giải CTF đang diễn ra** hoặc máy HTB *active* (vi phạm điều khoản).
- Ẩn token, cookie, IP thật, thông tin cá nhân.
- Nêu rõ: *công cụ dùng cho mục đích học tập, trong môi trường được phép.*

## Cam kết cá nhân (tự ký)

> Tôi, ____________________, cam kết dùng kiến thức bảo mật để bảo vệ, không để gây hại; tuân thủ pháp luật và các quy tắc trên.
> Ngày: ____/____/____
