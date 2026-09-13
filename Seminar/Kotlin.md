# CHƯƠNG 2. NGÔN NGỮ KOTLIN TRONG ANDROID DEVELOPMENT

---

## 2.1. Tổng quan về Kotlin

### Kotlin là gì?

Kotlin là ngôn ngữ lập trình **hiện đại, đa nền tảng, kiểu tĩnh (statically typed)** được phát triển bởi **JetBrains** – công ty đứng sau IntelliJ IDEA. Kotlin chạy trên **JVM (Java Virtual Machine)**, có thể biên dịch sang JavaScript và native code.

### Lịch sử và mục đích phát triển

- **2010**: JetBrains bắt đầu phát triển Kotlin để khắc phục nhược điểm của Java.
- **2016**: Kotlin 1.0 chính thức ra mắt.
- **2017**: Google chính thức hỗ trợ Kotlin như ngôn ngữ **first-class** cho Android.
- **2019**: Google tuyên bố **Kotlin-first** – ưu tiên Kotlin trong toàn bộ tài liệu và thư viện Android.

### Đặc điểm nổi bật

- Cú pháp ngắn gọn, rõ ràng, giảm boilerplate code đáng kể so với Java.
- **Null Safety** được tích hợp sẵn vào hệ thống kiểu dữ liệu.
- **100% tương thích với Java** – có thể dùng lẫn lộn Java và Kotlin trong cùng một project.
- Hỗ trợ **lập trình hàm (Functional Programming)** và **lập trình hướng đối tượng (OOP)**.

### Mối quan hệ giữa Kotlin, JVM và Android

```
Kotlin Source (.kt)
       ↓ Kotlin Compiler
  Bytecode (.class)
       ↓ D8/R8
  DEX Bytecode (.dex)
       ↓ Android Runtime (ART)
  Native Machine Code → Chạy trên thiết bị Android
```

---

## 2.2. Cú pháp và các thành phần cơ bản của Kotlin

### Biến và hằng số

```kotlin
var count: Int = 10       // Biến có thể thay đổi
val name: String = "Android"  // Hằng số, không thể reassign
val pi = 3.14             // Type Inference: tự suy kiểu Double
```

### Kiểu dữ liệu cơ bản

| Kiểu | Mô tả | Ví dụ |
|------|-------|-------|
| `Int` | Số nguyên 32-bit | `42` |
| `Long` | Số nguyên 64-bit | `1_000_000L` |
| `Double` | Số thực 64-bit | `3.14` |
| `Float` | Số thực 32-bit | `3.14f` |
| `Boolean` | Đúng/Sai | `true`, `false` |
| `String` | Chuỗi ký tự | `"Hello"` |
| `Char` | Ký tự đơn | `'A'` |

### Câu điều kiện

```kotlin
// if-else biểu thức (expression)
val max = if (a > b) a else b

// when (thay thế switch-case)
when (score) {
    in 90..100 -> println("Xuất sắc")
    in 70..89  -> println("Khá")
    in 50..69  -> println("Trung bình")
    else       -> println("Yếu")
}
```

### Vòng lặp

```kotlin
for (i in 1..5) println(i)          // 1 2 3 4 5
for (i in 5 downTo 1 step 2) ...    // 5 3 1
while (condition) { ... }
```

### Function

```kotlin
// Hàm thông thường
fun greet(name: String): String {
    return "Hello, $name!"
}

// Single-expression function
fun add(a: Int, b: Int) = a + b

// Default parameter
fun log(message: String, tag: String = "DEBUG") { ... }
```

### Collection

```kotlin
val list = listOf(1, 2, 3)              // Immutable
val mutableList = mutableListOf(1, 2, 3) // Mutable
val map = mapOf("key" to "value")
val set = setOf(1, 2, 3)
```

---

## 2.3. Lập trình hướng đối tượng với Kotlin

### Class và Object

```kotlin
class Car(val brand: String, var speed: Int = 0) {
    fun accelerate(amount: Int) {
        speed += amount
    }
}

val car = Car("Toyota", 0)
car.accelerate(60)
println(car.speed) // 60
```

### Kế thừa (Inheritance)

```kotlin
open class Animal(val name: String) {
    open fun sound() = println("...")
}

class Dog(name: String) : Animal(name) {
    override fun sound() = println("Woof!")
}
```

### Interface

```kotlin
interface Drivable {
    fun drive()
    fun stop() = println("Stopped") // Default implementation
}

class Truck : Drivable {
    override fun drive() = println("Truck is driving")
}
```

### Data Class

Tự động sinh `equals()`, `hashCode()`, `toString()`, `copy()`:

```kotlin
data class User(val id: Int, val name: String, val email: String)

val user1 = User(1, "An", "an@example.com")
val user2 = user1.copy(name = "Binh")
```

### Enum và Sealed Class

```kotlin
// Enum
enum class Status { LOADING, SUCCESS, ERROR }

// Sealed Class – linh hoạt hơn Enum, cho phép mỗi subclass có data riêng
sealed class Result<out T> {
    data class Success<T>(val data: T) : Result<T>()
    data class Error(val message: String) : Result<Nothing>()
    object Loading : Result<Nothing>()
}
```

---

## 2.4. Các đặc trưng nổi bật của Kotlin

### Null Safety

Kotlin phân biệt rõ kiểu có thể `null` và không thể `null` ngay ở compile time:

```kotlin
var nonNull: String = "Hello"
// nonNull = null  // ❌ Lỗi compile

var nullable: String? = "Hello"
nullable = null  // ✅ OK

// Safe call operator
val length = nullable?.length  // Trả về null nếu nullable là null

// Elvis operator
val len = nullable?.length ?: 0  // Trả về 0 nếu null

// Non-null assertion (dùng cẩn thận!)
val len2 = nullable!!.length  // Ném NullPointerException nếu null
```

### Extension Function

Thêm hàm mới vào class có sẵn mà không cần kế thừa:

```kotlin
fun String.isPalindrome(): Boolean = this == this.reversed()

println("racecar".isPalindrome()) // true
```

### Lambda và Higher-order Function

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

val evens = numbers.filter { it % 2 == 0 }  // [2, 4]
val doubled = numbers.map { it * 2 }         // [2, 4, 6, 8, 10]
val sum = numbers.reduce { acc, n -> acc + n } // 15
```

### Scope Functions

Cho phép thực thi một block code trong ngữ cảnh của một object:

| Function | Context Object | Return Value | Dùng khi |
|----------|---------------|-------------|---------|
| `let` | `it` | Kết quả lambda | Null check, chuyển đổi |
| `run` | `this` | Kết quả lambda | Tính toán, khởi tạo |
| `with` | `this` | Kết quả lambda | Gọi nhiều hàm trên object |
| `apply` | `this` | Object | Cấu hình object |
| `also` | `it` | Object | Side effects |

```kotlin
val user = User().apply {
    name = "An"
    email = "an@example.com"
}
```

### Coroutines và Xử lý bất đồng bộ

```kotlin
// Thay vì callback hell, Kotlin Coroutines cho phép viết code bất đồng bộ theo phong cách tuần tự
viewModelScope.launch {
    val data = repository.fetchData()  // Suspend function – không block main thread
    _uiState.value = UiState.Success(data)
}
```

---

## 2.5. Java vs Kotlin trong Android Development

### So sánh theo các tiêu chí

| Tiêu chí | Java | Kotlin |
|---------|------|--------|
| **Cú pháp** | Verbose, nhiều boilerplate | Ngắn gọn, rõ ràng |
| **Null Safety** | Không có (NullPointerException thường xuyên) | Tích hợp sẵn vào type system |
| **Boilerplate** | Nhiều (getter/setter, constructor,...) | Ít hơn rất nhiều (data class, properties) |
| **Functional Programming** | Hỗ trợ hạn chế (Java 8+) | Hỗ trợ đầy đủ (lambda, HOF, extension) |
| **Async Programming** | Thread, AsyncTask (deprecated), RxJava | Coroutines (đơn giản, hiệu quả, native) |
| **Extension Functions** | Không có | Có |
| **Data Classes** | Phải tự viết (hoặc dùng Lombok) | Tích hợp sẵn |
| **Java Interop** | — | 100% tương thích |
| **Hiệu năng** | Tương đương | Tương đương (có thể tốt hơn với inline) |
| **Learning Curve** | Dễ bắt đầu hơn | Dễ nếu đã biết Java |
| **Hỗ trợ Android** | Tốt (legacy) | **Kotlin-first** từ 2019 |

### Kết luận

- **Ưu điểm Java**: Cộng đồng lớn, nhiều tài liệu cũ, dễ học ban đầu.
- **Nhược điểm Java**: Verbose, thiếu null safety, async phức tạp.
- **Ưu điểm Kotlin**: Ngắn gọn, an toàn, hiện đại, được Google ưu tiên.
- **Nhược điểm Kotlin**: Cần làm quen nếu chưa biết, compile time có thể chậm hơn Java đôi chút.
- **Lý do Kotlin được ưu tiên**: Kotlin giảm thiểu lỗi phổ biến (NullPointerException), tăng năng suất lập trình và được Google đầu tư mạnh vào hệ sinh thái (Jetpack, Compose đều Kotlin-first).

---

## 2.6. Kotlin trong một ứng dụng Android

### Kotlin với Activity

```kotlin
class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        binding.btnGreet.setOnClickListener {
            binding.tvMessage.text = "Xin chào, Android!"
        }
    }
}
```

### Kotlin với ViewModel và StateFlow

```kotlin
class UserViewModel : ViewModel() {
    private val _uiState = MutableStateFlow<UiState>(UiState.Loading)
    val uiState: StateFlow<UiState> = _uiState.asStateFlow()

    fun loadUser(id: Int) {
        viewModelScope.launch {
            _uiState.value = UiState.Loading
            val user = repository.getUser(id)
            _uiState.value = UiState.Success(user)
        }
    }
}
```

### Kotlin với Jetpack Compose

```kotlin
@Composable
fun UserCard(user: User) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp)
    ) {
        Column(modifier = Modifier.padding(16.dp)) {
            Text(text = user.name, style = MaterialTheme.typography.headlineSmall)
            Text(text = user.email, style = MaterialTheme.typography.bodyMedium)
        }
    }
}
```

### Vai trò của Kotlin trong kiến trúc Android hiện đại

Kotlin là nền tảng của toàn bộ kiến trúc MVVM (Model-View-ViewModel) phổ biến trong Android:

```
View (Compose / XML)
    ↕ StateFlow / LiveData
ViewModel (Kotlin + Coroutines)
    ↕ suspend functions
Repository
    ↕ 
Data Sources (Room, Retrofit, DataStore)
```
