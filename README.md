# Chrome MV2 Extension Patcher (v1.16.1)

> **Tác giả gốc:** [Sketchystan1/chrome-mv2-patch](https://github.com/Sketchystan1/chrome-mv2-patch) (Phát hành theo [MIT License](LICENSE) - Copyright (c) 2026 Sketchy)  
> **Bản dựng độc lập:** [Huytdn123/chrome-mv2-patch](https://github.com/Huytdn123/chrome-mv2-patch)

Khôi phục hỗ trợ tiện ích mở rộng Manifest V2 (MV2) cho Google Chrome (152–159).  
Windows: Sử dụng `version.dll` proxy nạp vào bộ nhớ khi Chrome khởi động và vá cổng MV2 trong RAM. Giữ nguyên file gốc, DRM Widevine hoạt động bình thường.

## Cài đặt trên Windows (Chrome 152–159 x64, x86, ARM64)

Chạy lệnh sau trong PowerShell hoặc Terminal:

```powershell
powershell "irm github.com/Huytdn123/chrome-mv2-patch/raw/main/chrome-mv2.ps1|iex"
```

<details> 
    <summary>Cài đặt thủ công</summary>
    Tải file <code>version.dll-v1.16.0.zip</code> từ Releases, copy file <code>version.dll</code> phù hợp kiến trúc và <code>signatures.json</code> đặt cạnh <code>chrome.exe</code>.  
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
