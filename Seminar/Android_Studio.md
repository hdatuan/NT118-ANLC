# CHƯƠNG 1. TỔNG QUAN ANDROID VÀ ANDROID STUDIO

---

## 1.1. Tổng quan về nền tảng Android

### Giới thiệu hệ điều hành Android

Android là hệ điều hành di động mã nguồn mở, được Google phát triển và dựa trên nhân Linux. Ra mắt lần đầu vào năm 2008, Android hiện là hệ điều hành di động phổ biến nhất thế giới với hơn **70% thị phần toàn cầu**.

Một số mốc quan trọng:
- **2003**: Android Inc. được thành lập bởi Andy Rubin.
- **2005**: Google mua lại Android Inc.
- **2008**: Android 1.0 ra mắt cùng thiết bị HTC Dream.
- **2019**: Android trở thành hệ điều hành được sử dụng bởi hơn 2,5 tỷ thiết bị.

### Đặc điểm của ứng dụng Android

- **Đa nhiệm (Multitasking):** Nhiều ứng dụng có thể chạy đồng thời.
- **Sandbox Model:** Mỗi ứng dụng chạy trong một tiến trình riêng biệt, cách ly với các ứng dụng khác để tăng bảo mật.
- **Phân quyền (Permissions):** Ứng dụng phải xin quyền truy cập tài nguyên hệ thống (camera, GPS, danh bạ,...) từ người dùng.
- **Đa dạng màn hình:** Android hỗ trợ nhiều kích thước, độ phân giải màn hình và mật độ điểm ảnh (DPI) khác nhau.
- **Phân phối qua Google Play Store** hoặc các kênh tải trực tiếp (APK sideloading).

### Tổng quan quy trình phát triển ứng dụng Android

```
Lên ý tưởng → Thiết kế UI/UX → Lập trình (Kotlin/Java) 
    → Build (Gradle) → Test (Unit Test / UI Test) 
    → Deploy (Google Play Store)
```

---

## 1.2. Android Architecture and Components

### Kiến trúc hệ điều hành Android (từ dưới lên)

Android được tổ chức thành nhiều tầng, mỗi tầng đảm nhiệm một chức năng riêng biệt:

| Tầng | Mô tả |
|------|-------|
| **Linux Kernel** | Nền tảng cốt lõi: quản lý driver phần cứng (Camera, Bluetooth, USB...), bộ nhớ, tiến trình, và năng lượng. |
| **Hardware Abstraction Layer (HAL)** | Lớp trừu tượng hóa phần cứng, cung cấp interface chuẩn để Android Framework giao tiếp với phần cứng mà không cần biết chi tiết driver. |
| **Android Runtime (ART)** | Môi trường thực thi ứng dụng Android. Biên dịch bytecode (`.dex`) sang mã máy thông qua AOT (Ahead-of-Time) và JIT (Just-in-Time) compilation. Thay thế cho Dalvik VM. |
| **Native Libraries** | Các thư viện C/C++ dùng nội bộ: OpenGL ES (đồ họa), SQLite (cơ sở dữ liệu), WebKit (trình duyệt),... |
| **Application Framework** | Bộ API Java/Kotlin mà developer sử dụng: Activity Manager, Content Provider, Notification Manager, Location Manager,... |
| **Applications** | Tầng ứng dụng: nơi các ứng dụng người dùng (bao gồm ứng dụng hệ thống lẫn ứng dụng bên thứ ba) hoạt động. |

### Các thành phần chính của ứng dụng Android

Android định nghĩa 4 loại thành phần cơ bản (Application Components), mỗi loại có vòng đời và mục đích riêng:

#### Activity
- Đại diện cho **một màn hình giao diện người dùng** (UI).
- Ví dụ: Màn hình đăng nhập, màn hình danh sách sản phẩm.
- Mỗi Activity có vòng đời riêng (Lifecycle) và được quản lý bởi **Back Stack**.

#### Service
- Chạy **tác vụ nền (background)** mà không cần giao diện.
- Ví dụ: Phát nhạc, tải tệp, đồng bộ dữ liệu.
- Hai loại chính: **Foreground Service** (hiển thị notification) và **Background Service**.

#### Broadcast Receiver
- **Lắng nghe và phản hồi các sự kiện hệ thống** hoặc ứng dụng khác phát đi.
- Ví dụ: Nhận sự kiện "pin yếu", "kết nối mạng thay đổi", "tin nhắn đến".

#### Content Provider
- Cơ chế **chia sẻ dữ liệu** giữa các ứng dụng một cách an toàn và có kiểm soát.
- Ví dụ: Ứng dụng ảnh chia sẻ thư viện ảnh với các ứng dụng khác qua Content Provider.

### AndroidManifest và Resources

- **AndroidManifest.xml**: File cấu hình tổng thể của ứng dụng. Khai báo tất cả các thành phần (Activity, Service,...), quyền truy cập (permissions), phiên bản SDK tối thiểu, và các metadata khác.
- **Resources (`res/`)**: Chứa tài nguyên tách biệt khỏi code:
  - `layout/` – File XML mô tả giao diện.
  - `drawable/` – Hình ảnh, icon, vector.
  - `values/` – Chuỗi văn bản (`strings.xml`), màu sắc (`colors.xml`), kích thước (`dimens.xml`).
  - `mipmap/` – Icon ứng dụng ở các độ phân giải khác nhau.

### Vòng đời cơ bản của Activity

```
onCreate() → onStart() → onResume() ← [App đang chạy]
                                           ↓
                                       onPause()
                                           ↓
                                       onStop()
                                           ↓
                                       onDestroy()
```

---

## 1.3. Tổng quan về Android Studio

### Android Studio là gì?

Android Studio là **Môi trường Phát triển Tích hợp (IDE) chính thức** dành cho phát triển ứng dụng Android, được Google phát triển dựa trên nền tảng **IntelliJ IDEA** của JetBrains. Ra mắt năm 2014, thay thế Eclipse ADT.

### Vai trò của Android Studio

Android Studio tích hợp toàn bộ công cụ cần thiết vào một môi trường duy nhất:
- Viết và chỉnh sửa code (Kotlin, Java, XML).
- Build và đóng gói ứng dụng.
- Chạy và kiểm thử trên thiết bị ảo hoặc thật.
- Debug và phân tích hiệu năng.
- Quản lý phiên bản SDK và phụ thuộc (dependencies).

### Các thành phần chính

| Thành phần | Mô tả |
|-----------|-------|
| **Android SDK** | Bộ công cụ và thư viện cần thiết để xây dựng ứng dụng Android (Platform Tools, Build Tools, API levels). |
| **Gradle** | Hệ thống build tự động. Quản lý dependencies, biên dịch code và đóng gói thành file `.apk` hoặc `.aab`. |
| **Emulator / AVD Manager** | Tạo và quản lý thiết bị Android ảo (Android Virtual Device) để test ứng dụng mà không cần thiết bị thật. |
| **Debugger** | Đặt breakpoint, kiểm tra giá trị biến, theo dõi luồng thực thi khi ứng dụng đang chạy. |
| **Logcat** | Hiển thị log hệ thống và log của ứng dụng theo thời gian thực, hỗ trợ lọc theo tag, level (DEBUG, ERROR,...). |

### Cấu trúc cơ bản của một Android Project

```
MyApp/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com.example.myapp/  ← Source code Kotlin/Java
│   │   │   ├── res/                      ← Tài nguyên (layout, drawable,...)
│   │   │   └── AndroidManifest.xml       ← Cấu hình ứng dụng
│   │   └── test/                         ← Unit Tests
│   └── build.gradle                      ← Cấu hình build của module app
├── gradle/
└── build.gradle                          ← Cấu hình build toàn project
```

---

## 1.4. Setting up Android Studio

### Yêu cầu hệ thống (khuyến nghị)

| Yêu cầu | Tối thiểu | Khuyến nghị |
|---------|-----------|-------------|
| RAM | 8 GB | 16 GB+ |
| Ổ cứng | 8 GB trống | SSD 16 GB+ |
| Màn hình | 1280×800 | 1920×1080 |
| OS | Windows 8 / macOS 10.14 / Ubuntu 20.04 | Phiên bản mới nhất |

### Các bước cài đặt

1. Tải Android Studio tại [developer.android.com/studio](https://developer.android.com/studio).
2. Chạy installer và làm theo hướng dẫn.
3. Khởi động lần đầu – **Setup Wizard** sẽ tự động tải Android SDK.

### Cài đặt và cấu hình Android SDK

- Vào **SDK Manager** (`Tools → SDK Manager`).
- Tải các **Android API Level** cần thiết (ví dụ: API 34 – Android 14).
- Tải **SDK Build Tools** và **Platform Tools**.

### Tạo Android Virtual Device (AVD)

1. Vào **Device Manager** (`Tools → Device Manager`).
2. Chọn **Create Virtual Device**.
3. Chọn thiết bị (Pixel 8, Tablet,...).
4. Chọn System Image (phiên bản Android).
5. Cấu hình RAM, bộ nhớ và khởi động emulator.

### Kết nối và chạy trên thiết bị thật

1. Bật **Developer Options** trên điện thoại (`Settings → About Phone → tap Build Number 7 lần`).
2. Bật **USB Debugging**.
3. Kết nối điện thoại qua USB.
4. Chọn thiết bị trong Android Studio và nhấn **Run**.

---

## 1.5. Creating and Running a Basic Android App *(Demo)*

### Tạo project mới

1. Mở Android Studio → **New Project**.
2. Chọn template: **Empty Activity** (Jetpack Compose) hoặc **Empty Views Activity**.
3. Cấu hình:
   - **Name**: `HelloWorldApp`
   - **Package name**: `com.example.helloworldapp`
   - **Language**: Kotlin
   - **Minimum SDK**: API 24 (Android 7.0)

### Các file và thư mục quan trọng

- `MainActivity.kt` – Activity chính, điểm vào của ứng dụng.
- `activity_main.xml` – File layout XML định nghĩa giao diện.
- `AndroidManifest.xml` – Khai báo Activity và cấu hình ứng dụng.
- `build.gradle (Module: app)` – Khai báo dependencies và cấu hình build.

### Ví dụ: Hello World với Jetpack Compose

```kotlin
// MainActivity.kt
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            HelloWorldTheme {
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    Greeting("Android")
                }
            }
        }
    }
}

@Composable
fun Greeting(name: String) {
    Text(
        text = "Hello, $name!",
        modifier = Modifier.padding(16.dp)
    )
}
```

### Build và chạy ứng dụng

- **Build**: `Build → Make Project` hoặc `Ctrl+F9`.
- **Run**: Chọn thiết bị (Emulator / Thiết bị thật) → Nhấn **Run** (`Shift+F10`).
- **Xem log**: Mở **Logcat** để theo dõi output và lỗi.

