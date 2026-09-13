# Câu hỏi trắc nghiệm – Seminar NT118

> **Chủ đề:** Android & Android Studio · Kotlin · Gemini in Android Studio
> **Tổng số câu:** 30 câu (10 câu/chương)
> ✅ = Đáp án đúng · 💡 = Giải thích

---

## Chương 1 – Android & Android Studio *(10 câu)*

---

**Câu 1.** Android Inc. – công ty tạo ra hệ điều hành Android – được Google mua lại vào năm nào?

- A. 2003
- B. 2004
- C. 2005 ✅
- D. 2008

> 💡 Android Inc. được Andy Rubin thành lập năm 2003. Google mua lại năm 2005 với giá ~50 triệu USD. Android 1.0 chính thức ra mắt năm 2008 cùng thiết bị HTC Dream.

---

**Câu 2.** Tầng nào trong kiến trúc Android đóng vai trò "phiên dịch viên" – giúp Android Framework giao tiếp với driver phần cứng mà *không cần biết* chi tiết từng loại phần cứng?

- A. Linux Kernel
- B. Android Runtime (ART)
- C. Hardware Abstraction Layer (HAL) ✅
- D. Application Framework

> 💡 HAL cung cấp interface chuẩn cho mỗi loại phần cứng (Camera, Bluetooth, GPS...). Nhờ HAL, cùng một Android Framework có thể chạy trên hàng nghìn model điện thoại khác nhau.

---

**Câu 3.** Ứng dụng nhạc cần tiếp tục phát nhạc khi người dùng thoát ra màn hình chính (Home). Thành phần Android nào phù hợp nhất để xử lý điều này?

- A. Activity
- B. Content Provider
- C. Broadcast Receiver
- D. Service ✅

> 💡 Service chạy tác vụ nền mà không cần giao diện. Cụ thể hơn, Foreground Service (với notification) phù hợp cho nhạc – người dùng biết app đang chạy nền và có thể tương tác qua notification.

---

**Câu 4.** File nào trong Android project khai báo tất cả các thành phần (Activity, Service,...), quyền truy cập (permissions) và phiên bản SDK tối thiểu của ứng dụng?

- A. `build.gradle`
- B. `strings.xml`
- C. `AndroidManifest.xml` ✅
- D. `MainActivity.kt`

> 💡 AndroidManifest.xml là "khai sinh" của ứng dụng. Nếu một Activity không được khai báo trong Manifest, Android sẽ không biết đến sự tồn tại của nó và app sẽ crash khi cố gắng mở Activity đó.

---

**Câu 5.** Thứ tự đúng trong vòng đời Activity khi người dùng nhấn nút **Home** (ứng dụng thu nhỏ xuống nền)?

- A. `onPause()` → `onStop()` ✅
- B. `onStop()` → `onPause()`
- C. `onPause()` → `onDestroy()`
- D. `onStop()` → `onDestroy()`

> 💡 Nhấn Home → Activity mất focus (`onPause()`) → Activity không còn hiển thị (`onStop()`). Activity vẫn còn trong bộ nhớ, không bị destroy. Khi quay lại app: `onRestart()` → `onStart()` → `onResume()`.

---

**Câu 6.** Trong Android Studio, công cụ nào cho phép xem log của ứng dụng theo thời gian thực và lọc theo tag hoặc mức độ (DEBUG, ERROR,...)?

- A. Gradle
- B. AVD Manager
- C. Profiler
- D. Logcat ✅

> 💡 Logcat hiển thị tất cả log của hệ thống và app. Developer dùng `Log.d("TAG", "message")` trong code để ghi log, sau đó lọc theo TAG trong Logcat để debug. Có 5 mức: VERBOSE < DEBUG < INFO < WARN < ERROR.

---

**Câu 7.** Android Runtime (ART) dùng kỹ thuật nào để tối ưu hiệu năng ứng dụng khi cài đặt?

- A. Chỉ biên dịch từng dòng khi chạy (Interpreted)
- B. Biên dịch sang native code một lần khi cài đặt (AOT) ✅
- C. Gửi code lên server để biên dịch
- D. Chạy trực tiếp file `.kotlin` mà không cần biên dịch

> 💡 ART dùng AOT (Ahead-of-Time) – biên dịch bytecode `.dex` sang native code ngay lúc cài đặt. Điều này giúp app khởi động và chạy nhanh hơn so với Dalvik (dùng JIT – biên dịch từng đoạn lúc chạy).

---

**Câu 8.** Ứng dụng A muốn cho phép ứng dụng B đọc danh sách ảnh của mình một cách có kiểm soát và an toàn. Thành phần nào phù hợp?

- A. Service
- B. Broadcast Receiver
- C. Content Provider ✅
- D. Activity

> 💡 Content Provider là cơ chế chia sẻ dữ liệu có kiểm soát giữa các ứng dụng. Ví dụ thực tế: `MediaStore` (ảnh, video), `ContactsProvider` (danh bạ) đều là Content Provider mà bất kỳ app nào có quyền đều có thể truy cập.

---

**Câu 9.** Trong cấu trúc Android project, các file XML mô tả giao diện (layout) được đặt trong thư mục nào?

- A. `res/values/`
- B. `src/main/java/`
- C. `res/drawable/`
- D. `res/layout/` ✅

> 💡 `res/layout/` chứa file XML giao diện (ví dụ: `activity_main.xml`). `res/values/` chứa strings, colors, dimens. `res/drawable/` chứa hình ảnh và vector. `src/main/java/` chứa code Kotlin/Java.

---

**Câu 10.** Khi publish ứng dụng lên Google Play Store, Google khuyến nghị dùng định dạng file nào thay cho APK truyền thống?

- A. `.jar`
- B. `.dex`
- C. `.apk`
- D. `.aab` ✅

> 💡 AAB (Android App Bundle) cho phép Google Play tự tối ưu và chỉ gửi đúng phần code và resource cần thiết cho từng thiết bị → giảm dung lượng file người dùng phải tải xuống đáng kể (thường 15–20%).

---

## Chương 2 – Kotlin *(10 câu)*

---

**Câu 1.** Đoạn code Kotlin nào sau đây sẽ gây ra **lỗi compile**?

- A. `val x = 10`
- B. `var name: String? = null`
- C. `val greeting: String = null` ✅
- D. `var count: Int = 0`

> 💡 Trong Kotlin, kiểu `String` (không có `?`) là non-nullable – không thể gán `null`. Muốn cho phép null phải dùng `String?`. Lỗi được bắt ngay lúc compile, không phải lúc runtime như Java.

---

**Câu 2.** `data class` trong Kotlin tự động sinh ra những hàm nào mà Java bắt lập trình viên phải tự viết tay?

- A. Chỉ `toString()`
- B. `start()` và `stop()`
- C. `equals()`, `hashCode()`, `toString()`, `copy()` ✅
- D. Constructor và Destructor

> 💡 Một `data class User(val id: Int, val name: String)` thay thế hàng chục dòng Java boilerplate. Hàm `copy()` đặc biệt tiện: `val user2 = user1.copy(name = "Binh")` tạo bản sao với một field thay đổi.

---

**Câu 3.** Google tuyên bố Kotlin là ngôn ngữ **"first-class"** (được hỗ trợ chính thức ngang Java) cho Android vào năm nào?

- A. 2014
- B. 2016 (khi Kotlin 1.0 ra mắt)
- C. 2017 ✅
- D. 2019

> 💡 Tại Google I/O 2017, Google tuyên bố Kotlin là ngôn ngữ chính thức cho Android. Đến 2019, Google tuyên bố "Kotlin-first" – tất cả tài liệu, mẫu code và thư viện Jetpack mới đều ưu tiên Kotlin.

---

**Câu 4.** Lập trình viên muốn thêm hàm `isValidEmail()` vào class `String` có sẵn *mà không kế thừa* class đó. Đặc trưng nào của Kotlin cho phép điều này?

- A. Data Class
- B. Sealed Class
- C. Extension Function ✅
- D. Higher-order Function

> 💡 Extension Function cho phép "mở rộng" class của bất kỳ thư viện nào mà không cần source code. Cực kỳ phổ biến trong Jetpack: `View.gone()`, `Context.showToast()` đều là extension functions.

---

**Câu 5.** Cú pháp khai báo biến nào sau đây đúng trong Kotlin?

- A. `int count = 5;`
- B. `Int count = 5`
- C. `val count: Int = 5` ✅
- D. `const count = 5`

> 💡 Kotlin dùng `val` (immutable) hoặc `var` (mutable), theo sau là tên biến, rồi `: KiểuDữLiệu`. Kotlin không cần dấu chấm phẩy cuối câu. `const` trong Kotlin chỉ dùng cho hằng số compile-time trong companion object.

---

**Câu 6.** Toán tử `?.` và `?:` trong Kotlin lần lượt được gọi là gì?

- A. Force Unwrap và Null Check
- B. Safe Call và Elvis Operator ✅
- C. Null Assert và Default Value
- D. Optional Chain và Nil Coalescing

> 💡 `obj?.method()` (Safe Call) – chỉ gọi khi obj không null, ngược lại trả về null. `value ?: default` (Elvis) – trả về `value` nếu không null, ngược lại trả về `default`. Kết hợp: `obj?.name ?: "Unknown"`.

---

**Câu 7.** `sealed class` khác `enum class` ở điểm quan trọng nào?

- A. Sealed class chạy nhanh hơn enum
- B. Enum hỗ trợ kế thừa, sealed class thì không
- C. Mỗi subclass của sealed class có thể chứa data với kiểu khác nhau ✅
- D. Không có sự khác biệt, chỉ là cú pháp

> 💡 Enum: tất cả instance đều cùng kiểu. Sealed class: linh hoạt hơn, mỗi subclass là class riêng với data riêng. Ví dụ điển hình: `sealed class Result { data class Success<T>(val data: T); data class Error(val msg: String) }`.

---

**Câu 8.** Lập trình viên muốn lấy ra tất cả số chẵn từ một danh sách. Cách nào viết *idiomatic Kotlin* nhất?

- A. Dùng vòng lặp `for` và `if` để kiểm tra từng phần tử
- B. `list.filter { it % 2 == 0 }` ✅
- C. `list.map { it % 2 == 0 }`
- D. `list.reduce { acc, it -> acc + it }`

> 💡 `filter` trả về danh sách phần tử thỏa điều kiện. `map` biến đổi từng phần tử sang giá trị khác. `reduce` gộp thành một giá trị duy nhất. Kotlin khuyến khích dùng higher-order functions thay vì vòng lặp thủ công.

---

**Câu 9.** Tại sao Kotlin được coi là an toàn hơn Java trong việc xử lý `null`?

- A. Kotlin tự gán giá trị mặc định cho mọi biến, không bao giờ null
- B. Kotlin không có khái niệm null
- C. Kotlin phân biệt nullable và non-nullable ngay tại compile time, bắt lỗi trước khi chạy ✅
- D. Kotlin tự động bọc try-catch xung quanh mọi lần truy cập biến

> 💡 `NullPointerException` ("The Billion Dollar Mistake") là lỗi runtime phổ biến nhất Java. Kotlin đưa null-check vào type system – compiler từ chối code không an toàn ngay lúc build. Không có lỗi null nào "lọt" đến runtime nếu không dùng `!!`.

---

**Câu 10.** Trong Kotlin, `when` expression là phiên bản mạnh hơn của cấu trúc nào trong Java?

- A. `try-catch`
- B. `for` loop
- C. `switch-case` ✅
- D. `synchronized`

> 💡 `when` mạnh hơn `switch` ở chỗ: kiểm tra được range (`in 1..10`), kiểu dữ liệu (`is String`), và có thể dùng như expression để trả về giá trị (gán vào biến). Không cần `break` như Java.

---

## Chương 3 – Gemini in Android Studio *(10 câu)*

---

**Câu 1.** Trước khi được đổi tên thành "Gemini", AI Coding Assistant tích hợp sẵn trong Android Studio có tên là gì?

- A. Copilot
- B. Studio Bot ✅
- C. Bard
- D. CodeWhisperer

> 💡 Studio Bot ra mắt tại Google I/O 2023. Đầu năm 2024, Google đổi tên thành "Gemini" để thống nhất toàn bộ sản phẩm AI dưới thương hiệu Gemini. Studio Bot/Gemini được tích hợp sẵn, không cần cài plugin thêm.

---

**Câu 2.** Gemini sinh code dùng một Android API đã bị **deprecated** và không còn tồn tại. Hiện tượng AI "bịa" thông tin này gọi là gì?

- A. Stack Overflow
- B. Memory Leak
- C. Race Condition
- D. Hallucination ✅

> 💡 AI Hallucination là khi mô hình tạo ra thông tin sai lệch với vẻ ngoài tự tin. Với code, đây có thể là API không tồn tại, logic sai, hoặc deprecated method. **Đây là lý do developer phải luôn review kỹ code AI sinh ra.**

---

**Câu 3.** Ứng dụng crash và xuất hiện stack trace trong Logcat. Tính năng nào của Gemini phân tích nguyên nhân và đề xuất cách sửa?

- A. Code Completion
- B. Add Documentation
- C. Smart Debugging ✅
- D. Generate Code

> 💡 Smart Debugging: dán stack trace vào Gemini Chat → Gemini xác định file và dòng code gây lỗi, giải thích nguyên nhân và hướng dẫn sửa. Đặc biệt hữu ích cho developer mới khi gặp lỗi khó hiểu.

---

**Câu 4.** Developer A dùng prompt *"viết app Android"*, Developer B dùng prompt *"Generate a ViewModel using MVVM + Hilt + StateFlow, with sealed class Result for error handling"*. Ai nhận được kết quả tốt hơn?

- A. Developer A – prompt ngắn giúp AI sáng tạo hơn
- B. Developer B – prompt chi tiết cung cấp đủ context, AI sinh code đúng yêu cầu hơn ✅
- C. Kết quả như nhau vì Gemini tự hiểu context
- D. Cả hai đều sai vì Gemini không hỗ trợ MVVM

> 💡 Prompt tốt cần: (1) Rõ ràng về yêu cầu, (2) Cung cấp tech stack và pattern đang dùng, (3) Nêu ràng buộc. Prompt mơ hồ → AI phải "đoán" → kết quả không như ý.

---

**Câu 5.** Lập trình viên muốn hiểu nhanh đoạn code phức tạp mà đồng nghiệp viết. Tính năng nào của Gemini phù hợp nhất?

- A. Generate Code
- B. Code Completion
- C. Explain Code ✅
- D. Add Documentation

> 💡 "Explain Code": chọn đoạn code → chuột phải → Gemini → Explain. Gemini giải thích từng phần: mục đích, cách hoạt động, API được dùng, và các lưu ý quan trọng. Rất hữu ích khi làm việc với legacy code.

---

**Câu 6.** Tại sao developer KHÔNG nên paste **API key hoặc secret token** vào Gemini Chat?

- A. Gemini không thể đọc ký tự đặc biệt trong key
- B. Code và context được gửi lên server Google để xử lý – có nguy cơ lộ thông tin nhạy cảm ✅
- C. Gemini sẽ báo lỗi syntax khi gặp secret key
- D. Key sẽ bị tự động xóa khỏi prompt

> 💡 Gemini hoạt động bằng cách gửi context lên server Google. Mặc dù Google có chính sách bảo mật, **không bao giờ** paste secret key, token, hay password vào bất kỳ AI tool nào – đây là nguyên tắc bảo mật cơ bản.

---

**Câu 7.** Code Completion của Gemini khác với autocomplete thông thường của IDE ở điểm gì?

- A. Gemini chỉ gợi ý tên biến, không gợi ý logic
- B. Gemini hiểu ngữ cảnh toàn project, có thể gợi ý cả block code dựa trên logic đang viết ✅
- C. Gemini chỉ hỗ trợ Kotlin, không hỗ trợ Java
- D. Gemini chậm hơn nên ít được dùng

> 💡 Autocomplete thường dựa trên tên method/class. Gemini Code Completion hiểu context sâu hơn: biết bạn đang implement gì, project dùng pattern nào, và gợi ý cả function body hoàn chỉnh hoặc Composable phù hợp.

---

**Câu 8.** Developer muốn Gemini tự sinh **KDoc** (comment chuẩn Kotlin) cho một function. Tính năng nào phù hợp?

- A. Explain Code
- B. Generate Code
- C. Smart Debugging
- D. Add Documentation ✅

> 💡 "Add Documentation": chọn function/class → Gemini sinh KDoc gồm mô tả tổng quan, `@param` cho từng tham số, `@return` cho giá trị trả về. Tiết kiệm thời gian đáng kể khi cần viết doc cho codebase lớn.

---

**Câu 9.** Gemini in Android Studio yêu cầu điều kiện nào để hoạt động?

- A. Chỉ cần Android Studio phiên bản mới nhất
- B. Kết nối internet và đăng nhập bằng tài khoản Google ✅
- C. Cài thêm plugin riêng từ JetBrains Marketplace
- D. Tài khoản GitHub Enterprise

> 💡 Gemini là built-in feature từ Android Studio **Hedgehog (2023.1.1)** trở đi. Cần đăng nhập Google Account và có internet vì model AI chạy trên server của Google, không phải local. Không hoạt động offline.

---

**Câu 10.** Khi dùng Gemini để viết code, nguyên tắc quan trọng nhất lập trình viên cần ghi nhớ là gì?

- A. Dùng càng nhiều AI càng tốt để tiết kiệm thời gian tối đa
- B. Chỉ dùng AI khi bị stuck, không dùng chủ động
- C. Lập trình viên là người quyết định cuối cùng – phải hiểu và kiểm thử kỹ mọi code do AI sinh ra ✅
- D. Tin tưởng hoàn toàn vào AI vì AI ít sai hơn con người

> 💡 AI là công cụ hỗ trợ tăng tốc, **không phải thay thế tư duy**. Code AI sinh ra có thể chứa bug logic, security issue, hoặc dùng API sai/lỗi thời. Developer chịu trách nhiệm về mọi code đưa vào production – không có lý do nào để đổ lỗi cho AI.
