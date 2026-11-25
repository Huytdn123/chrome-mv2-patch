# Chrome MV2 Extension Patcher (v1.17.0)

> **Tác giả gốc:** [Sketchystan1/chrome-mv2-patch](https://github.com/Sketchystan1/chrome-mv2-patch) (Phát hành theo [MIT License](LICENSE) - Copyright (c) 2026 Sketchy)  
> **Bản dựng độc lập:** [Huytdn123/chrome-mv2-patch](https://github.com/Huytdn123/chrome-mv2-patch)

Khôi phục hỗ trợ tiện ích mở rộng Manifest V2 (MV2) và cài đặt tiện ích ngoài Store (`.crx` / uBlock Origin) cho **Google Chrome, Chromium, Microsoft Edge** (151–160+ trở lên).  
Windows: Sử dụng `secur32.dll` proxy với engine **Autoscan** tự động quét và vá cổng MV2 trong RAM (không cần `signatures.json`, giữ nguyên file gốc, DRM Widevine hoạt động bình thường).

## Cài đặt trên Windows (Chrome / Edge / Chromium 151–160+ x64, x86, ARM64)

Chạy lệnh sau trong PowerShell hoặc Terminal:

```powershell
powershell "irm github.com/Huytdn123/chrome-mv2-patch/raw/main/chrome-mv2.ps1|iex"
```

<details> 
    <summary>Cài đặt thủ công</summary>
    Tải file <code>mv2-patch-1.17.0-win-&lt;arch&gt;.zip</code> từ Releases, copy file <code>secur32.dll</code> đặt cạnh <code>chrome.exe</code> hoặc <code>msedge.exe</code> (xóa <code>version.dll</code> cũ nếu có).  
    Cài uBlock Origin MV2 qua Registry (chạy Terminal quyền Admin):

    reg.exe add "HKLM\Software\Google\Chrome\Extensions\fkgkibajhfbepljeaefdnfnegdcjomkh" /v update_url /t REG_SZ /d "https://github.com/gorhill/uBlock/raw/refs/heads/master/dist/chromium/update.xml" /f /reg:32
</details>

## Linux, macOS
<details>
  <summary>Xem thêm</summary>
    Chrome 152–159 x64, ARM, macOS ARM:

    curl -fsSL https://raw.githubusercontent.com/Huytdn123/chrome-mv2-patch/main/chrome-mv2.sh | sudo bash
</details>

## License

Phát hành theo giấy phép [MIT License](LICENSE).
