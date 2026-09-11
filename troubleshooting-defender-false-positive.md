# Khắc phục: Windows Defender chặn ứng dụng không khởi động được

## Triệu chứng

- Cài đặt `Agents.Windows_0.3.0_x64-setup.exe` báo thành công nhưng mở app không lên.
- Trước đó app dùng bình thường, đang dùng thì tự thoát và không mở lại được.
- Gỡ cài đặt rồi cài lại vẫn không mở lên.

## Nguyên nhân

**Windows Defender (Microsoft Defender) nhận diện sai (false positive) file thực thi chính `agents-windows-app.exe` là mã độc `Trojan:Win32/Bearfoos.A!ml` và tự động xóa ngay khi installer ghi file ra đĩa.**

Đây là phát hiện dựa trên heuristic machine learning (thẻ `!ml`), không phải signature cố định — rất phổ biến với ứng dụng Tauri/Rust chưa ký chứng chỉ số (code signing certificate).

### Chuỗi sự kiện

1. Installer NSIS ghi `agents-windows-app.exe` (~24 MB) vào `C:\Users\<user>\AppData\Local\Agents Windows\`.
2. Defender real-time protection quét file ngay khi được ghi, match heuristic `!ml` → xóa file.
3. Thư mục cài đặt chỉ còn 2 file phụ (`bench_dir_load.exe`, `uninstall.exe`) — file chính biến mất.
4. Không có exe để khởi động → ứng dụng "không mở lên được".

### Bằng chứng

Bản ghi `Get-MpThreatDetection` cho thấy nhiều lần phát hiện, tất cả đều nhắm vào đúng file:

```
ThreatName  : Trojan:Win32/Bearfoos.A!ml
Resources   : file:_C:\Users\<user>\AppData\Local\Agents Windows\agents-windows-app.exe
ProcessName : C:\Users\<user>\Downloads\Agents.Windows_0.3.0_x64-setup.exe  (lúc installer đang cài)
ProcessName : C:\Windows\explorer.exe                                        (scan nền)
```

## Cách khắc phục

> Tất cả lệnh PowerShell dưới đây cần chạy **dạng Administrator**
> (chuột phải Start → "Terminal (Admin)" hoặc "PowerShell (Admin)").

### Bước 1 — Thêm thư mục cài đặt vào exclusion của Defender

```powershell
Add-MpPreference -ExclusionPath "C:\Users\$env:USERNAME\AppData\Local\Agents Windows"
```

Nếu muốn loại trừ luôn file installer để cài lại không bị chặn:

```powershell
Add-MpPreference -ExclusionPath "C:\Users\$env:USERNAME\Downloads\Agents.Windows_0.3.0_x64-setup.exe"
```

### Bước 2 — Cài lại ứng dụng

Click đúp file installer hoặc chạy:

```powershell
Start-Process "C:\Users\$env:USERNAME\Downloads\Agents.Windows_0.3.0_x64-setup.exe"
```

### Bước 3 — Khởi động ứng dụng

```powershell
Start-Process "C:\Users\$env:USERNAME\AppData\Local\Agents Windows\agents-windows-app.exe"
```

### Trường hợp vẫn bị chặn

Nếu chính sách tổ chức hoặc Defender cloud-delivery protection vẫn xóa file sau khi thêm exclusion, tạm tắt real-time protection trong lúc cài:

```powershell
# Tắt tạm thời
Set-MpPreference -DisableRealtimeMonitoring $true

# Cài lại (Bước 2), khởi động (Bước 3), xác nhận app chạy OK

# Bật lại ngay sau khi xong
Set-MpPreference -DisableRealtimeMonitoring $false
```

## Giải pháp lâu dài cho nhà phát triển

False positive này sẽ tiếp tục xảy ra cho người dùng cuối cho đến khi ứng dụng được ký bởi chứng chỉ số hợp lệ. Các hướng giải quyết:

### 1. Ký chứng chỉ số (code signing) — giải pháp triệt để

Mua chứng chỉ code signing (OV hoặc EV) và ký installer + exe trong quá trình build:

```json
// tauri.conf.json — thêm section	sign
// Cần đặt biến môi trường: SIGNTOOL, CERTIFICATE_PATH, CERTIFICATE_PASSWORD
```

Với **EV Code Signing Certificate**, Defender sẽ tin tưởng ngay lập tức mà không cần build reputation. **OV Certificate** cần thời gian tích lũy reputation.

### 2. Gửi file lên Microsoft để whitelist

Microsoft cung cấp portal [Microsoft Security Intelligence submission](https://www.microsoft.com/wdsi/filesubmission) để nhà phát triển gửi bản build bị false positive, Microsoft sẽ review và thêm vào danh sách an toàn.

### 3. Hướng dẫn người dùng

Trước khi có chứng chỉ số, thêm hướng dẫn này vào README hoặc trang download để người dùng biết cách xử lý khi bị Defender chặn.

## Kiểm tra sau khi khắc phục

Xác nhận file exe tồn tại sau khi cài:

```powershell
Test-Path "C:\Users\$env:USERNAME\AppData\Local\Agents Windows\agents-windows-app.exe"
# Phải trả về True
```

Xác nhận process chạy sau khi khởi động:

```powershell
Get-Process -Name "agents-windows-app" -ErrorAction SilentlyContinue
# Phải trả về thông tin process
```
