# Công cụ & cài đặt

## 1. Soạn ghi chú

| Lựa chọn | Ưu điểm | Gợi ý |
| --- | --- | --- |
| **VS Code** (đang dùng) | Sẵn có, gõ Markdown tốt, tích hợp git | Cài: *Markdown All in One*, *Markdown Preview Enhanced*, *Paste Image*, *Code Spell Checker*, *GitLens*, *Mermaid Preview* |
| **Obsidian** (mở thư mục này như một vault) | Backlink, graph, flashcards (plugin Spaced Repetition), canvas | Cài plugin: *Spaced Repetition*, *Dataview*, *Templater*, *Excalidraw* |

Dùng cả hai cùng lúc được — chúng đều đọc file `.md` thuần.

## 2. Mẹo VS Code

- Dán ảnh: cài *Paste Image* → đặt `pasteImage.path = ${currentFileDir}/anh`.
- Xem trước: `Ctrl+Shift+V`. Chia đôi màn hình: video bên phải, ghi chú bên trái.
- Snippet: tạo snippet `chuong` để chèn nhanh khung chương (hoặc copy từ chương mẫu).
- Tìm toàn kho: `Ctrl+Shift+F` — gõ `#tag` hay từ khoá để tìm lại ghi chú.

## 3. Git & backup

```bash
cd c:/security-foundations-notes
git init
git add .
git commit -m "khoi tao kho ghi chu"
```

- Tạo repo **private** trên GitHub để backup (chỉ đưa lên public những write-up/dự án đã rà soát).
- `.gitignore` đã chặn file nhạy cảm cơ bản (ảnh chụp có token, `.env`, file mã độc mẫu…). Kiểm tra trước khi push.
- Sao lưu thêm 1 bản (Google Drive / ổ ngoài) — mất kho = mất hàng trăm giờ học.

## 4. Ghi hình & ảnh chụp

- Chụp màn hình: `Win+Shift+S`. Che (blur) IP/domain/tên thật/cookie/token trước khi đưa vào write-up public.
- Ghi terminal: `asciinema` (Linux) hoặc ghi màn hình bằng OBS khi lab quan trọng.

## 5. Môi trường lab (xem chi tiết trong [home-lab/](../home-lab/README.md))

- Hypervisor: VirtualBox / VMware Workstation / Proxmox.
- VM tối thiểu GĐ 0–1: Ubuntu Server, Windows Server (AD), Windows client, pfSense/OPNsense, Kali.
- **Luôn snapshot** trước khi lab; mạng lab dùng *Host-only / Internal*, không bridge ra mạng nhà khi chạy mã độc hoặc tool tấn công.

## 6. Tài khoản nền tảng cần tạo

| Nền tảng | Dùng cho | Tạo ở GĐ |
| --- | --- | --- |
| TryHackMe | Lộ trình có hướng dẫn | 0–1 |
| OverTheWire | Bandit (Linux) | 0–1 |
| GitHub | Portfolio, script, detection-as-code | 0–1 |
| PortSwigger Academy | Web security | 4 |
| Hack The Box | Máy/AD/Academy | 4 |
| CyberDefenders / BTLO / LetsDefend | Blue team lab | 3 |
| CTFtime | Lịch CTF | 6 |

## 7. Bộ công cụ cài sẵn theo giai đoạn

- **GĐ 0–1:** Wireshark, nmap, netcat, curl, dig, Python 3, Git, Docker.
- **GĐ 2:** OpenSSL, CyberChef, OWASP Threat Dragon, hashcat (trên lab).
- **GĐ 3:** Wazuh/ELK, Sysmon, Atomic Red Team, Sigma (sigma-cli), Volatility 3, FTK Imager, REMnux/FLARE VM.
- **GĐ 4:** Burp Suite, ffuf, sqlmap, Nuclei, BloodHound, Impacket, NetExec, Metasploit.
- **GĐ 5:** Semgrep, Trivy, Gitleaks, Checkov, Terraform, kubectl, MISP/OpenCTI.
