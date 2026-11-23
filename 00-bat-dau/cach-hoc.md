# Cách học hiệu quả (đọc 1 lần, áp dụng suốt lộ trình)

## 1. Nguyên tắc nền

| Nguyên tắc | Nghĩa là | Áp dụng |
| --- | --- | --- |
| **Active recall** | Tự lôi kiến thức ra khỏi đầu, không đọc lại thụ động | Mục "Tự kiểm tra" + flashcards trong mỗi chương |
| **Spaced repetition** | Ôn đúng lúc sắp quên | Lịch +1/+3/+7/+21/+60 ngày ở cuối mỗi chương |
| **Feynman** | Hiểu = giải thích được đơn giản | Mục 4 của mỗi chương |
| **Learn by doing** | Bảo mật là kỹ năng tay chân | Mỗi chương ≥ 1 lab; tỉ lệ lý thuyết : lab ≈ 40 : 60 |
| **Interleaving** | Xen kẽ chủ đề, đừng nhồi 1 thứ 8 tiếng | Theo [ke-hoach-tuan.md](ke-hoach-tuan.md) |
| **Output > input** | Viết ra mới là học | Write-up, blog, cheat sheet |

## 2. Quy trình xem video rồi chép (3 lượt)

1. **Lượt 1 — Lướt (1× tốc độ 1.5–2×, KHÔNG ghi):** nắm bức tranh lớn, ghi 3 câu hỏi "mình muốn biết gì".
2. **Lượt 2 — Học thật (tốc độ 1×):** dừng sau mỗi ý chính (khoảng 3–5 phút) → ghi vào bảng Cornell trong chương:
   - Cột *Mốc thời gian* (để quay lại)
   - Cột *Câu hỏi gợi nhớ* (viết dạng câu hỏi)
   - Cột *Ghi chú* (bằng lời mình, ngắn gọn, có ví dụ/lệnh)
3. **Lượt 3 — Làm theo:** vừa xem vừa gõ lệnh trong lab. Xem xong **đóng video**, viết "Tóm tắt 3 dòng" rồi mới đối chiếu.

> Quy tắc 20/10: không ghi quá 20% nội dung; nếu đang chép gần như nguyên văn nghĩa là chưa hiểu → dừng, tua lại.

## 3. Quy trình đọc sách / giáo trình (SQ3R)

**S**urvey (lướt tiêu đề, sơ đồ) → **Q**uestion (biến tiêu đề thành câu hỏi) → **R**ead (đọc tìm câu trả lời) → **R**ecite (khép sách, nói lại) → **R**eview (xem lại sau 1 ngày).

## 4. Quy trình làm lab

1. Đọc mục tiêu, **dự đoán** kết quả trước khi chạy ("mình nghĩ lệnh này in ra gì?").
2. **Snapshot VM** trước khi làm.
3. Làm từng bước, ghi lệnh + output quan trọng.
4. Chụp ảnh/ghi log bằng chứng.
5. Hỏi 3 câu: *Vì sao hoạt động? Kẻ tấn công lạm dụng thế nào? Log để lại dấu vết gì?*
6. Dọn dẹp / revert snapshot. Viết lab-report ngắn nếu lab lớn ([mau/lab-report.md](../mau/lab-report.md)).

## 5. Khi bị kẹt (quy tắc thang 4 bậc)

| Bậc | Hành động | Thời gian tối đa |
| --- | --- | --- |
| 1 | Tự nghĩ, đọc lại đề, `man`/docs chính thức | 20 phút |
| 2 | Google/forum, hint của nền tảng | 20 phút |
| 3 | Hỏi cộng đồng / AI (kèm bạn đã thử gì) | 10 phút |
| 4 | Xem walkthrough — **sau đó tự làm lại từ đầu không nhìn** và ghi "mình đã sai tư duy ở đâu" | — |

Ghi mọi lần kẹt vào mục "Lỗi gặp phải" — đó là vàng cho phỏng vấn.

## 6. Pomodoro gợi ý

25 phút tập trung + 5 phút nghỉ; sau 4 vòng nghỉ 20 phút. Buổi lab dài: 50 + 10.

## 7. Ôn tập định kỳ

| Tần suất | Việc | Thời lượng |
| --- | --- | --- |
| Hằng ngày | Ôn flashcards đến hạn | 10–15 phút |
| Cuối tuần | Điền [mau/weekly-review.md](../mau/weekly-review.md), viết write-up | 1–2 giờ |
| Cuối module | Tự kiểm tra tổng hợp, làm sơ đồ, giải thích cho người khác | 2 giờ |
| Cuối giai đoạn | Làm **gate**, rà lại toàn bộ chỗ yếu | 1 tuần |

## 8. Dấu hiệu học sai

- Xem video 10 giờ nhưng không có lab nào ("tutorial hell").
- Ghi chú dài hơn video.
- Không giải thích lại được sau 1 ngày.
- Chạy tool mà không biết nó làm gì ở tầng gói tin / hệ thống.
→ Giải pháp: giảm input, tăng lab và Feynman.
