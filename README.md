# Agents Windows Releases

[![Latest Release](https://img.shields.io/github/v/release/ntd237/agents-windows-app-releases?style=flat-square)](https://github.com/ntd237/agents-windows-app-releases/releases/latest)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE)
[![Last Updated](https://img.shields.io/github/last-commit/ntd237/agents-windows-app-releases?style=flat-square)](https://github.com/ntd237/agents-windows-app-releases/commits/main)

Kênh phân phối công khai cho ứng dụng riêng tư [agents-windows-app](https://github.com/ntd237/agents-windows-app): bao gồm các bộ cài đặt NSIS, chữ ký xác minh bảo mật và manifest cập nhật tự động.

---

## Mục Lục

- [Giới Thiệu](#giới-thiệu)
- [Tính Năng](#tính-năng)
- [Tải Xuống](#tải-xuống)
- [Cài Đặt](#cài-đặt)
- [Cập Nhật](#cập-nhật)
- [Cấu Trúc Kho Lưu Trữ](#cấu-trúc-kho-lưu-trữ)
- [Liên Hệ](#liên-hệ)

---

## Giới Thiệu

Kho lưu trữ này phục vụ như một kênh phân phối công khai cho ứng dụng **Agents Windows**. 

### Mục Đích Chính

- **Phân phối an toàn**: Cung cấp các bộ cài đặt được xác minh bằng chữ ký số
- **Cập nhật tự động**: Hỗ trợ cơ chế cập nhật trong ứng dụng thông qua manifest `latest.json`
- **Bảo mật**: Sử dụng minisign để ký các tệp cài đặt, đảm bảo tính toàn vẹn và xác thực

### Lưu Ý Quan Trọng

- **Mã nguồn riêng tư**: Kho lưu trữ chính của ứng dụng được giữ riêng tư
- **Chỉ chứa tài sản phát hành**: Repository này chỉ lưu trữ các tệp phát hành (bộ cài đặt, chữ ký, manifest)
- **Tạo tự động**: Các phát hành được tạo tự động từ quy trình CI/CD

---

## Tính Năng

### Tính Năng Cơ Bản
- ✅ Bộ cài đặt Windows (`.exe`) 64-bit
- ✅ Chữ ký xác minh bảo mật (`.sig`)
- ✅ Manifest cập nhật tự động (`latest.json`)

### Tính Năng Bảo Mật
- ✅ Xác minh chữ ký bằng minisign
- ✅ Cải thiện độ tin cậy khi cài đặt
- ✅ Phát hiện các tệp bị sửa đổi hoặc giả mạo

---

## Tải Xuống

### Cách Tải Bộ Cài Đặt Mới Nhất

Tải phiên bản mới nhất từ [Releases](https://github.com/ntd237/agents-windows-app-releases/releases/latest):

```
https://github.com/ntd237/agents-windows-app-releases/releases/latest
```

### Tệp Sẵn Có

Mỗi phát hành bao gồm:

| Tệp | Mô Tả |
|-----|-------|
| `Agents.Windows_X.X.X_x64-setup.exe` | Bộ cài đặt cho Windows (64-bit) |
| `Agents.Windows_X.X.X_x64-setup.exe.sig` | Chữ ký xác minh bảo mật (minisign) |
| `latest.json` | Manifest cập nhật cho ứng dụng |

---

## Cài Đặt

### Yêu Cầu Hệ Thống

- Windows 10 hoặc mới hơn (64-bit)
- Quyền quản trị để cài đặt
- Kết nối Internet (để tải xuống)

### Hướng Dẫn Cài Đặt

#### Bước 1: Tải Xuống Bộ Cài Đặt

Tải tệp `Agents.Windows_X.X.X_x64-setup.exe` từ [Releases](https://github.com/ntd237/agents-windows-app-releases/releases/latest).

#### Bước 2: Xác Minh Chữ Ký (Tùy Chọn nhưng Khuyến Nghị)

Để xác minh tính toàn vẹn của bộ cài đặt:

1. Cài đặt [minisign](https://jedisct1.github.io/minisign/)
2. Tải chữ ký `Agents.Windows_X.X.X_x64-setup.exe.sig`
3. Chạy lệnh xác minh:

```bash
minisign -Vm Agents.Windows_X.X.X_x64-setup.exe -P <public-key>
```

*(Khóa công khai sẽ được cung cấp trong phần Bảo Mật)*

#### Bước 3: Chạy Bộ Cài Đặt

1. Nhấp đúp vào tệp `.exe` để khởi động bộ cài đặt
2. Làm theo các hướng dẫn trên màn hình
3. Chọn vị trí cài đặt hoặc chấp nhận mặc định
4. Hoàn thành cài đặt

#### Bước 4: Xác Minh Cài Đặt

Sau khi cài đặt hoàn thành:

1. Tìm "Agents" trong menu Start
2. Khởi chạy ứng dụng
3. Kiểm tra phiên bản trong menu Help → About

---

## Cập Nhật

### Cập Nhật Tự Động

Ứng dụng **Agents Windows** hỗ trợ cập nhật tự động:

1. Ứng dụng kiểm tra file `latest.json` từ kho này
2. Nếu phiên bản mới khả dụng, người dùng sẽ nhận thông báo
3. Nhấp nút "Cập Nhật" để tải và cài đặt phiên bản mới

### Cập Nhật Thủ công

Nếu cập nhật tự động không hoạt động:

1. Tải xuống bộ cài đặt mới nhất từ [Releases](https://github.com/ntd237/agents-windows-app-releases/releases/latest)
2. Chạy bộ cài đặt (sẽ ghi đè phiên bản cũ)
3. Khởi động lại ứng dụng nếu cần

---

## Cấu Trúc Kho Lưu Trữ

```
agents-windows-app-releases/
├── README.md                          # Tài liệu này
├── .github/
│   └── workflows/                     # Quy trình CI/CD (nếu có)
└── releases/                          # Tệp phát hành (tự động quản lý)
    ├── v0.1.2/
    │   ├── Agents.Windows_0.1.2_x64-setup.exe
    │   ├── Agents.Windows_0.1.2_x64-setup.exe.sig
    │   └── latest.json
    └── ...
```

### Các Tệp Chính

| Tệp | Mục Đích |
|-----|---------|
| `README.md` | Tài liệu và hướng dẫn |
| `.exe` | Bộ cài đặt Windows |
| `.sig` | Chữ ký xác minh (minisign) |
| `latest.json` | Manifest phiên bản mới nhất |

---

## Liên Hệ

**Tác Giả**: ntd237

- **Email**: ntd237.work@gmail.com
- **GitHub**: [@ntd237](https://github.com/ntd237)
- **Repository Chính**: [agents-windows-app](https://github.com/ntd237/agents-windows-app) (riêng tư)

Nếu bạn có câu hỏi hoặc phát hiện vấn đề liên quan đến các bản phát hành, vui lòng mở một [Issue](https://github.com/ntd237/agents-windows-app-releases/issues).

---

**Lần cập nhật cuối**: 2026-09-05
