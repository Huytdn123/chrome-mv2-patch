# Chrome MV2 Extension Patcher (Bản v1.16.0 Độc Lập)

Công cụ khôi phục khả năng hỗ trợ tiện ích mở rộng **Manifest V2 (MV2)** (như uBlock Origin MV2) trên Google Chrome phiên bản từ **152 đến 159**.

> **Lưu ý về nguồn gốc & bản quyền:**  
> Dự án này được fork và duy trì độc lập từ dự án gốc [Sketchystan1/chrome-mv2-patch](https://github.com/Sketchystan1/chrome-mv2-patch) theo giấy phép [MIT License](LICENSE). Mọi quyền tác giả gốc (Copyright (c) 2026 Sketchy) được giữ nguyên vẹn.

---

## 1. Giới thiệu & Cơ chế hoạt động

- **Phương pháp In-Memory (Windows):** Sử dụng thư viện `version.dll` đặt cạnh `chrome.exe`. Khi Chrome khởi động, nó tự động tải `version.dll` trước `chrome.dll` và tiến hành patch cổng kiểm tra Manifest V2 trực tiếp trên bộ nhớ RAM.
- **Không can thiệp file gốc:** File `chrome.dll` trên ổ đĩa hoàn toàn không bị chỉnh sửa, đảm bảo chứng chỉ số Authenticode và hệ thống DRM Widevine (Netflix, Spotify, xem video bản quyền...) hoạt động bình thường 100%.
- **Tự động thích ứng:** Phiên bản DLL tự nạp bảng chữ ký (`signatures.json`) tương ứng với từng phiên bản Chrome (152–159).

---

## 2. Các cải tiến và sửa lỗi trong phiên bản này

Bản dựng này cố định ở phiên bản ổn định **v1.16.0**, loại bỏ hoàn toàn sự phụ thuộc vào upstream và khắc phục các lỗi sau:

1. **Sửa lỗi Int32 Overflow khi quét thư mục:**
   - Kiểm tra chặt chẽ tên thư mục phiên bản hợp lệ trước khi so sánh (`Major.Minor.Build.Patch`).
   - Xử lý các thư mục hệ thống có tên dài hoặc chứa ký tự đặc biệt (`Crashpad`, `SetupMetrics`...) mà không gây lỗi tràn số nguyên Int32 trong PowerShell.
   - Bảo toàn kiểm tra chữ ký và kiểm tra toàn vẹn Authenticode.
2. **Cố định đường dẫn Release & Xác thực SHA-256:**
   - Cố định tải gói `version.dll` từ Release v1.16.0 của repository `Huytdn123/chrome-mv2-patch`.
   - Cố định URL tải `signatures.json` về tag v1.16.0.
   - Tự động kiểm tra mã băm SHA-256 của file zip và file DLL tương ứng (`x64`, `x86`, `arm64`) trước khi tiến hành cài đặt nhằm đảm bảo an toàn tuyệt đối.
3. **Sửa lỗi luồng biến Menu (Check status chạy nhầm Install):**
   - Đồng bộ hóa biến `$script:Command` và `$Command` giữa menu tương tác và hàm điều phối `Invoke-Main`.
   - Lựa chọn `k` (hoặc `4`) chạy chính xác `Check status` (chế độ chỉ đọc, không ghi đè file hay Registry).
   - Hỗ trợ đầy đủ cả phím số (`1`, `2`, `3`, `4`, `5`) lẫn phím tắt (`i`, `u`, `s`, `k`, `q`).

---

## 3. Hướng dẫn cài đặt nhanh (PowerShell)

Mở PowerShell (không cần quyền Administrator trước, script sẽ tự yêu cầu khi cần ghi file hệ thống) và chạy lệnh sau:

```powershell
irm "https://raw.githubusercontent.com/Huytdn123/chrome-mv2-patch/main/chrome-mv2.ps1" | iex
```

### Menu tương tác

Nếu không truyền tham số, script sẽ hiển thị menu:

```text
Select browser:
  [1]    Choose the numbered browser above
  [c]    Use a custom path
  [q]    Quit

What would you like to do?
  [1/i]  Install / repair MV2         (default)
  [2/u]  Uninstall (remove version.dll + uBlock Origin)
  [3/s]  Update signatures
  [4/k]  Check status
  [5/q]  Quit
```

### Các tùy chọn dòng lệnh nâng cao

Bạn có thể chạy trực tiếp với các tham số:

- **Kiểm tra trạng thái (chỉ đọc):**
  ```powershell
  .\chrome-mv2.ps1 check
  ```
- **Gỡ cài đặt hoàn toàn:**
  ```powershell
  .\chrome-mv2.ps1 uninstall
  ```
- **Cập nhật bảng chữ ký mới nhất:**
  ```powershell
  .\chrome-mv2.ps1 update
  ```
- **Cài đặt không kèm uBlock Origin MV2:**
  ```powershell
  .\chrome-mv2.ps1 install -NoUblock
  ```
- **Chỉ định đường dẫn Chrome tùy ý:**
  ```powershell
  .\chrome-mv2.ps1 install "C:\Path\To\Google\Chrome\Application\chrome.dll"
  ```
- **Chế độ tự động không hỏi (dành cho script):**
  ```powershell
  .\chrome-mv2.ps1 install -Yes -Quiet
  ```

---

## 4. Bảng kiểm tra toàn vẹn (SHA-256 Checksums)

Tất cả các bản dựng nhị phân trong Release v1.16.0 đều được đối chiếu với mã băm SHA-256 chính thức:

| Tệp tin | Kích thước | SHA-256 Checksum |
|---|---|---|
| `version.dll-v1.16.0.zip` | 308,214 bytes | `FD7CF43ADEAC73375F83E956F2E43B5BF84506C4B6AF5245557225DCB9B68B5F` |
| `x64/version.dll` | 255,488 bytes | `8544C3229C8E0E4D075CDE78AC04E072BF9AC201101A031BD1D3E12211FC78A0` |
| `x86/version.dll` | 197,632 bytes | `008238E5739C2FC52A07168E9E6F553116E3166C4508251728891D7829D2A430` |
| `arm64/version.dll` | 212,992 bytes | `77B91E8836CDB81B2CAAD996C9FCF35DACD918558FDA9DF85F4FA61C3621861A` |

---

## 5. Linux & macOS

Trên Linux và macOS (Apple Silicon ARM64), công cụ sử dụng `chrome-mv2.sh`:

```bash
curl -fsSL https://raw.githubusercontent.com/Huytdn123/chrome-mv2-patch/main/chrome-mv2.sh | sudo bash
```

---

## 6. Giấy phép & Tuyên bố từ chối trách nhiệm

Dự án này được phân phối theo [MIT License](LICENSE). Bạn được toàn quyền sử dụng, sửa đổi và phân phối theo các điều khoản của giấy phép MIT.
