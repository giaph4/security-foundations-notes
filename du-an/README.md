# Dự án Portfolio (Giai đoạn 5)

> Mỗi dự án: 1 thư mục, có `README.md` (dùng [mau/project-readme.md](../mau/project-readme.md)), sơ đồ, kết quả đo được, bài học. Đẩy lên GitHub public sau khi rà soát bí mật.

| # | Dự án | Thư mục | Trạng thái |
| --- | --- | --- | --- |
| 1 | CI/CD DevSecOps cho 1 đồ án Java, có security gate chặn build | [01-devsecops-pipeline/](01-devsecops-pipeline/README.md) | ⬜ |
| 2 | Kiến trúc cloud an toàn bằng Terraform + báo cáo CSPM trước/sau | [02-cloud-secure-terraform/](02-cloud-secure-terraform/README.md) | ⬜ |
| 3 | Home SOC hoàn chỉnh + dashboard + 20 detection rule có tài liệu | [03-home-soc/](03-home-soc/README.md) | ⬜ |
| 4 | Blog/GitHub: 10 bài write-up/nghiên cứu | [04-blog-writeups/](04-blog-writeups/README.md) | ⬜ |

## Ý tưởng bổ sung (đề xuất)

- Script Python quét port + parse log SSH (đã có ở GĐ 0–1) → nâng cấp thành công cụ có test + CI.
- Bộ **Sigma rules** có mapping ATT&CK và kết quả test Atomic Red Team.
- **Threat model** của đồ án phần mềm của bạn (Java/Android) — rất ăn điểm trong phỏng vấn AppSec.
- Báo cáo pentest mẫu (trên Juice Shop/DVWA) 15–25 trang.
