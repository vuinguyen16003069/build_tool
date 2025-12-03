# Hướng dẫn cài đặt Node-gyp trên Windows (Không cần WSL)

Hướng dẫn này giúp bạn thiết lập môi trường Windows để **cài đặt và build các module Node.js yêu cầu node-gyp**, mà không cần WSL hay cài cả Visual Studio nặng.

---

## 1. Yêu cầu hệ thống

* Windows 10/11
* Node.js >= 18.x (khuyến nghị LTS)
* Python 3.10 – 3.12
* Microsoft Build Tools 2022 (nhẹ hơn Visual Studio đầy đủ)
* MSBuild và Windows SDK

---

## 2. Cài đặt Microsoft Build Tools 2022

Tải về từ: [Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

**Khi cài đặt, chỉ chọn:**

* **Desktop development with C++**
* Trong đó tick:

  * MSVC v143 Build Tools
  * Windows 10 SDK
  * C++ CMake tools (tuỳ chọn nhưng khuyến nghị)
  * C++ ATL (optional)

> Tổng dung lượng: ~2 GB, nhẹ hơn nhiều so với Visual Studio full.

---

## 3. Kiểm tra MSBuild

Mở CMD hoặc PowerShell và chạy:

```powershell
"C:\Program Files\Microsoft Visual Studio\Installer\vswhere.exe" -latest -products * -find MSBuild\**\MSBuild.exe
```

Nếu trả về path dạng:

```
C:\Program Files\Microsoft Visual Studio\2022\BuildTools\MSBuild\Current\Bin\MSBuild.exe
```

→ OK.

Thêm MSBuild vào PATH:

```powershell
setx PATH "%PATH%;C:\Program Files\Microsoft Visual Studio\2022\BuildTools\MSBuild\Current\Bin"
```

> Sau đó mở cửa sổ CMD/PowerShell mới để PATH có hiệu lực.

---

## 4. Cài Python

Tải Python 3.10 – 3.12 từ [python.org](https://www.python.org/downloads/windows/)

Khi cài, tick:

* **Add Python to PATH**

---

## 5. Cài node-gyp và thiết lập MSVS version

```powershell
npm install -g node-gyp
npm config set msvs_version 2022 --global
```

> Lưu ý: `msvs_version` chỉ hợp lệ nếu đã cài Build Tools 2022.

---

## 6. Cài module Node yêu cầu node-gyp

Ví dụ:

```powershell
npm install canvas
npm install lzma-native
```

Nếu gặp lỗi prebuilt binaries không có → node-gyp sẽ tự build bằng Build Tools + Python.

---

## 7. Test môi trường

Chạy trong thư mục module:

```powershell
node-gyp configure
node-gyp build
```

Nếu không báo lỗi → môi trường Windows đã chuẩn.

---

## 8. Lời khuyên

* **Không dùng WSL** nếu bạn muốn module Node chạy trực tiếp trên Windows.
* Cài Build Tools thay vì Visual Studio full → nhẹ, nhanh, ít lỗi.
* Luôn mở CMD/PowerShell mới sau khi thay đổi PATH hoặc cài Build Tools.
* Nếu module có prebuilt binary fail, node-gyp sẽ compile source → cần Build Tools + Python đúng version.

---

**Tác giả:** Vui Nguyễn
**Ngày tạo:** 2025-12-03
