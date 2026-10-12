# Flutter Handoff – Food Ordering App KTX

> **Dự án:** Food Ordering App cho Sinh viên Ký túc xá ĐHQG-HCM (PRM323 – Lab 2)  
> **Người thực hiện:** Thành viên 4 – Trần Sanh Điền - Prototyping & Flutter Handoff Lead  
> **Tài liệu tham chiếu:** `ux/persona.md`, `ux/user-flow.md`, `design/DESIGN.md`, `food_ordering_app_srs.md` (Mục 3 & 4.A), và Figma Prototype (File chính key `84O0L9O6Z5TVkMjBvMRn33`, File phụ key `ALDYFWUZ72BaeyulpVi7uY`).  
> **Cam kết:** KHÔNG viết mã nguồn code hoàn chỉnh (tuân thủ quy định đề bài); đặc tả chi tiết cấu trúc Flutter Widget, thuộc tính chính, Design Tokens, ràng buộc tương tác và xử lý responsive để đội ngũ phát triển hiện thực hóa 100% giao diện không cần hỏi lại.

---

## 0. Quy ước chung (Technical Conventions)

1. **Chuẩn thiết kế & Nền tảng:**  
   - Framework: **Flutter 3.x**, ngôn ngữ **Dart**.
   - Design System: **Material Design 3 (M3)** với `useMaterial3: true` trong `ThemeData`.
   - Kích thước thiết kế chuẩn di động: **360 × 800 dp** (Android chuẩn phổ biến tại Việt Nam; lưu ý frame hiện tại trên Figma đang là 390dp/440dp).
2. **Đơn vị đo lường:**  
   - Khoảng cách, kích thước, bo góc, elevation: Đơn vị logic pixel **`dp`** (tương ứng `double` trong Flutter).
   - Kích thước chữ: Đơn vị scalable pixel **`sp`** (tự động co giãn theo cài đặt trợ năng hệ thống).
3. **Kiến trúc ThemeData & Tokens:**  
   - Toàn bộ màu sắc gọi qua `Theme.of(context).colorScheme.<tên_màu>` hoặc hằng số `AppColors.<tên_token>`. Tuyệt đối không hardcode mã Hex phân tán trong widget.
   - Toàn bộ kiểu chữ gọi qua `Theme.of(context).textTheme.<tên_style>`.
   - Khoảng cách padding/margin gọi qua hằng số `AppSpacing.<tên_token>`.
   - Bo góc viền gọi qua `AppRadius.<tên_token>`.

---

## 1. Bảng Token → Flutter

Bảng đối chiếu toàn diện mọi Design Token từ hệ thống thiết kế sang thuộc tính Flutter:

### 1.1. Color Tokens (Màu sắc)
| Token Name | Giá trị Hex | Thuộc tính Flutter tương ứng (M3) | Nguồn định nghĩa | Ghi chú & ⚠ Mâu thuẫn nguồn |
| :--- | :---: | :--- | :--- | :--- |
| `primary` | `#FF5722` | `ColorScheme.primary` | Figma Variables / DESIGN.md | Cam thương hiệu chính, nút CTA chính |

| `onPrimary` | `#FFFFFF` | `ColorScheme.onPrimary` | DESIGN.md §2.1 | Chữ trắng trên nền cam. ⚠ Tương phản 3.16:1 (cần dùng font chữ lớn/đậm để đạt chuẩn Large Text) |

| `primaryContainer` | `#FBE9E7` | `ColorScheme.primaryContainer` | DESIGN.md §2.1 | Nền chip, pill active Bottom Nav |

| `onPrimaryContainer` | `#E64A19` | `ColorScheme.onPrimaryContainer` | DESIGN.md §2.1 | Icon/Text trên nền Primary Container |

| `secondary` | `#FFA000` | `ColorScheme.secondary` | DESIGN.md §2.1 | Màu phụ hổ phách: Đánh giá sao ⭐, huy hiệu giảm giá |

| `secondaryContainer`| `#FFF8E1` | `ColorScheme.secondaryContainer` | DESIGN.md §2.1 | Nền voucher chip |

| `background` | `#FFFFFF` | `ColorScheme.background` / `surface` | Figma Variables | Nền chuẩn màn hình |

| `surfaceBg` | `#F8F9FA` | `ThemeData.scaffoldBackgroundColor` | DESIGN.md §2.1 | ⚠ Figma Variables chưa có token này, chỉ có `Background #FFFFFF` |

| `surfaceCard` | `#FFFFFF` | `ColorScheme.surface` | DESIGN.md §2.1 | Nền thẻ món ăn, card, dialog |

| `textPrimary` | `#111111` | `ColorScheme.onSurface` | Figma Variables | ⚠ DESIGN.md ghi `#1A1A1A`. Ưu tiên Figma `#111111` (tương phản 18.85:1) |

| `textSecondary` | `#757575` | `ColorScheme.onSurfaceVariant` | Figma Variables | ⚠ DESIGN.md ghi `#5F6368`. Ưu tiên Figma `#757575` (tương phản 4.61:1) |

| `textDisabled` | `#BDBDBD` | `ColorScheme.outlineVariant` | DESIGN.md §2.1 | Chữ nút vô hiệu hóa, món hết hàng |

| `error` | `#F44336` | `ColorScheme.error` | Figma Variables | ⚠ MÂU THUẪN: Variables là `#F44336` (tương phản 3.75:1, chưa đạt AA); DESIGN.md là `#D32F2F` (đạt 6.73:1). Khuyên dùng `#D32F2F` trong Flutter để đạt chuẩn Accessibility |

| `errorContainer` | `#FFEBEE` | `ColorScheme.errorContainer` | DESIGN.md 2.1 | Nền hộp thông báo lỗi, banner khiếu nại |

| `onErrorContainer` | `#D32F2F` | `ColorScheme.onErrorContainer` | DESIGN.md 2.1 | Chữ/Icon lỗi trên nền đỏ nhạt |

| `success` | `#2E7D32` | Hằng số `AppColors.success` | DESIGN.md 2.1 | Trạng thái giao thành công, đối soát hợp lệ |

| `successContainer` | `#E8F5E9` | Hằng số `AppColors.successContainer`| DESIGN.md 2.1 | Nền banner thành công, badge hợp lệ |

| `warning` | `#ED6C02` | Hằng số `AppColors.warning` | DESIGN.md 2.1 | Cảnh báo Cut-off time, đếm ngược |

| `warningContainer` | `#FFF3E0` | Hằng số `AppColors.warningContainer`| DESIGN.md 2.1 | Nền banner Cut-off time |

| `borderDefault` | `#E0E0E0` | `ColorScheme.outline` | DESIGN.md 2.1 | Đường viền ô nhập liệu, divider |

| `borderFocused` | `#FF5722` | Hằng số `AppColors.borderFocused` | DESIGN.md 2.1 | Viền ô input khi đang nhập liệu |

### 1.2. Typography Tokens (Kiểu chữ)
*Font family chuẩn: **Inter** (hoặc **Roboto** có sẵn trong hệ sinh thái Android/Flutter).*
| Typography Token | Size (sp) | Weight | Line Height | Ánh xạ Flutter `TextTheme` | Mục đích sử dụng |
| :--- | :---: | :--- | :---: | :--- | :--- |
| `headline-large` | 28sp | Bold (w700) | 34dp (1.2) | `textTheme.headlineLarge` | Tổng tiền thanh toán lớn (`S4`, `S5`) |

| `headline-medium`| 22sp | Bold (w700) | 28dp (1.27)| `textTheme.headlineMedium` | Tiêu đề App Bar chính, tiêu đề Dialog |

| `title-large` | 18sp | Semi-Bold (w600) | 24dp (1.33)| `textTheme.titleLarge` | Tên quán ăn, tiêu đề section |

| `title-medium` | 16sp | Semi-Bold (w600) | 22dp (1.38)| `textTheme.titleMedium` | Tên món ăn trên card, tên danh mục |

| `body-large` | 16sp | Regular (w400) | 24dp (1.5) | `textTheme.bodyLarge` | Nội dung mô tả chi tiết món ăn |

| `body-medium` | 14sp | Regular (w400) | 20dp (1.43)| `textTheme.bodyMedium` | Nhãn ô nhập liệu, mô tả phụ, đơn giá |

| `body-medium-bold`| 14sp| Semi-Bold (w600) | 20dp (1.43)| `textTheme.bodyMedium.copyWith(fontWeight: FontWeight.w600)` | Đơn giá món, tên tài xế trên thẻ `S6` |

| `label-large` | 15sp | Semi-Bold (w600) | 20dp (1.33)| `textTheme.labelLarge` | Chữ trên nút bấm (Buttons), Tab Bottom Nav |

| `label-small` | 12sp | Medium (w500) | 16dp (1.33)| `textTheme.labelSmall` | Badge giảm giá, chip đếm ngược |

| `caption` | 12sp | Regular (w400) | 16dp (1.33)| `textTheme.bodySmall` | Helper text ô nhập liệu, ghi chú chân trang |

### 1.3. Spacing Tokens (Khoảng cách & Padding)
| Token Name | Giá trị | Hằng số Flutter dự kiến | Nguồn | Ghi chú & ⚠ Mâu thuẫn nguồn |
| :--- | :---: | :--- | :--- | :--- |
| `spacing/4` | 4dp | `AppSpacing.xs = 4.0` | DESIGN.md | Khoảng cách icon và text phụ |
| `spacing/8` | 8dp | `AppSpacing.sm = 8.0` | Figma Variables / DESIGN.md | Gap giữa các phần tử nhỏ trong Auto Layout |
| `spacing/12` | 12dp | `AppSpacing.md = 12.0` | DESIGN.md | Khoảng cách giữa các cột grid |
| `spacing/16` | 16dp | `AppSpacing.base = 16.0` | Figma Variables / DESIGN.md | **Lề màn hình chuẩn (Screen Margin)**, padding card |
| `spacing/24` | 24dp | `AppSpacing.lg = 24.0` | DESIGN.md | Khoảng cách giữa các khối section |
| `spacing/32` | 32dp | `AppSpacing.xl = 32.0` | DESIGN.md | Padding đỉnh Modal Bottom Sheet |
| `spacing/48` | 48dp | `AppSpacing.xxl = 48.0` | DESIGN.md | **Chiều cao tối thiểu Touch Target** |

### 1.4. Border Radius Tokens (Bo góc)
| Token Name | Giá trị | Cấu hình Flutter dự kiến | Nguồn | Ghi chú & ⚠ Mâu thuẫn nguồn |
| :--- | :---: | :--- | :--- | :--- |
| `radius/sm` | 4dp | `BorderRadius.circular(4.0)` | DESIGN.md | Checkbox, badge mini |
| `radius/md` | 8dp | `BorderRadius.circular(8.0)` | Figma Variables / DESIGN.md | Ô nhập liệu (`TextFormField`), nút phụ nhỏ |
| `radius/lg` | 12dp | `BorderRadius.circular(12.0)` | Figma Variables / DESIGN.md | Thẻ món ăn (`Food Item Card`), khung ảnh |
| `radius/xl` | 16dp | `BorderRadius.circular(16.0)` | DESIGN.md | Hộp thoại (`AlertDialog`), Modal Bottom Sheet |
| `radius/full` | 999dp | `const StadiumBorder()` | DESIGN.md | Nút CTA dạng Pill, Avatar, Chip lọc |

### 1.5. Elevation & Shadow Tokens (Độ nổi)
| Token Name | Giá trị Shadow | Ánh xạ Flutter Elevation | Ứng dụng cụ thể |
| :--- | :--- | :---: | :--- |
| `elevation-0` | None | `0.0` | Scaffold background, Divider, Input flat |
| `elevation-1` | `0px 2px 6px rgba(0,0,0,0.06)` | `1.0` (M3) | Thẻ món ăn (`Card`), Banner nhẹ |
| `elevation-2` | `0px 4px 12px rgba(0,0,0,0.08)` | `2.0` (M3) | Sticky Header khi cuộn, Filter Chip bar |
| `elevation-3` | `0px 6px 16px rgba(0,0,0,0.12)` | `3.0` (M3) | `NavigationBar` chân trang, Thẻ shipper nổi |
| `elevation-4` | `0px 12px 28px rgba(0,0,0,0.18)`| `6.0` (M3) | `AlertDialog`, Modal `showModalBottomSheet` |

---

## 2. Bảng Component → Widget (C01–C09)

Bảng đối chiếu 9 bộ Master Component từ Figma sang Widget Flutter chuẩn Material 3:

| Mã | Tên Component | Tên trong Figma & Node ID | Variant hiện có trên Figma | Variant còn thiếu (⚠ CẦN BỔ SUNG) | Flutter Widget tương ứng | Thuộc tính chính cấu hình trong Flutter |
| :---: | :--- | :--- | :--- | :--- | :--- | :--- |
| **C01** | Button | `KTX/Button/Primary` (`111:8`) | `State=Default`, `Disabled` | `State=Pressed`, `Loading`; Biến thể `Type=Secondary`, `Outline`, `Danger` | **`FilledButton`** (chính), `OutlinedButton`, `ElevatedButton` | `style: FilledButton.styleFrom(backgroundColor: ColorScheme.primary, minimumSize: const Size(double.infinity, 48), shape: const StadiumBorder())` |

| **C02** | Text Field | `Crave/Text Field` (`84:25`) | `State=Default`, `Error` | `State=Focused`, `Filled`, `Disabled` | **`TextFormField`** | `decoration: InputDecoration(border: OutlineInputBorder(borderRadius: BorderRadius.circular(8)), contentPadding: const EdgeInsets.symmetric(horizontal: 16, vertical: 14))` |

| **C03** | Food Item Card | `Food Item Card` (`116:43`) | 1 trạng thái mặc định | Thiếu phân nhánh `Layout=Vertical` vs `Horizontal`; Thiếu `State=Available` vs `SoldOut` | **`Card`** hoặc `InkWell` + `Container` | `Card(elevation: 1, shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)), child: ...)` |

| **C04** | Bottom Navigation | `Crave/Bottom Navigation` (`87:152`) | `Active=Home`, `Explore`, `Orders`, `Profile` | Thiếu badge đếm số lượng cho tab Orders | 
**`NavigationBar`** (M3) | `NavigationBar(selectedIndex: currentIndex, destinations: const [NavigationDestination(icon: Icon(Icons.home), label: 'Trang chủ'), ...])` |

| **C05** | App Bar | `Crave/App Bar` (`90:26`) | 1 trạng thái tiêu đề chuẩn | Thiếu biến thể Home Header (kèm Dropdown chọn Cổng KTX), thiếu Header có Action gọi hotline | **`AppBar`** | `AppBar(title: Text(...), centerTitle: true, elevation: 0, leading: IconButton(icon: const Icon(Icons.arrow_back), onPressed: ...))` |

| **C06** | Dialog | `Dialog / Xác nhận giao hàng KTX` (`123:72`) | 1 trạng thái xác nhận giao nhận | ⚠ Thiếu Dialog "Đặt đơn thành công" `S5_Success` (chỉ có ở file phụ 192:2); thiếu Danger Dialog (Hủy đơn) | **`AlertDialog`** / `showModalBottomSheet` | `AlertDialog(shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(16)), title: ..., content: ..., actions: [FilledButton(...)])` |

| **C07** | Loading State | `KTXFood/Loading State` (`95:19`) | 1 trạng thái spinner toàn trang | Thiếu Shimmer Skeleton cho Card món ăn, thiếu Shimmer danh mục, thiếu Circular Overlay cho S5 | **`CircularProgressIndicator`** & gói `shimmer` | `CircularProgressIndicator(color: ColorScheme.primary)` hoặc `Shimmer.fromColors(baseColor: Colors.grey[300]!, highlightColor: Colors.grey[100]!)` |

| **C08** | Empty State | `Empty State / Giỏ hàng trống` (`131:16`)| 1 trạng thái giỏ hàng rỗng | Thiếu Empty state tìm kiếm không thấy món (`S1`), thiếu Empty state lịch sử trống (`S10`) | Custom **`Column`** Widget | `Column(mainAxisAlignment: MainAxisAlignment.center, children: [Icon(Icons.shopping_bag_outlined, size: 64), Text(...), FilledButton(...)])` |

| **C09** | Error State | `Crave/Error State` (`96:60`) | 1 trạng thái toàn màn hình mất mạng | Thiếu Inline Error Banner cho Form `S8`, thiếu Banner hết hạn Cut-off time ở `S1`/`S4` | Custom **`Container`** / `Card` Inline Alert | `Container(padding: const EdgeInsets.all(12), decoration: BoxDecoration(color: ColorScheme.errorContainer, borderRadius: BorderRadius.circular(8)), child: ...)` |

---

## 3. Đặc tả từng màn hình

### S1 – S1_FoodSearchHome (Tra cứu đặt đồ ăn)
* **3.1 Layout:**
  - `Scaffold` với nền `surfaceBg` (#F8F9FA).
  - Header: Custom `Container` (Home Header) chứa Avatar, Dropdown chọn cổng KTX ("Cổng KTX Khu A"), Icon Bell (`S12`), Icon Cart (`S4`).
  - Thân trang cuộn dọc (`SingleChildScrollView` hoặc `CustomScrollView` với `SliverList`):
    - Khối 1: Ô tìm kiếm (`Padding(16)`, `TextFormField` chiều cao 48dp).
    - Khối 2: Banner đếm ngược Cut-off time ca trưa (`Container` bo góc 12dp, nền `warningContainer`, đếm ngược đến 10:45).
    - Khối 3: Bộ lọc khu vực dạng ngang (`ListView.builder(scrollDirection: Axis.horizontal)`, các `FilterChip` lề 8dp).
    - Khối 4: Lưới món ăn nổi bật (`GridView.builder`, 2 cột, childAspectRatio: 0.75, spacing 12dp).
  - Chân trang: `NavigationBar` cố định (Active Tab Index = 0: Trang chủ).
* **3.2 Components:**
  - `C02 Text Field` (Tìm kiếm món).
  - `C03 Food Item Card` (Layout=Vertical, State=Available).
  - `C04 Bottom Navigation Bar` (Active=Home).
* **3.3 States:**
  - `default`: Hiển thị danh mục món và đồng hồ đếm ngược đang chạy.
  - `loading`: Khung Shimmer Skeleton hiển thị trong lúc gọi API danh sách món.
  - `empty`: Khi tìm kiếm từ khóa không có kết quả $\rightarrow$ hiển thị `C08 Empty State` ("Không tìm thấy món").
* **3.4 User interactions:**
  - Chạm Dropdown cổng KTX $\rightarrow$ Mở bottom sheet chọn Cổng Khu A / Cổng Khu B.
  - Gõ vào ô tìm kiếm $\rightarrow$ Lọc danh sách món theo từ khóa thời gian thực.
  - Chạm Chip khu vực $\rightarrow$ Lọc quán thuộc KTX Khu A, Khu B hoặc Làng ĐH.
  - Chạm vào Food Item Card $\rightarrow$ Điều hướng tới `S2_StoreDetailMenu`.
  - Chạm icon Giỏ hàng $\rightarrow$ Mở `S4_GroupCartCheckout`.
* **3.5 Navigation:**
  - Vào từ: Mở ứng dụng sau đăng nhập (`S0`), hoặc quay lại từ `S9` sau đánh giá.
  - Chạm thẻ món $\rightarrow$ `Navigator.push` sang `S2`.
  - Chạm Tab "Đơn hàng" trên Bottom Nav $\rightarrow$ `Navigator.pushReplacement` sang `S6`.
  - Chạm Tab "Lịch sử" $\rightarrow$ Chuyển sang `S10`. Nút Back trên Android $\rightarrow$ Thoát app hoặc hiện dialog thoát.
* **3.6 Important UI constraints:**
  - Touch target $\ge 48\times 48\text{dp}$ cho tất cả icon header và card.
  - Bàn phím: Tự động ẩn bàn phím (`FocusScope.of(context).unfocus()`) khi cuộn danh sách món.
  - Tên món trên Card cắt dòng bằng `TextOverflow.ellipsis`, tối đa 2 dòng.

---

### S2 – S2_StoreDetailMenu (Chi tiết Quán ăn & Thực đơn)
* **3.1 Layout:**
  - `Scaffold` với `CustomScrollView` (Sliver AppBar):
    - `SliverAppBar` mở rộng (cao 200dp) chứa ảnh bìa quán, co lại thành 56dp khi cuộn, có nút Back và nút Tim yêu thích.
    - `SliverToBoxAdapter`: Thông tin quán (Tên quán, số sao, cự ly, bảng tin thông báo từ chủ quán).
    - `SliverPersistentHeader`: Thanh tab phân loại danh mục món (Cơm, Bún, Nước) bám dính đỉnh (Sticky).
    - `SliverList`: Danh sách món ăn bố trí theo chiều dọc (Horizontal Cards).
  - Chân trang nổi: Floating Cart Bar (`Container` bo góc 16dp, lề 16dp, nền cam `primary`, hiển thị tổng tiền và nút xem giỏ).
* **3.2 Components:**
  - `C05 App Bar` (Detail Style có Back button và Favorite action).
  - `C03 Food Item Card` (Layout=Horizontal, State=Available / SoldOut).
  - `C01 Button` (Floating Action Bar xem giỏ).
* **3.3 States:**
  - `populated`: Danh sách món đầy đủ.
  - `soldOut`: Món hết hàng hiển thị lớp phủ mờ xám kèm nhãn "Hết hàng ca này", nút thêm bị disable.
* **3.4 User interactions:**
  - Bấm nút Tim $\rightarrow$ Đổi trạng thái icon thành đỏ/cam (đã lưu vào `S11`).
  - Bấm nút `+ Thêm` trên thẻ món $\rightarrow$ Kích hoạt mở Modal `S3_FoodCustomization`.
  - Bấm Floating Cart Bar $\rightarrow$ Điều hướng mở `S4_GroupCartCheckout`.
* **3.5 Navigation:**
  - Vào từ: `S1_FoodSearchHome` hoặc `S11_FavoriteList`.
  - Bấm Back $\rightarrow$ Quay lại `S1`.
  - Bấm `+ Thêm` $\rightarrow$ Mở `S3` (Modal Bottom Sheet).
  - Bấm Giỏ hàng $\rightarrow$ `Navigator.push` sang `S4`.
* **3.6 Important UI constraints:**
  - Nút Back và nút Tim phải bọc trong `Container` tròn có nền mờ nhẹ để đọc rõ trên ảnh bìa quán.
  - Touch target $\ge 48\text{dp}$. Ảnh thumbnail món cố định $80\times 80\text{dp}$.

---

### S3 – S3_FoodCustomization (Tùy biến món ăn)
* **3.1 Layout:**
  - Cấu trúc: `showModalBottomSheet` với `isScrollControlled: true`.
  - Container bo góc trên `radius-xl` (16dp), nền trắng `#FFFFFF`.
  - Chiều cao chiếm tối đa 85% màn hình, có Handle Bar kéo vuốt ở đỉnh.
  - Thân modal: `ListView` cuộn dọc:
    - Ảnh lớn món ăn (tỉ lệ 16:9), Tên món, Đơn giá cơ sở.
    - Nhóm 1: Chọn Size (`RadioListTile` - Size Vừa / Size Lớn).
    - Nhóm 2: Mức cay (`RadioListTile` - Không cay / Vừa / Nhiều).
    - Nhóm 3: Topping thêm (`CheckboxListTile` - Trứng ốp la, Chả thêm, Canh).
    - Nhóm 4: Ghi chú (`TextFormField` nhiều dòng, maxLines: 3).
    - Nhóm 5: Bộ đếm số lượng (`Row` chứa nút `-`, Text số lượng, nút `+`).
  - Đáy modal: Cố định nút CTA `FilledButton` ("Thêm vào giỏ - [Tổng tiền]đ").
* **3.2 Components:**
  - `C02 Text Field` (Ghi chú khẩu vị).
  - `C01 Button` (CTA Thêm vào giỏ hàng).
* **3.3 States:**
  - `default`: Size Vừa được chọn mặc định, số lượng = 1.
  - `interactive`: Khi người dùng tích thêm topping, tổng giá trên nút CTA tự động cộng dồn theo thời gian thực.
* **3.4 User interactions:**
  - Chạm chọn radio/checkbox $\rightarrow$ Cập nhật state và tính lại tổng tiền.
  - Chạm `-` / `+` $\rightarrow$ Tăng giảm số lượng (tối thiểu là 1).
  - Nhập văn bản ghi chú (tối đa 100 ký tự).
  - Chạm nút CTA $\rightarrow$ Đóng modal, phát event thêm vào giỏ hàng.
* **3.5 Navigation:**
  - Vào từ: `S2_StoreDetailMenu` khi bấm `+ Thêm`.
  - Chạm nút CTA hoặc vuốt modal xuống $\rightarrow$ `Navigator.pop(context)` quay lại `S2`.
* **3.6 Important UI constraints:**
  - Bàn phím: Bọc trong `Padding(EdgeInsets.only(bottom: MediaQuery.of(context).viewInsets.bottom))` để nút CTA và ô ghi chú không bị bàn phím che khuất.
  - Touch target mỗi tùy chọn $\ge 48\text{dp}$.

---

### S4 – S4_GroupCartCheckout (Giỏ hàng & Thanh toán gom đơn)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` tiêu đề "Giỏ hàng & Thanh toán".
  - Thân trang: `ListView` cuộn dọc với padding 16dp:
    - Section 1: Điểm nhận cố định (`RadioListTile` chọn Cổng Khu A / Cổng Khu B).
    - Section 2: Ca nhận gom đơn (`RadioListTile` chọn Ca trưa 11h30 / Ca tối 18h00 kèm banner Cut-off).
    - Section 3: Danh sách món trong giỏ (mỗi món là 1 item kèm bộ đếm số lượng và nút xóa).
    - Section 4: Nhập mã voucher (`Row` gồm `TextFormField` + `OutlinedButton` "Áp dụng").
    - Section 5: Phương thức thanh toán (`RadioListTile` chọn VietQR / COD).
    - Section 6: Bảng tính tiền (`Column` tạm tính, phí ship gom 0đ, giảm giá, Tổng cộng `headline-large`).
  - Đáy màn hình: Khung cố định (Sticky Bottom) chứa nút thanh toán 48dp.
* **3.2 Components:**
  - `C05 App Bar` (Detail Header kèm Back).
  - `C02 Text Field` (Nhập mã giảm giá).
  - `C01 Button` (Nút Áp dụng, Nút Thanh toán / Xác nhận).
  - `C08 Empty State` (khi giỏ hàng = 0 món).
* **3.3 States:**
  - `populated`: Giỏ có món, cho phép chọn cổng và phương thức thanh toán.
  - `empty`: Khi xóa hết món $\rightarrow$ hiển thị `C08 Empty State` kèm nút "Khám phá món" quay về `S1`.
  - `voucherApplied`: Hiển thị dòng giảm giá màu xanh lá và cập nhật lại tổng tiền.
* **3.4 User interactions:**
  - Thay đổi số lượng món hoặc bấm xóa món.
  - Nhập mã voucher $\rightarrow$ Bấm Áp dụng (kiểm tra hợp lệ).
  - Chọn phương thức thanh toán: Nếu chọn VietQR, nhãn nút đáy đổi thành "Tiến hành thanh toán"; nếu chọn COD, nhãn nút đổi thành "Xác nhận đặt đơn".
* **3.5 Navigation:**
  - Vào từ: `S2` hoặc icon Giỏ hàng ở `S1`; hoặc quay lại từ `S5` (nhánh đổi sang COD).
  - Bấm Back $\rightarrow$ Quay lại `S2`.
  - Bấm nút đáy khi chọn VietQR $\rightarrow$ `Navigator.push` sang `S5_OnlinePayment`.
  - Bấm nút đáy khi chọn COD $\rightarrow$ Mở Dialog `S5_Success`.
* **3.6 Important UI constraints:**
  - Validation: Bắt buộc phải chọn Cổng KTX và Ca nhận trước khi bấm thanh toán.
  - Tổng tiền thanh toán hiển thị font `headline-large` (28sp Bold) nổi bật.

---

### S5 – S5_OnlinePayment (Thanh toán online VietQR)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` tiêu đề "Thanh toán VietQR".
  - Thân trang cuộn dọc (`SingleChildScrollView`, padding 16dp):
    - Khung tóm tắt đơn: Mã đơn `#KTX-8492`, Tổng tiền cần chuyển (`headline-large` màu cam).
    - Khung hiển thị mã VietQR động chính giữa màn hình (kích thước $220\times 220\text{dp}$, bo góc 12dp).
    - Nút phụ: `OutlinedButton.icon` "Tải mã QR về máy".
    - Bảng thông tin thụ hưởng: Tên chủ quán, Ngân hàng, Số tài khoản (kèm icon `IconButton` sao chép nhanh), Cú pháp chuyển khoản.
    - Đồng hồ đếm ngược phiên thanh toán (10:00 phút).
    - Nút liên kết chuyển đổi: `TextButton` "Gặp sự cố chuyển khoản? Đổi sang Tiền mặt (COD)".
  - Chân trang: Sticky `FilledButton` 48dp "Đã hoàn tất chuyển khoản".
* **3.2 Components:**
  - `C05 App Bar` (Detail Header kèm Back).
  - `C01 Button` (CTA Hoàn tất chuyển khoản, Nút phụ tải QR, Nút đổi COD).
  - `C07 Loading State` (Overlay spinner khi kiểm tra giao dịch).
* **3.3 States:**
  - `default`: Đang hiển thị mã VietQR và đồng hồ đếm ngược.
  - `loading`: Hiển thị `CircularProgressIndicator` overlay khi bấm "Đã hoàn tất chuyển khoản" để đối soát.
* **3.4 User interactions:**
  - Bấm icon sao chép STK / Cú pháp $\rightarrow$ Copy vào clipboard, hiện `SnackBar` thông báo "Đã sao chép".
  - Bấm "Đổi sang Tiền mặt (COD)" $\rightarrow$ Quay lại `S4` và tự động chọn radio COD.
  - Bấm "Đã hoàn tất chuyển khoản" $\rightarrow$ Kích hoạt loading kiểm tra và mở Dialog `S5_Success`.
* **3.5 Navigation:**
  - Vào từ: `S4_GroupCartCheckout` khi chọn VietQR.
  - Bấm Back hoặc Đổi sang COD $\rightarrow$ `Navigator.pop(context)` quay lại `S4`.
  - Thanh toán thành công $\rightarrow$ Hiển thị Dialog `S5_Success`.
* **3.6 Important UI constraints:**
  - Mã QR phải có padding viền trắng $\ge 16\text{dp}$ để camera quét không bị lỗi viền.
  - Đồng hồ đếm ngược khi về 00:00 sẽ báo hết hạn phiên giao dịch.

---

### S5_Success – S5_OrderSuccessDialog (Dialog Xác nhận Đặt hàng thành công)
* **3.1 Layout:**
  - `AlertDialog` hoặc Pop-up Modal canh giữa màn hình trên nền tối phủ mờ `rgba(0,0,0,0.5)`.
  - Khung dialog bo góc `radius-xl` (16dp), nền trắng `#FFFFFF`, padding 24dp.
  - Bố cục theo chiều dọc (`Column`, `mainAxisSize: MainAxisSize.min`):
    - Icon minh họa checkmark tròn thành công màu xanh lá (kích thước 64dp).
    - Tiêu đề: "Đặt đơn ca trưa thành công!" (`headlineMedium`, 20sp Bold, canh giữa).
    - Nội dung: `Text` mô tả mã đơn `#KTX-8492`, nhắc nhở có mặt tại Cổng KTX Khu A lúc 11:30.
    - Nút CTA: `FilledButton` chiều cao 48dp "Theo dõi đơn hàng ngay".
* **3.2 Components:**
  - `C06 Dialog` *(⚠ Lưu ý: Trên file phụ node 192:2, chưa có Master Component trong file chính)*.
  - `C01 Button` (FilledButton CTA).
* **3.3 States:**
  - `default`: Hiển thị thông báo đặt đơn thành công và mã đơn hàng.
* **3.4 User interactions:**
  - Chạm nút "Theo dõi đơn hàng ngay" $\rightarrow$ Đóng dialog và chuyển trang sang `S6`.
  - Không cho phép đóng dialog khi chạm ra vùng ngoài màn hình (`barrierDismissible: false`).
* **3.5 Navigation:**
  - Vào từ: `S5_OnlinePayment` (sau khi chuyển khoản xong) HOẶC từ `S4_GroupCartCheckout` (sau khi đặt COD).
  - Bấm nút CTA $\rightarrow$ `Navigator.pushAndRemoveUntil` tới `S6_LiveOrderTracking` (xóa sạch stack giỏ hàng/thanh toán).
* **3.6 Important UI constraints:**
  - Bắt buộc `barrierDismissible: false` để buộc người dùng chủ động bấm xác nhận.
  - Nút bấm full width trong dialog, chiều cao $\ge 48\text{dp}$.

---

### S6 – S6_LiveOrderTracking (Theo dõi Đơn hàng thời gian thực)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` hiển thị mã đơn `#KTX-8492` và icon gọi Hotline hỗ trợ.
  - Thân trang cuộn dọc (`SingleChildScrollView`, padding 16dp):
    - Section 1: Bộ đếm thời gian shipper tới cổng ("Dự kiến tới cổng KTX trong: 12 phút").
    - Section 2: Thanh tiến trình Stepper (4 bước: `Đã nhận đơn` $\rightarrow$ `Đang nấu` $\rightarrow$ `Đang gom chuyến` $\rightarrow$ `Đã tới cổng KTX`).
    - Section 3: Thẻ thông tin shipper (`Card` bo góc 12dp gồm Avatar, Tên, Biển số xe, Vị trí đón tại cổng KTX, nút gọi điện nhanh).
    - Section 4: Danh sách tóm tắt các món trong bọc đơn hàng.
    - Section 5: Nút "Hủy đơn hàng" (bị disabled nếu quán đã bấm nấu).
    - Section 6: Nút liên kết "Báo cáo sự cố đơn hàng" (mở `S8`).
  - Chân trang: Sticky Bottom Bar chứa nút CTA lớn: "Mở Mã QR Nhận Hàng" (48dp).
* **3.2 Components:**
  - `C05 App Bar` (Live Tracking Style).
  - `C01 Button` (CTA Mở mã QR, Nút Hủy đơn).
  - `C04 Bottom Navigation Bar` (Active Tab Index = 1: Đơn hàng).
* **3.3 States:**
  - `cooking`: Trạng thái đang nấu, nút hủy đơn bị mờ vô hiệu hóa.
  - `arrived`: Shipper đã đến cổng $\rightarrow$ Nút "Mở Mã QR Nhận Hàng" đổi sang màu cam nổi bật và nhấp nháy báo hiệu.
  - `disputed`: Trạng thái đơn đổi thành "Đang chờ xử lý hoàn tiền" (sau khi gửi khiếu nại ở `S8`).
* **3.4 User interactions:**
  - Chạm nút gọi điện trên thẻ shipper $\rightarrow$ Gọi tới số điện thoại tài xế qua `url_launcher`.
  - Chạm nút "Mở Mã QR Nhận Hàng" $\rightarrow$ Mở Modal `S7_PickupQRCode`.
  - Chạm liên kết "Báo cáo sự cố đơn hàng" $\rightarrow$ Điều hướng tới `S8_DisputeRefund`.
* **3.5 Navigation:**
  - Vào từ: `S5_Success` sau đặt hàng, hoặc Tab "Đơn hàng" trên Bottom Nav, hoặc từ `S10`, hoặc từ Push Notification.
  - Bấm nút Mở mã QR $\rightarrow$ Mở `S7`.
  - Bấm Báo cáo sự cố $\rightarrow$ Chuyển tới `S8`.
  - Bấm Back $\rightarrow$ Quay về Trang chủ `S1`.
* **3.6 Important UI constraints:**
  - Nút Mở QR phải luôn neo cố định ở chân màn hình để thao tác một chạm nhanh nhất khi vừa xuống tới cổng KTX.
  - Touch target nút gọi điện $\ge 48\times 48\text{dp}$.

---

### S7 – S7_PickupQRCode (Mã QR Nhận hàng tại Cổng KTX)
* **3.1 Layout:**
  - Modal Bottom Sheet hoặc Full-screen Overlay trên nền trắng tương phản cao.
  - Thanh tiêu đề có nút Đóng `(X)` ở góc trên bên phải.
  - Thân modal bố trí canh giữa:
    - Tiêu đề: "Đưa mã cho tài xế quét tại Cổng KTX".
    - Khung viền chứa Mã QR kích thước lớn ($200\times 200\text{dp}$) nền trắng, viền rõ nét.
    - **Vùng đối soát thủ công nổi bật dưới QR:** `Container` nền xám nhạt bo góc 8dp, hiển thị dòng chữ cỡ lớn `title-large`: **"Đuôi SĐT: •••• 2947"** (để đọc đối soát khi chói nắng).
    - Tóm tắt mã đơn `#KTX-8492` và số lượng hộp cơm trong túi.
    - Hướng dẫn ngắn gọn: "Nếu camera tài xế chói nắng không quét được, vui lòng đọc 4 số cuối SĐT ở trên."
  - Chân modal: Nút CTA `FilledButton` "Đã nhận được thức ăn" (chiều cao 48dp).
* **3.2 Components:**
  - `C01 Button` (CTA Đã nhận thức ăn).
  - Custom QR Display Widget (dùng thư viện `qr_flutter`).
* **3.3 States:**
  - `default`: Hiển thị QR và 4 số cuối SĐT.
* **3.4 User interactions:**
  - Đưa màn hình cho shipper quét QR.
  - Đọc 4 số cuối SĐT nếu shipper yêu cầu đối soát thủ công.
  - Chạm nút "Đã nhận được thức ăn" (hoặc tự động kích hoạt qua Socket/Push khi tài xế bấm giao xong) $\rightarrow$ Điều hướng sang `S9_ReviewFeedback`.
* **3.5 Navigation:**
  - Vào từ: `S6_LiveOrderTracking` khi bấm "Mở Mã QR Nhận Hàng".
  - Chạm nút Đóng `(X)` $\rightarrow$ Quay lại `S6`.
  - Chạm "Đã nhận được thức ăn" $\rightarrow$ `Navigator.pushReplacement` sang `S9_ReviewFeedback`.
* **3.6 Important UI constraints:**
  - Độ sáng màn hình: Tự động kích hoạt độ sáng tối đa khi mở màn hình này (giúp quét ngoài trời nắng).
  - Tương phản tuyệt đối: Mã QR đen trên nền trắng tinh khiết, 4 số cuối SĐT hiển thị với kích thước $\ge 18\text{sp}$ Semi-Bold.

---

### S8 – S8_DisputeRefund (Khiếu nại và hoàn tiền)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` tiêu đề "Khiếu nại & Hoàn tiền".
  - Thân trang cuộn dọc (`ListView`, padding 16dp):
    - Khung tóm tắt đơn hàng lỗi: Mã đơn `#KTX-8492`, Tên quán.
    - Section 1: Chọn nguyên nhân sự cố (`CheckboxListTile` chọn nhiều: Đổ vỡ thức ăn, Thiếu món, Sai vị, Chất lượng kém).
    - Section 2: Chọn món ăn bị ảnh hưởng (`Row` nút "Chọn tất cả" + danh sách các món kèm checkbox chọn từng món).
    - Section 3: Hộp hiển thị số tiền yêu cầu hoàn (`Container` viền cam, hiển thị tổng tiền tự động tính).
    - Section 4: Tải ảnh bằng chứng (`Wrap` các ô thumbnail ảnh đã chụp + nút thêm ảnh `+` viền đứt nét).
    - Section 5: Mô tả chi tiết (`TextFormField` nhiều dòng).
    - Section 6: Chọn kênh nhận hoàn tiền (`RadioListTile` chọn: Ví KTX Food / Chuyển khoản ngân hàng. Nếu chọn Ngân hàng, mở thêm các trường nhập Tên ngân hàng, STK, Tên chủ thẻ).
  - Chân trang: Sticky `FilledButton` 48dp "Gửi yêu cầu khiếu nại".
* **3.2 Components:**
  - `C05 App Bar` (Detail Header).
  - `C02 Text Field` (Mô tả sự cố, Nhập thông tin ngân hàng).
  - `C01 Button` (CTA Gửi khiếu nại, Nút Chọn tất cả).
  - `C09 Error State` (Inline alert cảnh báo khi thiếu ảnh bằng chứng).
* **3.3 States:**
  - `default`: Chưa chọn món và sự cố.
  - `calculating`: Số tiền hoàn tự động cập nhật khi tích chọn thêm món.
  - `submitting`: Nút CTA hiển thị spinner trong lúc tải ảnh lên hệ thống.
* **3.4 User interactions:**
  - Tích chọn một hoặc nhiều sự cố.
  - Bấm "Chọn tất cả" để chọn nhanh toàn bộ món bị hư hỏng.
  - Bấm tải ảnh $\rightarrow$ Mở Camera hoặc Thư viện ảnh thiết bị qua `image_picker`.
  - Chọn kênh hoàn tiền (Ví KTX Food hoặc Ngân hàng).
  - Bấm "Gửi yêu cầu khiếu nại" $\rightarrow$ Validate form.
* **3.5 Navigation:**
  - Vào từ: `S6_LiveOrderTracking` hoặc `S10_OrderHistory`.
  - Bấm Back $\rightarrow$ Quay lại màn hình trước.
  - Gửi thành công $\rightarrow$ Hiển thị màn hình thành công (node `192:19` file phụ) rồi trở về `S6`/`S10` với trạng thái "Đang chờ xử lý hoàn tiền".
* **3.6 Important UI constraints:**
  - Validation: Bắt buộc chọn ít nhất 1 sự cố, ít nhất 1 món ăn, tải ít nhất 1 ảnh bằng chứng thực tế; nếu chọn ngân hàng thì bắt buộc nhập đủ STK.
  - Chữ báo lỗi dưới ô input phải dùng mã màu `#D32F2F` (tương phản $\ge 4.5:1$).

---

### S9 – S9_ReviewFeedback (Đánh giá và phản hồi)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` tiêu đề "Đánh giá đơn hàng" và nút "Bỏ qua" ở góc phải.
  - Thân trang cuộn dọc (`ListView`, padding 16dp):
    - Section 1 - Đánh giá Quán ăn:
      - Tên quán, logo quán.
      - Thanh đánh giá 5 sao ⭐ tương tác (`RatingBar` lớn, chạm để chọn số sao).
      - Hàng Filter Chip nhận xét nhanh ("Món ngon", "Đóng gói kỹ", "Đúng khẩu vị").
      - `TextFormField` nhập nhận xét chi tiết cho quán.
    - Section 2 - Đánh giá Shipper:
      - Tên và avatar shipper KTX.
      - Thanh đánh giá 5 sao ⭐ riêng cho shipper.
      - Chip nhận xét nhanh ("Giao đúng giờ", "Thân thiện", "Bảo quản tốt").
      - `TextFormField` góp ý riêng cho tài xế.
  - Chân trang: Sticky `FilledButton` 48dp "Gửi đánh giá".
* **3.2 Components:**
  - `C05 App Bar` (có nút Bỏ qua).
  - `C02 Text Field` (Nhận xét quán và shipper).
  - `C01 Button` (CTA Gửi đánh giá).
* **3.3 States:**
  - `default`: Cả 2 đối tượng mặc định 5 sao ⭐.
* **3.4 User interactions:**
  - Chạm chọn số sao (từ 1 đến 5 sao) cho từng đối tượng riêng biệt.
  - Chạm các chip nhận xét nhanh để tự động điền gợi ý.
  - Gõ văn bản nhận xét tự do.
  - Chạm nút "Gửi đánh giá" $\rightarrow$ Gửi lên hệ thống, hiển thị thông báo cảm ơn.
* **3.5 Navigation:**
  - Vào từ: `S7_PickupQRCode` sau khi nhận hàng xong; hoặc từ nút Đánh giá trong `S10_OrderHistory`.
  - Chạm "Bỏ qua" hoặc "Gửi đánh giá" $\rightarrow$ `Navigator.pushAndRemoveUntil` trở về Trang chủ `S1_FoodSearchHome`.
* **3.6 Important UI constraints:**
  - Icon sao đánh giá có kích thước tối thiểu $36\times 36\text{dp}$, vùng chạm $48\times 48\text{dp}$ để tránh bấm trượt sao.
  - Bàn phím tự động đẩy giao diện lên trên khi gõ nhận xét.

---

### S10 – S10_OrderHistory (Lịch sử đơn hàng)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` tiêu đề "Lịch sử đơn hàng".
  - Dưới AppBar: Thanh phân loại trạng thái Segmented Tabs cố định (`TabBar`: "Tất cả", "Đang xử lý", "Hoàn tất", "Đã hủy").
  - Thân trang: `TabBarView` chứa các danh sách thẻ đơn hàng cũ (`ListView.separated`, padding 16dp):
    - Mỗi item là 1 `Card` đơn hàng:
      - Dòng đỉnh: Mã đơn `#KTX-...`, ngày giờ đặt, tên quán.
      - Badge trạng thái: "Đã giao thành công" (Xanh), "Đang hoàn tiền" (Cam), "Đã hủy" (Xám).
      - Dòng giữa: Danh sách món tóm tắt, tổng số tiền thanh toán (`body-medium-bold`).
      - Dòng đáy: Hàng nút tương tác:
        - Nút `Secondary Button` "Đặt lại đơn này".
        - Nút `Outlined/Danger Button` "Khiếu nại / Hoàn tiền" (cho đơn vừa giao có sự cố).
  - Chân trang: `NavigationBar` cố định (Active Tab Index = 2: Orders / Lịch sử).
* **3.2 Components:**
  - `C05 App Bar` (Standard Title).
  - `C01 Button` (Secondary "Đặt lại đơn", Outline/Danger "Khiếu nại").
  - `C04 Bottom Navigation Bar` (Active=Orders).
  - `C08 Empty State` (khi chưa có lịch sử đơn hàng nào).
* **3.3 States:**
  - `populated`: Danh sách các đơn hàng cũ.
  - `empty`: Khi tab không có đơn nào $\rightarrow$ Hiển thị `C08 Empty State` ("Chưa có đơn hàng nào trong mục này").
* **3.4 User interactions:**
  - Chuyển tab lọc trạng thái đơn hàng.
  - Bấm vào thân thẻ đơn $\rightarrow$ Mở chi tiết tiến trình đơn (`S6`).
  - Bấm nút "Đặt lại đơn này" $\rightarrow$ Đẩy nguyên vẹn các món vào giỏ hàng và mở `S4`.
  - Bấm nút "Khiếu nại / Hoàn tiền" $\rightarrow$ Mở form `S8_DisputeRefund`.
* **3.5 Navigation:**
  - Vào từ: Tab "Lịch sử" trên Bottom Navigation Bar từ bất kỳ màn hình nào.
  - Bấm "Đặt lại đơn này" $\rightarrow$ `Navigator.push` sang `S4_GroupCartCheckout`.
  - Bấm "Khiếu nại / Hoàn tiền" $\rightarrow$ `Navigator.push` sang `S8_DisputeRefund`.
  - Bấm vào đơn đang giao $\rightarrow$ Chuyển tới `S6_LiveOrderTracking`.
* **3.6 Important UI constraints:**
  - Các nút hành động trên mỗi thẻ đơn phải có khoảng cách gap $\ge 8\text{dp}$, chiều cao $\ge 40\text{dp}$ (vùng chạm vật lý $\ge 48\text{dp}$).
  - Hỗ trợ thao tác kéo để làm mới danh sách (`RefreshIndicator`).

---

## 4. Hành vi màn hình rộng (≥600dp) áp dụng chung

Để đảm bảo ứng dụng hiển thị thẩm mỹ trên máy tính bảng (Tablet) hoặc màn hình điện thoại gập (Foldables):

1. **Giới hạn độ rộng tối đa nội dung (Max Content Width Constraint):**
   - Toàn bộ nội dung thân trang (`Scaffold body`) được bọc trong widget `Center` với ràng buộc `ConstrainedBox(constraints: BoxConstraints(maxWidth: 600))`.
   - Vùng viền hai bên màn hình vượt quá 600dp sẽ hiển thị màu nền nền trung tính `surfaceBg` (#F8F9FA).
2. **Chuyển đổi Lưới hiển thị (Grid Layout Adaptation):**
   - Danh sách món ăn tại `S1`: Chuyển từ lưới 2 cột (ở 360dp) sang lưới **3 hoặc 4 cột** (ở $\ge 600\text{dp}$) với `crossAxisCount: 3` hoặc `4`.
3. **Chuyển đổi Thanh điều hướng (Navigation Rail):**
   - Khi chiều rộng màn hình $\ge 600\text{dp}$, thanh điều hướng chân trang `NavigationBar` được chuyển đổi thành thanh điều hướng bên hông `NavigationRail` neo bên trái màn hình.
4. **Hộp thoại & Modal Bottom Sheet:**
   - Các `AlertDialog` và `showModalBottomSheet` được khống chế chiều rộng tối đa `maxWidth: 480dp`, luôn canh giữa màn hình thay vì kéo giãn toàn bộ bề ngang máy tính bảng.

---

## 5. Ngoài phạm vi flow (S0, S11, S12, S13)

Các màn hình dưới đây thuộc kiến trúc hệ thống nhưng không nằm trong 3 User Flows cốt lõi, được liệt kê để đội ngũ phát triển lưu ý kiến trúc:

| Mã | Tên màn hình | Vị trí trong hệ thống | Flutter Widget dự kiến | Lý do ngoài phạm vi flow |
| :---: | :--- | :--- | :--- | :--- |
| **S0** | `S0_StudentLogin` | Điểm vào ứng dụng (Auth) | `Scaffold` + `TextFormField` SĐT/Mật khẩu + OTP | Xác thực định danh tiền đề, không thuộc chu trình đặt món |
| **S11** | `S11_FavoriteList` | Tab Quán quen trên Bottom Nav | `Scaffold` + `ListView` thẻ quán quen | Lối tắt xem menu, Flow 1 đã chuẩn hóa xuất phát từ `S1` |
| **S12** | `S12_NotificationBoard`| Icon Chuông trên Header | `Scaffold` + `ListView` thông báo | Kênh nhận tin thụ động; Flow 2 mở trực tiếp từ `S6`/Push |
| **S13** | `S13_ProfileSettings` | Tab Tài khoản trên Bottom Nav | `Scaffold` + `ListView` cài đặt hồ sơ KTX | Thiết lập tài khoản cá nhân, không thuộc luồng giao dịch |

---