# 📱 Giải Thích Chi Tiết — HorizontalScrollView Demo

---

## 🗂️ Tổng Quan Cấu Trúc Project

```
app/src/main/
│
├── java/.../MainActivity.java        ← Logic chính (Java)
├── res/
│   ├── layout/
│   │   ├── activity_main.xml         ← Layout màn hình chính
│   │   └── frame_icon_caption.xml    ← Layout 1 ô ảnh trong scroll
│   └── drawable/
│       ├── small_*.xml               ← Ảnh thumbnail (nhỏ, dùng trong scroll)
│       └── large_*.xml               ← Ảnh lớn (hiển thị khi click)
```

---

## 📄 1. activity_main.xml — Layout Màn Hình Chính

```xml
<LinearLayout
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="#ffffffff"
    android:padding="2dp">
```

> **LinearLayout vertical** = xếp các thành phần con từ **trên xuống dưới** theo chiều dọc.
> - `match_parent` → chiều rộng bằng màn hình.
> - `wrap_content` → chiều cao vừa đủ với nội dung bên trong.
> - `padding="2dp"` → lề bên trong 2dp cho tất cả 4 cạnh.

---

### 📌 Thành phần 1: TextView (thanh thông báo)

```xml
<TextView
    android:id="@+id/txtMsg"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="#ff00ff00"
    android:text="scroll and click to select ..."
    android:textAppearance="?android:attr/textAppearanceLarge" />
```

| Thuộc tính | Ý nghĩa |
|---|---|
| `android:id="@+id/txtMsg"` | Đặt ID để Java tìm được view này qua `findViewById()` |
| `background="#ff00ff00"` | Nền màu xanh lá `#ff00ff00` (ARGB: Alpha=ff, R=00, G=ff, B=00) |
| `textAppearance="?android:attr/textAppearanceLarge"` | Dùng style chữ lớn mặc định của hệ thống |

> 💡 **Mục đích:** Hiển thị thông báo khi người dùng click vào ảnh, ví dụ: *"Selected position: 2 Photo-3"*

---

### 📌 Thành phần 2: HorizontalScrollView (thanh cuộn ngang)

```xml
<HorizontalScrollView
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="#44aaaaaa">

    <LinearLayout
        android:id="@+id/viewgroup"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:padding="10dip" />

</HorizontalScrollView>
```

> ⚠️ **Quy tắc quan trọng:** `HorizontalScrollView` **chỉ được chứa đúng 1 view con trực tiếp**. View con đó phải là một **layout** để chứa nhiều phần tử bên trong.

**Giải thích từng phần:**

| Phần | Giải thích |
|---|---|
| `HorizontalScrollView` | Container cho phép cuộn **ngang**. Chính nó không chứa ảnh trực tiếp. |
| `LinearLayout` bên trong | View con duy nhất của HorizontalScrollView. Orientation `horizontal` → các ảnh xếp ngang nhau. |
| `android:id="@+id/viewgroup"` | ID để Java tìm được LinearLayout này, sau đó thêm ảnh vào động (dynamically). |
| `background="#44aaaaaa"` | Nền xám mờ (`44` là alpha = khoảng 27% opacity). |
| `padding="10dip"` | `dip` = `dp`, khoảng cách lề bên trong 10dp. |

---

### 📌 Thành phần 3: ImageView (ảnh lớn)

```xml
<ImageView
    android:id="@+id/imageSelected"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_weight="2" />
```

> Hiển thị ảnh chất lượng cao khi người dùng click vào một ô trong scroll. Ban đầu trống, sẽ được set ảnh bằng Java.

---

## 📄 2. frame_icon_caption.xml — Layout Một Ô Ảnh

File này định nghĩa **khuôn mẫu (template)** cho mỗi ô trong HorizontalScrollView.

```xml
<LinearLayout
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:padding="2dp">

    <ImageView
        android:id="@+id/icon"
        android:layout_width="100dp"
        android:layout_height="80dp"
        android:scaleType="fitXY"
        android:src="@mipmap/ic_launcher" />

    <TextView
        android:id="@+id/caption"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:background="#33ffff00"
        android:textSize="20sp"
        android:gravity="center" />

</LinearLayout>
```

**Giải thích chi tiết:**

| Thuộc tính | Ý nghĩa |
|---|---|
| `orientation="vertical"` | Icon ở trên, caption ở dưới |
| `ImageView` width/height = `100dp` / `80dp` | Kích thước cố định cho ảnh thumbnail |
| `scaleType="fitXY"` | Co/giãn ảnh vừa đúng với khung `100×80dp`, **không giữ tỉ lệ** |
| `android:src="@mipmap/ic_launcher"` | Ảnh mặc định khi layout được tạo (Java sẽ thay thế sau) |
| `TextView` width = `100dp` | Cùng chiều rộng với ảnh để caption căn chỉnh đẹp |
| `background="#33ffff00"` | Nền vàng mờ (`33` = alpha ~20%) |
| `android:gravity="center"` | Căn giữa chữ trong TextView |
| `textSize="20sp"` | `sp` = scale-independent pixels, tự động scale theo cỡ chữ hệ thống |

> 💡 **Tại sao cần file riêng?** Vì Java sẽ **tạo ra nhiều ô** từ template này bằng cách `inflate` (thổi phồng) file XML thành View object trong bộ nhớ.

---

## 📄 3. MainActivity.java — Logic Chính

### 3.1 Khai Báo Biến Toàn Cục

```java
public class MainActivity extends Activity {

    TextView txtMsg;          // Thanh thông báo trên cùng
    ViewGroup scrollViewgroup; // LinearLayout bên trong HorizontalScrollView
    ImageView icon;            // Ảnh thumbnail trong mỗi frame (dùng tạm)
    TextView caption;          // Caption trong mỗi frame (dùng tạm)
    ImageView imageSelected;   // Ảnh lớn bên dưới
```

> `extends Activity` → kế thừa từ `Activity` (chuẩn Android cũ, không dùng AppCompatActivity).
>
> `ViewGroup` → là lớp cha của tất cả layout (LinearLayout, ConstraintLayout, ...). Dùng kiểu này vì ta chỉ cần gọi `addView()` để thêm view con.

---

### 3.2 Mảng Dữ Liệu

```java
// Tên caption cho 26 ảnh
String[] items = {
    "Photo-1", "Photo-2", ..., "Photo-26"
};

// ID resource của ảnh nhỏ (thumbnail)
Integer[] thumbnails = {
    R.drawable.small_blossom_918453_1280,
    R.drawable.small_building_922529_1280,
    ...
};

// ID resource của ảnh lớn
Integer[] largeImages = {
    R.drawable.large_blossom_918453_1280,
    R.drawable.large_building_922529_1280,
    ...
};
```

> `R.drawable.ten_anh` → Android tự động sinh ra class `R` khi build. Nó ánh xạ tên file drawable → số nguyên (int/Integer) dùng làm ID.
>
> ⚠️ Ba mảng `items`, `thumbnails`, `largeImages` phải có **cùng số phần tử** và **cùng thứ tự**, vì cùng dùng chung chỉ số `i`.

---

### 3.3 onCreate() — Khởi Động Activity

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main); // Gán layout XML cho Activity
```

> `@Override` → ghi đè phương thức của lớp cha `Activity`.
>
> `super.onCreate(savedInstanceState)` → **bắt buộc** phải gọi trước, để lớp cha khởi tạo Activity.
>
> `setContentView(R.layout.activity_main)` → nạp file XML `activity_main.xml` làm giao diện.

---

### 3.4 Bind View — Liên Kết XML với Java

```java
txtMsg        = (TextView)  findViewById(R.id.txtMsg);
imageSelected = (ImageView) findViewById(R.id.imageSelected);
scrollViewgroup = (ViewGroup) findViewById(R.id.viewgroup);
```

> `findViewById(R.id.xxx)` → tìm view trong layout hiện tại theo ID.
>
> `(TextView)`, `(ImageView)`, `(ViewGroup)` → **ép kiểu (cast)**, vì `findViewById` trả về kiểu `View` chung chung. Ta phải ép sang đúng kiểu để dùng các method đặc thù.

---

### 3.5 Vòng Lặp — Tạo Frames Động

Đây là phần **quan trọng nhất** của bài:

```java
for (int i = 0; i < items.length; i++) {
```
> Lặp từ `i = 0` đến `i = 25` (26 lần), mỗi lần tạo 1 ô ảnh.

---

#### Bước 1: Inflate — "Thổi phồng" XML thành View

```java
final View singleFrame = getLayoutInflater().inflate(R.layout.frame_icon_caption, null);
```

> - `getLayoutInflater()` → lấy đối tượng `LayoutInflater` từ Activity.
> - `.inflate(R.layout.frame_icon_caption, null)` → đọc file XML `frame_icon_caption.xml` và **tạo ra một View object trong bộ nhớ** (chưa hiển thị lên màn hình).
> - Tham số `null` = không có ViewGroup cha (vì sẽ add vào sau).
> - `final` → biến `singleFrame` không thay đổi tham chiếu, cần thiết để dùng trong **anonymous class** (OnClickListener bên dưới).

**Mỗi vòng lặp tạo ra 1 bản sao độc lập** từ template XML. 26 vòng = 26 frame riêng biệt.

---

#### Bước 2: Đặt ID cho Frame

```java
singleFrame.setId(i);
```

> Gán ID cho frame là chỉ số `i` (0, 1, 2, ..., 25).
> Sau này khi click, ta gọi `singleFrame.getId()` để biết đây là frame thứ mấy → tra cứu đúng ảnh lớn.

---

#### Bước 3: Tìm View Con Bên Trong Frame

```java
TextView caption = (TextView) singleFrame.findViewById(R.id.caption);
ImageView icon   = (ImageView) singleFrame.findViewById(R.id.icon);
```

> `singleFrame.findViewById(...)` → tìm view **bên trong** frame vừa inflate (không phải toàn layout).
> Đây là lý do ta gọi `singleFrame.find...` chứ không gọi `this.find...` hay `Activity.find...`.

---

#### Bước 4: Đổ Dữ Liệu vào Frame

```java
icon.setImageResource(thumbnails[i]);   // Gán ảnh thumbnail
caption.setText(items[i]);              // Gán tên "Photo-1", "Photo-2"...
caption.setBackgroundColor(Color.YELLOW); // Nền caption màu vàng
```

> - `thumbnails[i]` → lấy phần tử thứ `i` trong mảng thumbnails.
> - `Color.YELLOW` → hằng số màu vàng trong Android (= `0xFFFFFF00`).

---

#### Bước 5: Thêm Frame vào ScrollView

```java
scrollViewgroup.addView(singleFrame);
```

> `addView()` → thêm `singleFrame` vào `LinearLayout` bên trong `HorizontalScrollView`.
> Sau lệnh này, frame mới hiển thị trong danh sách ngang.

---

#### Bước 6: Gán Click Listener cho Frame

```java
singleFrame.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        txtMsg.setText("Selected position: " + singleFrame.getId() + " " + items[singleFrame.getId()]);
        showLargeImage(singleFrame.getId());
    }
});
```

> - `new View.OnClickListener() { ... }` → tạo **anonymous class** (lớp vô danh) implement interface `OnClickListener`.
> - `@Override public void onClick(View v)` → phương thức được gọi khi người dùng nhấn vào frame.
> - `singleFrame.getId()` → trả về chỉ số `i` đã set ở Bước 2.
> - Dùng `singleFrame.getId()` (không dùng `i` trực tiếp) vì khi vòng lặp kết thúc, biến `i` không còn tồn tại; nhưng `singleFrame` là `final` nên vẫn còn.

---

### 3.6 showLargeImage() — Hiển Thị Ảnh Lớn

```java
protected void showLargeImage(int frameId) {
    Drawable selectedLargeImage = getResources().getDrawable(largeImages[frameId], getTheme());
    imageSelected.setBackground(selectedLargeImage);
}
```

> - `getResources().getDrawable(id, theme)` → lấy resource drawable từ ID với theme hiện tại. **API 21+** (Android 5.0 trở lên).
> - `largeImages[frameId]` → lấy ID ảnh lớn tương ứng với frame đã click.
> - `imageSelected.setBackground(...)` → đặt ảnh làm **background** của ImageView (không phải `setImageDrawable`).

---

## 🔄 Luồng Chạy Toàn Bộ

```
App khởi động
    │
    ▼
onCreate() chạy
    │
    ├── setContentView()  → nạp activity_main.xml
    ├── findViewById()    → bind txtMsg, imageSelected, scrollViewgroup
    │
    └── for (i = 0..25)
            │
            ├── inflate(frame_icon_caption.xml) → tạo 1 View mới
            ├── setId(i)                        → gán số thứ tự
            ├── find icon, caption bên trong
            ├── setImageResource(thumbnails[i]) → đặt ảnh nhỏ
            ├── setText(items[i])               → đặt caption
            ├── addView(singleFrame)            → thêm vào HorizontalScrollView
            └── setOnClickListener              → đăng ký sự kiện click
                        │
                        ▼
                    onClick() (khi user nhấn)
                        │
                        ├── txtMsg.setText("Selected position: X Photo-X")
                        └── showLargeImage(X)
                                │
                                └── imageSelected.setBackground(large_X)
```

---

## 🧩 Tổng Hợp Khái Niệm Quan Trọng

| Khái niệm | Giải thích ngắn |
|---|---|
| `HorizontalScrollView` | Widget cuộn ngang, **chỉ nhận 1 view con trực tiếp** |
| `LayoutInflater.inflate()` | Chuyển file XML → View object trong bộ nhớ |
| `ViewGroup.addView()` | Thêm view con vào layout tại runtime (không phải lúc build) |
| `setId(i)` | Gán định danh số cho view để tra cứu sau |
| `View.OnClickListener` | Interface xử lý sự kiện click, dùng anonymous class |
| `final` variable | Biến không thay đổi tham chiếu, cần thiết để dùng trong inner class |
| `R.drawable.xxx` | Tham chiếu đến file drawable trong `res/drawable/` |
| `getResources().getDrawable()` | Lấy Drawable object từ resource ID (API 21+) |
| `dp` / `sp` | `dp` = mật độ độc lập cho kích thước view; `sp` = `dp` + scale theo cỡ chữ |
| `ARGB` màu (`#44aaaaaa`) | 2 ký tự đầu = alpha (độ trong suốt), 6 ký tự sau = màu RGB |
