# So sánh Java và Kotlin trong lập trình Android

Năm 2017, Google công bố hỗ trợ Kotlin hạng nhất (First-class) trên Android. Đến năm 2019, Google chính thức tuyên bố Android là hệ sinh thái **"Kotlin-first"**. Điều này có nghĩa là các API mới, các thư viện Jetpack đều được ưu tiên phát triển cho Kotlin trước.

Mặc dù môn học sử dụng Java làm ngôn ngữ nền tảng (rất tốt để hiểu bản chất), việc nắm bắt Kotlin là điều bắt buộc nếu bạn muốn làm dự án thực tế.

## 1. Tại sao Google lại chọn Kotlin?

- **Tính ngắn gọn (Conciseness):** Kotlin giúp giảm đáng kể lượng mã boilerplate code (code rập khuôn, lặp đi lặp lại) so với Java (có thể giảm tới 40% số dòng code).
- **An toàn (Safety):** Tính năng "Null Safety" được tích hợp sẵn vào Type System của Kotlin, giúp loại bỏ triệt để lỗi `NullPointerException` - lỗi phổ biến nhất gây crash app trên Java.
- **Khả năng tương tác (Interoperability):** Kotlin và Java có thể gọi lẫn nhau một cách hoàn hảo trong cùng một project. Bạn có thể thêm file Kotlin vào project Java cũ mà không gặp vấn đề gì.
- **Hỗ trợ Coroutines:** Xử lý đa luồng (Multi-threading) bất đồng bộ trong Java thường phức tạp (dùng RxJava hoặc AsyncTask đã bị deprecated). Kotlin Coroutines giúp viết code bất đồng bộ tuần tự, dễ đọc và cực kỳ tối ưu về mặt tài nguyên.

## 2. Các điểm khác biệt cơ bản về Cú pháp

### 2.1. Khai báo biến
- **Java:** Bắt buộc khai báo kiểu dữ liệu.
  ```java
  String name = "Tuan";
  final int age = 25; // Hằng số
  ```
- **Kotlin:** Sử dụng `var` (biến thay đổi được) và `val` (hằng số, giống `final`). Kotlin có Type Inference (tự suy luận kiểu dữ liệu).
  ```kotlin
  var name = "Tuan"
  val age = 25 
  ```

### 2.2. Null Safety
- **Java:** Bất kỳ Object nào cũng có thể là `null`. Phải check `if (obj != null)` liên tục.
- **Kotlin:** Biến mặc định **không được phép** chứa `null`. Nếu muốn cho phép `null`, phải thêm dấu `?`.
  ```kotlin
  var name: String = "Tuan"
  // name = null // LỖI COMPILER

  var nullableName: String? = "Tuan"
  nullableName = null // Hợp lệ
  ```

### 2.3. Data Classes (Lớp mô hình dữ liệu)
Khi định nghĩa một object (POJO) để parse JSON.
- **Java:** Phải tự viết Getter, Setter, `equals()`, `hashCode()`, `toString()`. Thường dài hàng chục dòng.
- **Kotlin:** Chỉ cần 1 dòng duy nhất với từ khóa `data class`. Compiler sẽ tự sinh ra mọi hàm cần thiết.
  ```kotlin
  data class User(val id: Int, val name: String, val email: String)
  ```

### 2.4. Extensions Functions (Hàm mở rộng)
- **Java:** Nếu muốn thêm chức năng cho một class có sẵn (ví dụ `String`), bạn phải tạo một class `StringUtils` với các hàm `static`.
- **Kotlin:** Cho phép "gắn" thêm hàm vào một class có sẵn mà không cần kế thừa nó.
  ```kotlin
  // Thêm hàm toTitleCase() cho class String
  fun String.toTitleCase(): String {
      return this.substring(0, 1).toUpperCase() + this.substring(1)
  }
  
  // Sử dụng
  val name = "tuan".toTitleCase() // Trả về "Tuan"
  ```

### 2.5. Smart Casts
- **Java:** Sau khi check `instanceof`, vẫn phải ép kiểu (cast) lại bằng tay.
  ```java
  if (obj instanceof String) {
      String s = (String) obj;
      System.out.println(s.length());
  }
  ```
- **Kotlin:** Compiler đủ thông minh để tự ép kiểu.
  ```kotlin
  if (obj is String) {
      println(obj.length) // obj tự động được coi là String
  }
  ```

## 3. Tổng kết

Việc sử dụng Kotlin cho phần Client của dự án Capstone (thay vì Java) là một quyết định rất hợp lý và thực tế. Nó sẽ giúp bạn:
1. Phát triển UI và Logic nhanh hơn.
2. Dễ dàng sử dụng các thư viện Networking hiện đại của Android (như Retrofit với Coroutines).
3. Đảm bảo ứng dụng ổn định hơn nhờ Null Safety.
