# Cài đặt Build Tools trên Windows

## Cách 1 (Khuyến nghị): Visual Studio Build Tools

1.  Tải **Build Tools for Visual Studio**:
    https://visualstudio.microsoft.com/visual-cpp-build-tools/

2.  Chạy trình cài đặt.

3.  Trong **Visual Studio Installer**, chọn:

-   Desktop development with C++

4.  Đảm bảo các thành phần sau được chọn:

-   MSVC v143 (hoặc phiên bản mới nhất)
-   Windows 10 SDK hoặc Windows 11 SDK
-   C++ CMake tools for Windows

5.  Nhấn **Install** và chờ hoàn tất.

6.  Khởi động lại Command Prompt hoặc PowerShell.

------------------------------------------------------------------------

## Kiểm tra cài đặt

``` cmd
cl
```

Nếu hiển thị:

``` text
Microsoft (R) C/C++ Optimizing Compiler...
```

là đã cài thành công.

Kiểm tra MSBuild:

``` cmd
msbuild -version
```

------------------------------------------------------------------------

## Nếu dùng Node.js

Kiểm tra:

``` cmd
node -v
npm -v
```

Sau đó:

``` cmd
npm install
```

------------------------------------------------------------------------

## Nếu dùng Python

Kiểm tra:

``` cmd
python --version
```

hoặc:

``` cmd
py --version
```

Nếu chưa có Python, tải tại:

https://www.python.org/downloads/windows/

------------------------------------------------------------------------

## Cài bằng Winget

``` powershell
winget install Microsoft.VisualStudio.2022.BuildTools
```

Sau khi cài, mở Visual Studio Installer và chọn:

-   Desktop development with C++

------------------------------------------------------------------------

## Ghi chú

Build Tools thường cần cho các dự án sử dụng native module như:

-   node-gyp
-   sharp
-   sqlite3
-   canvas
-   bcrypt

Nếu gặp lỗi khi `npm install`, hãy kiểm tra:

-   Đã cài MSVC
-   Đã cài Windows SDK
-   Đã cài Python 3
-   Đã khởi động lại terminal
