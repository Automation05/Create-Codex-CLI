# Create-Codex-CLI

#Cài và dùng Codex trên Windows bằng WSL + Ubuntu

## 1. Mục tiêu

README này dùng để ghi nhớ lại toàn bộ cách:

1. Cài **Codex CLI** lần đầu trên **máy Windows mới** bằng **WSL + Ubuntu**.
2. Mở lại và dùng **mỗi ngày** mà không phải mò lại từ đầu.
3. Hiểu ngắn gọn **vì sao cần Ubuntu/WSL**, và khi nào có thể dùng trực tiếp mà không cần Ubuntu.

> **23/04/2026**

---

## 2. Giải thích ngắn gọn trước khi bắt đầu

### 2.1 Tại sao phải cài Node.js và npm?

Vì Codex CLI được cài bằng npm:

```bash
npm i -g @openai/codex
```

Nên nếu chưa có `node` và `npm` thì chưa cài được Codex CLI.

---

# PHẦN A — CÀI LẦN ĐẦU CHO MÁY MỚI

## 3. Tổng quy trình cài lần đầu

1. Cài **WSL + Ubuntu**
2. Restart máy
3. Mở Ubuntu lần đầu và tạo tài khoản Linux
4. Cập nhật Ubuntu
5. Cài **nodejs** và **npm**
6. Nếu npm lỗi quyền thì sửa quyền
7. Cài **Codex CLI**
8. Đăng nhập bằng tài khoản ChatGPT
9. Tạo thư mục project/test
10. Mở Codex trong thư mục đó

---

## 4. Bước 1 — Cài WSL + Ubuntu

### 4.1 Mở PowerShell Admin
### 4.2 Chạy lệnh cài WSL

```powershell
wsl --install
```

### 4.3 Nếu máy báo đã cài xong Ubuntu / WSL
Các dòng kiểu:

* `Virtual Machine Platform has been installed`
* `Windows Subsystem for Linux has been installed`
* `Ubuntu has been installed`
* `Changes will not be effective until the system is rebooted`

thì bước cài cơ bản đã xong.

---

## 5. Bước 2 — Restart máy

Sau khi chạy `wsl --install`, **phải restart máy**.

---

## 6. Bước 3 — Mở Ubuntu lần đầu

Sau khi máy bật lại:

* Ubuntu có thể tự mở ra
* hoặc mở từ **Start > Ubuntu**

### 6.1 Sau khi mở

Ubuntu sẽ:

* tải / giải nén lần đầu
* hỏi bạn tạo tài khoản Linux

```text
Create a default Unix user account:
```
Nhập username:

```text
clement
```

Sau đó nó hỏi mật khẩu:

* gõ password muốn đặt
* lưu ý: lúc gõ password thường **không hiện ký tự**
* cứ gõ rồi Enter
* nhập lại lần nữa để xác nhận

### 6.2 Dấu hiệu thành công

Nếu thấy dạng prompt như:

```bash
clement@DESKTOP-XXXX:~$
```

thì Ubuntu trong WSL đã hoạt động.

---

## 7. Bước 4 — Cập nhật Ubuntu

Ngay sau khi vào được Ubuntu, chạy lần lượt:

```bash
sudo apt update
sudo apt upgrade -y
```
---

## 8. Bước 5 — Cài Node.js và npm

Trong Ubuntu, chạy:

```bash
sudo apt install -y nodejs npm
```

### Kiểm tra đã cài xong chưa

Chạy:

```bash
node -v
npm -v
```

Nếu hiện ra số phiên bản, ví dụ kiểu:

* `v18.x.x`
* `9.x.x`

thì là ổn.

---

## 9. Bước 6 — Nếu npm bị lỗi quyền EACCES

Nếu chạy:

```bash
npm i -g @openai/codex
```

mà báo lỗi kiểu:

* `EACCES`
* `permission denied`
* không ghi được vào `/usr/local/lib/node_modules`

thì sửa như sau:

```bash
mkdir -p ~/.local
npm config set prefix ~/.local
echo 'PATH=~/.local/bin:$PATH' >> ~/.profile
source ~/.profile
```

### Giải thích ngắn

* Ta chuyển chỗ cài global package npm sang thư mục của user
* Như vậy không cần ghi vào thư mục hệ thống
* Sau đó npm sẽ cài được mà không cần quyền root

### Kiểm tra lại

```bash
npm config get prefix
echo $PATH
```

Nếu prefix gần giống `/home/clement/.local` là đúng hướng.

---

## 10. Bước 7 — Cài Codex CLI

Chạy:

```bash
npm i -g @openai/codex
```

### Kiểm tra đã cài xong chưa

Chạy:

```bash
codex --version
```

Nếu hiện ra phiên bản, ví dụ kiểu `0.xxx.x`, là đã cài thành công.

---

## 11. Bước 8 — Chạy Codex lần đầu

Chạy:

```bash
codex
```

### Lần đầu nó sẽ hỏi đăng nhập

Codex sẽ cho bạn chọn đăng nhập bằng:

* **ChatGPT account**
* hoặc **API key**

Chọn **ChatGPT account** nếu đang dùng tài khoản ChatGPT bình thường.

## 12. Bước 9 — Tạo thư mục làm việc 

```bash
mkdir -p ~/projects
mkdir -p ~/projects/test-codex
```

Vào đó:

```bash
cd ~/projects/test-codex
```

Rồi mở Codex:

```bash
codex
```

Hoặc mở thẳng bằng một lệnh:

```bash
codex -C ~/projects/test-codex
```

---

## 14. Sau khi cài xong lần đầu, máy sẽ có:

* Windows đã có **WSL**
* WSL có **Ubuntu**
* Ubuntu có **node** và **npm**
* đã cài **Codex CLI**
* đã đăng nhập bằng tài khoản ChatGPT
* chỉ cần gõ `codex` là dùng được

---

# PHẦN B — CÁCH MỞ LẠI MỖI NGÀY

## 15. Cách sử dụng mỗi ngày

1. Mở Ubuntu
2. Vào đúng thư mục project
3. Gõ `codex`

---

### Cách 1 — Mở từ Start Menu

1. Bấm **Start**
2. Gõ **Ubuntu**
3. Mở ứng dụng **Ubuntu**

Khi Ubuntu mở lên, bạn sẽ thấy dạng:

```bash
clement@DESKTOP-XXXX:~$
```

Lúc đó làm tiếp:

```bash
cd ~/projects/test-codex
codex
```

---

### Cách 2 — Cách mở bằng lệnh từ Windows

Nếu muốn mở từ PowerShell / Windows Terminal:

```powershell
wsl
```

hoặc vào đúng Ubuntu:

```powershell
wsl --distribution Ubuntu
```

Sau đó trong Ubuntu:

```bash
cd ~/projects/test-codex
codex
```

---

### Cách 3 — Cách mở thẳng đúng thư mục luôn

Nếu muốn gọn hơn, sau khi vào Ubuntu bạn có thể chạy luôn:

```bash
codex -C ~/projects/test-codex
```

---
## Nếu muốn xem trạng thái

```text
/status
```

Lệnh này giúp xem:

* model đang dùng
* thư mục hiện tại
* policy / trạng thái phiên

---

## Nếu muốn thoát Codex

Trong Codex, gõ:

```text
/exit
```

Hoặc dùng:

* `Ctrl + C`


# PHẦN C — GỢI Ý CẤU TRÚC THƯ MỤC NÊN DÙNG

## 25. Nên tạo thư mục kiểu này

```bash
~/projects
~/projects/test-codex
~/projects/project-1
~/projects/project-2
```

Ví dụ:

```bash
mkdir -p ~/projects/arduino-demo
mkdir -p ~/projects/esp32-demo
mkdir -p ~/projects/ballandbeam
```

### Khi làm project nào thì vào project đó

Ví dụ:

```bash
cd ~/projects/esp32-demo
codex
```

---

# PHẦN D — CHECKLIST NHANH

## 26. Checklist cài lần đầu

```text
1. Mở PowerShell Admin
2. Chạy: wsl --install
3. Restart máy
4. Mở Ubuntu
5. Tạo username/password
6. Chạy: sudo apt update
7. Chạy: sudo apt upgrade -y
8. Chạy: sudo apt install -y nodejs npm
9. Nếu npm lỗi quyền thì sửa ~/.local và PATH
10. Chạy: npm i -g @openai/codex
11. Chạy: codex
12. Đăng nhập bằng ChatGPT
13. Tạo thư mục project
14. cd vào project và mở codex
```

## 27. Checklist mở lại mỗi ngày

```text
1. Mở Ubuntu
2. cd vào thư mục project
3. Gõ codex
4. Làm việc
5. Xong thì /exit
```

---
