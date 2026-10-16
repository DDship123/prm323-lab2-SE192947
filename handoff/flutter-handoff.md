# Flutter Handoff – Food Ordering App KTX

> **Dự án:** Food Ordering App cho Sinh viên Ký túc xá ĐHQG-HCM (PRM323 – Lab 2)  
> **Người thực hiện:** Thành viên 4 – Trần Sanh Điền - Prototyping & Flutter Handoff Lead  
> **Nguồn thiết kế duy nhất:** Figma Design File `Lab 2 - Food Ordering App` (fileKey: `ALDYFWUZ72BaeyulpVi7uY`, Page: `Prototype`).  
> **Tài liệu tham chiếu:** `ux/persona.md`, `ux/user-flow.md`, `design/DESIGN.md`, `design/screen-spec.md`, `food_ordering_app_srs.md` (Mục 3 & 4.A).  
> **Cam kết chuyên môn:** KHÔNG viết mã nguồn code hoàn chỉnh (tuân thủ quy định đề bài); đặc tả chi tiết cấu trúc Flutter Widget, thuộc tính chính, Design Tokens, ràng buộc tương tác và xử lý responsive để đội ngũ phát triển hiện thực hóa 100% giao diện không cần hỏi lại.

---

## 0. Quy ước chung (Technical Conventions)

1. **Chuẩn thiết kế & Nền tảng:**  
   - Framework: **Flutter 3.x**, ngôn ngữ **Dart**.
   - Design System: **Material Design 3 (M3)** với `useMaterial3: true` trong `ThemeData`.
   - Kích thước viewport thiết bị chuẩn di động: **360 × 800 dp** (Android chuẩn phổ biến tại Việt Nam).
   - Chiều cao các frame trên Figma hiện tại: **360dp bề rộng** và chiều cao linh hoạt từ **1074dp đến 2822dp** (thể hiện toàn bộ nội dung cuộn bên dưới viewport; trong Flutter sử dụng `SingleChildScrollView` hoặc `CustomScrollView` với `Slivers`).
2. **Đơn vị đo lường:**  
   - Khoảng cách, kích thước, bo góc, elevation: Đơn vị logic pixel **`dp`** (tương ứng kiểu dữ liệu `double` trong Flutter).
   - Kích thước chữ: Đơn vị scalable pixel **`sp`** (tự động co giãn theo cài đặt trợ năng hệ thống).
3. **Kiến trúc ThemeData & Tokens:**  
   - Toàn bộ màu sắc gọi qua `Theme.of(context).colorScheme.<tên_màu>` hoặc hằng số `AppColors.<tên_token>`. Tuyệt đối không hardcode mã Hex phân tán trong widget.
   - Toàn bộ kiểu chữ gọi qua `Theme.of(context).textTheme.<tên_style>`.
   - Khoảng cách padding/margin gọi qua hằng số `AppSpacing.<tên_token>`.
   - Bán kính bo góc gọi qua hằng số `AppRadius.<tên_token>` hoặc `BorderRadius.circular(...)`.

---

## 1. Bản đồ Tokens sang Flutter (Design Token Mapping)

### 1.1. Color Tokens (Màu sắc)

| Token Name | Giá trị Hex | Thuộc tính Flutter tương ứng (M3) | Nguồn định nghĩa | Ghi chú & Đối soát Accessibility |
| :--- | :---: | :--- | :--- | :--- |
| `primary` | `#FF5722` | `ColorScheme.primary` | Figma Variables / DESIGN.md | Cam thương hiệu chính, nút CTA chính |
| `onPrimary` | `#FFFFFF` | `ColorScheme.onPrimary` | DESIGN.md §2.1 | Chữ trắng trên nền cam. ⚠ Tương phản 3.16:1 (cần dùng font chữ lớn/đậm Bold/Semi-Bold để đạt chuẩn Large Text) |
| `primaryContainer` | `#FBE9E7` | `ColorScheme.primaryContainer` | DESIGN.md §2.1 | Nền chip, pill active Bottom Nav |
| `onPrimaryContainer`| `#E64A19`| `ColorScheme.onPrimaryContainer` | DESIGN.md §2.1 | Icon/Text trên nền Primary Container |
| `secondary` | `#FFA000` | `ColorScheme.secondary` | DESIGN.md §2.1 | Màu phụ hổ phách: Đánh giá sao ⭐, huy hiệu giảm giá |
| `secondaryContainer`| `#FFF8E1`| `ColorScheme.secondaryContainer`| DESIGN.md §2.1 | Nền voucher chip |
| `background` | `#FFFFFF` | `ColorScheme.background` | Figma Variables | Nền chuẩn màn hình |
| `surfaceBg` | `#F9FAFB` | `ThemeData.scaffoldBackgroundColor`| Figma Prototype | Nền Scaffold toàn màn hình |
| `surfaceCard` | `#FFFFFF` | `ColorScheme.surface` | Figma Prototype | Nền thẻ món ăn, card, dialog |
| `textPrimary` | `#111827` | `ColorScheme.onSurface` | Figma Prototype | Màu chữ tiêu đề chính (tương phản 16.08:1) |
| `textSecondary` | `#6B7280` | `ColorScheme.onSurfaceVariant` | Figma Prototype | Màu chữ mô tả phụ, nhãn phụ (tương phản 4.61:1) |
| `textDisabled` | `#9CA3AF` | `ColorScheme.outlineVariant` | Figma Prototype | Chữ nút vô hiệu hóa, món hết hàng |
| `error` | `#EF4444` | `ColorScheme.error` | Figma Prototype | Màu báo lỗi (Trong Flutter khuyên dùng `#D32F2F` nếu text nhỏ để đạt tương phản AA $\ge 4.5:1$) |
| `errorContainer` | `#FEE2E2` | `ColorScheme.errorContainer` | DESIGN.md §2.1 | Nền hộp thông báo lỗi, banner sự cố |
| `onErrorContainer` | `#B91C1C` | `ColorScheme.onErrorContainer` | DESIGN.md §2.1 | Chữ/Icon lỗi trên nền đỏ nhạt |
| `success` | `#10B981` | Hằng số `AppColors.success` | Figma Prototype | Trạng thái giao thành công, đối soát hợp lệ |
| `successContainer` | `#D1FAE5` | Hằng số `AppColors.successContainer`| Figma Prototype | Nền banner thành công, badge hợp lệ |
| `warning` | `#F59E0B` | Hằng số `AppColors.warning` | Figma Prototype | Cảnh báo Cut-off time, đếm ngược |
| `warningContainer` | `#FEF3C7` | Hằng số `AppColors.warningContainer`| Figma Prototype | Nền banner Cut-off time |
| `borderDefault` | `#E5E7EB` | `ColorScheme.outline` | Figma Prototype | Đường viền ô nhập liệu, divider |
| `borderFocused` | `#FF5722` | Hằng số `AppColors.borderFocused` | DESIGN.md §2.1 | Viền ô input khi đang nhập liệu |

### 1.2. Typography Tokens (Kiểu chữ)
*Font family chuẩn: **Plus Jakarta Sans** (chủ đạo) kết hợp **Inter** (Text Field, Navigation Bar, Tiêu đề App Bar, Empty State).*

| Typography Token | Size (sp) | Weight | Line Height | Ánh xạ Flutter `TextTheme` | Mục đích sử dụng |
| :--- | :---: | :--- | :---: | :--- | :--- |
| `headline-large` | 28sp | Bold (w700) | 34dp (1.2) | `textTheme.headlineLarge` | Tổng tiền thanh toán lớn (`S4`, `S5`), Mã PIN 4829 (`S7`) |
| `headline-medium`| 22sp | Bold (w700) | 28dp (1.27)| `textTheme.headlineMedium` | Tiêu đề App Bar chính, tiêu đề Dialog Đặt thành công |
| `title-large` | 18sp | Semi-Bold (w600) | 24dp (1.33)| `textTheme.titleLarge` | Tên quán ăn, tiêu đề section lớn |
| `title-medium` | 16sp | Semi-Bold (w600) | 22dp (1.38)| `textTheme.titleMedium` | Tên món ăn trên card, tên danh mục |
| `body-large` | 16sp | Regular (w400) | 24dp (1.5) | `textTheme.bodyLarge` | Nội dung mô tả chi tiết món ăn, quy định giao nhận |
| `body-medium` | 14sp | Regular (w400) | 20dp (1.43)| `textTheme.bodyMedium` | Nhãn ô nhập liệu, mô tả phụ, đơn giá |
| `body-medium-bold`| 14sp| Semi-Bold (w600) | 20dp (1.43)| `textTheme.bodyMedium.copyWith(fontWeight: FontWeight.w600)` | Đơn giá món, tên tài xế trên thẻ `S6` |
| `label-large` | 15sp | Semi-Bold (w600) | 20dp (1.33)| `textTheme.labelLarge` | Chữ trên nút bấm (Buttons), Tab Bottom Nav |
| `label-small` | 12sp | Medium (w500) | 16dp (1.33)| `textTheme.labelSmall` | Badge giảm giá, chip đếm ngược, badge trạng thái |
| `caption` | 12sp | Regular (w400) | 16dp (1.33)| `textTheme.bodySmall` | Helper text ô nhập liệu, ghi chú chân trang |

### 1.3. Spacing Tokens (Khoảng cách & Padding)

| Token Name | Giá trị | Hằng số Flutter dự kiến | Nguồn | Ứng dụng thực tế |
| :--- | :---: | :--- | :--- | :--- |
| `spacing/4` | 4dp | `AppSpacing.xs = 4.0` | DESIGN.md | Khoảng cách icon và text phụ |
| `spacing/8` | 8dp | `AppSpacing.sm = 8.0` | Figma Variables | Gap giữa các phần tử nhỏ trong Auto Layout |
| `spacing/12` | 12dp | `AppSpacing.md = 12.0` | DESIGN.md | Khoảng cách giữa các cột grid, gap các card |
| `spacing/16` | 16dp | `AppSpacing.base = 16.0` | Figma Variables | **Lề màn hình chuẩn (Screen Margin)**, padding card |
| `spacing/24` | 24dp | `AppSpacing.lg = 24.0` | DESIGN.md | Khoảng cách giữa các khối section |
| `spacing/32` | 32dp | `AppSpacing.xl = 32.0` | DESIGN.md | Padding đỉnh Modal Bottom Sheet, Dialog |
| `spacing/48` | 48dp | `AppSpacing.xxl = 48.0` | DESIGN.md | **Chiều cao tối thiểu Touch Target** |

### 1.4. Border Radius Tokens (Bo góc)

| Token Name | Giá trị | Cấu hình Flutter dự kiến | Ứng dụng cụ thể |
| :--- | :---: | :--- | :--- |
| `radius/sm` | 4dp | `BorderRadius.circular(4.0)` | Checkbox, badge mini |
| `radius/md` | 8dp | `BorderRadius.circular(8.0)` | Ô nhập liệu (`TextFormField`), nút phụ nhỏ |
| `radius/lg` | 12dp | `BorderRadius.circular(12.0)` | Thẻ món ăn (`Food Item Card`), khung ảnh |
| `radius/xl` | 16dp | `BorderRadius.circular(16.0)` | Hộp thoại (`AlertDialog`), Modal Bottom Sheet |
| `radius/full` | 999dp | `const StadiumBorder()` | Nút CTA dạng Pill, Avatar, Chip lọc |

### 1.5. Elevation & Shadow Tokens (Độ nổi)

| Token Name | Giá trị Shadow | Ánh xạ Flutter Elevation | Ứng dụng cụ thể |
| :--- | :--- | :---: | :--- |
| `elevation-0` | None | `0.0` | Scaffold background, Divider, Input flat |
| `elevation-1` | `0px 2px 6px rgba(0,0,0,0.06)` | `1.0` (M3) | Thẻ món ăn (`Card`), Banner nhẹ |
| `elevation-2` | `0px 4px 12px rgba(0,0,0,0.08)` | `2.0` (M3) | Sticky Header khi cuộn, Filter Chip bar |
| `elevation-3` | `0px 6px 16px rgba(0,0,0,0.12)` | `3.0` (M3) | `NavigationBar` chân trang, Thẻ shipper nổi, Cart Bar nổi |
| `elevation-4` | `0px 12px 28px rgba(0,0,0,0.18)`| `6.0` (M3) | `AlertDialog`, Modal `showModalBottomSheet` |

---

## 2. Bảng Component → Widget (C01–C09 & Cart Bar đặc thù)

Bảng đối chiếu toàn bộ các Master Component từ Figma `ALDYFWUZ72BaeyulpVi7uY` sang Flutter Widget chuẩn Material 3:

| Mã | Tên Component | Node Figma & Tên Layer | Variant hiện có trên Figma | Variant còn thiếu (⚠ CẦN BỔ SUNG) | Flutter Widget tương ứng | Thuộc tính chính cấu hình trong Flutter |
| :---: | :--- | :--- | :--- | :--- | :--- | :--- |
| **C01** | Button | `KTX/Button/Primary` (`438:4829`, `462:1932`) | `State=Default`, `Disabled` | `State=Pressed`, `Loading`; Biến thể `Type=Secondary`, `Outline`, `Danger` | **`FilledButton`** (chính), `OutlinedButton`, `ElevatedButton` | `style: FilledButton.styleFrom(backgroundColor: ColorScheme.primary, minimumSize: const Size(double.infinity, 48), shape: const StadiumBorder())` |
| **C02** | Text Field | `Crave/Text Field` (`438:4829`, `462:1932`) | `State=Default`, `Error` | `State=Focused`, `Filled`, `Disabled` | **`TextFormField`** | `decoration: InputDecoration(border: OutlineInputBorder(borderRadius: BorderRadius.circular(8)), contentPadding: const EdgeInsets.symmetric(horizontal: 16, vertical: 14))` |
| **C03** | Food Item Card | `Food Item Card` (`462:1932`, `438:1030`) | Vertical card (S1), Horizontal card (S2) | `State=SoldOut` (món hết hàng) | **`Card`** hoặc `InkWell` + `Container` | `Card(elevation: 1, shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)), child: ...)` |
| **C04** | Navigation Bar | `Điều hướng chính` (`438:478`, `438:571`) | 4 Tabs: `Home`, `Explore`, `Orders`, `Profile` | Badge đếm số lượng cho tab Orders | **`NavigationBar`** (M3) | `NavigationBar(selectedIndex: currentIndex, destinations: const [NavigationDestination(icon: Icon(Icons.home), label: 'Trang chủ'), ...])` |
| **C05** | App Bar / Top Header | Header có logo + Chuông + Giỏ + Avatar (`462:1932`); App Bar Detail (`438:1030`) | Default có Avatar mở User Dropdown Menu (`438:5147`); Detail có Back button | Header có nút Hotline khẩn cấp | **`AppBar`** hoặc custom `SliverAppBar` | `AppBar(title: Text(...), centerTitle: true, elevation: 0, leading: IconButton(icon: const Icon(Icons.arrow_back), onPressed: ...))` |
| **C06** | Dialog | Dialog / Đặt hàng thành công (`438:5157`) | 1 trạng thái thành công | Biến thể Danger Dialog (Hủy đơn hàng) | **`AlertDialog`** / `showDialog` | `AlertDialog(shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(16)), title: ..., content: ..., actions: [FilledButton(...)])` |
| **C07** | Loading State | Thư viện trạng thái chờ (`438:5148`); Shimmer S1/S2/S8b/S10 (`588:233...`) | Shimmer Skeleton toàn màn hình | Circular Overlay spinner cho S5 khi kiểm tra chuyển khoản | **`Shimmer`** & `CircularProgressIndicator` | `Shimmer.fromColors(baseColor: Colors.grey[300]!, highlightColor: Colors.grey[100]!)` |
| **C08** | Empty State | Giỏ hàng trống (`438:5594`); Lịch sử trống | 1 trạng thái giỏ trống kèm nút khám phá | Empty state tìm kiếm không thấy món | Custom **`Column`** Widget | `Column(mainAxisAlignment: MainAxisAlignment.center, children: [Icon(Icons.shopping_bag_outlined, size: 64), Text(...), FilledButton(...)])` |
| **C09** | Error State | Thông báo lỗi Form, Banner sự cố | 1 trạng thái inline error | Error State toàn màn hình mất mạng KTX | Custom **`Container`** Alert | `Container(padding: const EdgeInsets.all(12), decoration: BoxDecoration(color: ColorScheme.errorContainer, borderRadius: BorderRadius.circular(8)), child: ...)` |
| **Cart**| Sticky Cart Bar | `Bottom Floating Sticky Batch Order Cart Bar` (`605:381`) | 1 trạng thái hiển thị tổng tiền + số món + nút xem giỏ | Trạng thái loading khi đang đồng bộ giá | Custom **`Container`** bám đáy | `Container(padding: const EdgeInsets.all(16), decoration: BoxDecoration(color: ColorScheme.primary, borderRadius: BorderRadius.circular(16)), child: ...)` |

---

## 3. Đặc tả Kỹ thuật Từng Màn hình (Đủ 6 Mục)

### S0 – Cụm Khởi tạo & Xác thực Định danh KTX (Flow 0)

#### S0_StudentLogin (`438:4829`), S0_StudentRegister (`438:4279`), S0_OTPVerification (`438:5011`), S0_ForgotPassword (`438:4498/4656`)
* **3.1 Layout:**
  - `Scaffold` với nền `surfaceBg` (#F9FAFB).
  - Bố cục `SingleChildScrollView` kết hợp `Padding(EdgeInsets.all(24))`:
    - Phần đầu: Logo KTXFood, biểu ngữ chào đón, Segmented Tab chọn vai trò (Sinh viên KTX / Chủ quán / Shipper).
    - Phần thân: Cụm các trường `TextFormField` (SĐT/Email sinh viên `@vnuhcm.edu.vn`, Mật khẩu; với màn Đăng ký có thêm Dropdown chọn KTX Khu A/B, Tòa nhà *Tòa B3*, Số phòng *Phòng 408*).
    - Màn OTP (`438:5011`): Hiển thị thông tin sinh viên **Lê Thùy Linh**, SĐT **`+84 912 *** 829`**, hàng 6 ô `RawKeyboardListener` / `PinCodeTextField` độc lập, đồng hồ đếm ngược 60s.
    - Phần chân: Nút CTA `FilledButton` ("Đăng nhập" / "Tiếp tục" / "Xác nhận OTP"), các liên kết `TextButton` "Quên mật khẩu?" và "Đăng ký mới".
* **3.2 Components:** `C01 Button`, `C02 Text Field`, `C09 Error State`.
* **3.3 States:**
  - `default`: Hiển thị form trống hoặc số điện thoại đã lưu.
  - `error`: Hiển thị text lỗi đỏ (#EF4444) khi sai mật khẩu, sai định dạng email ĐHQG hoặc sai mã OTP.
  - `loading`: Nút CTA hiển thị `CircularProgressIndicator(color: Colors.white)` khi gọi API xác thực.
* **3.4 User interactions:**
  - Nhập văn bản; chạm icon con mắt để ẩn/hiện mật khẩu.
  - Nhập mã OTP: tự động nhảy focus sang ô kế tiếp khi gõ đủ số.
  - Chạm "Gửi lại OTP": kích hoạt gửi lại SMS và reset đồng hồ 60s.
* **3.5 Navigation:**
  - Từ `S0_StudentLogin` $\rightarrow$ Chạm Đăng ký mở `S0_StudentRegister`; chạm Quên MK mở `S0_ForgotPasswordStep1`.
  - Từ `S0_StudentRegister` $\rightarrow$ Bấm Tiếp tục mở `S0_OTPVerification` (`438:5011`).
  - Xác thực thành công $\rightarrow$ `Navigator.pushReplacementNamed(context, '/home')` dẫn vào `S1_FoodSearchHome`.
* **3.6 Important UI constraints:**
  - Bàn phím: Tự động co giãn theo `viewInsets.bottom` để ô nhập và nút CTA không bị che.
  - Touch target $\ge 48\text{dp}$. Ô nhập OTP kích thước tối thiểu $44\times 48\text{dp}$.

---

### S1 – S1_FoodSearchHome (Trang chủ "Main" - Tra cứu đặt đồ ăn)
* **3.1 Layout:**
  - `Scaffold` với nền `surfaceBg` (#F9FAFB).
  - Header cố định: `Container` chứa Logo KTXFood, lời chào **"Chào Linh!"**, icon Chuông thông báo (kèm badge đỏ), icon Giỏ hàng (badge số món), và Avatar mở `User Dropdown Menu` (`438:5147`).
  - Thân trang cuộn dọc (`CustomScrollView` với các `SliverToBoxAdapter` và `SliverList`):
    - Khối 1: Ô tìm kiếm (`Padding(EdgeInsets.symmetric(horizontal: 16))`, chiều cao 48dp).
    - Khối 2: Banner Gom đơn Ca Trưa: Nền `warningContainer`, hiển thị **"Giao 11:30–12:00, chốt đơn lúc 10:45"**, chỉ số **"Đã gom 42 đơn cho Cổng KTX Khu B"**, đồng hồ đếm ngược chạy từng giây.
    - Khối 3: Bộ lọc khu vực dạng ngang: `ListView.builder(scrollDirection: Axis.horizontal)`, các chip: `Tất cả` (Active), `KTX Khu B`, `KTX Khu A`, `Làng ĐH`.
    - Khối 4: Danh mục nhanh (Quick Categories): `Row` cuộn ngang các icon tròn kèm nhãn: *Cơm trưa, Bún phở, Trà sữa, Ăn vặt, Bánh mì, Nước ép*.
    - Khối 5: Section "Quán quen được yêu thích": Danh sách bố trí theo **dạng Thẻ dọc (Vertical List Card)**, mỗi thẻ gồm ảnh quán, tên quán (*Cơm Tấm Sinh Viên Cô Ba - KTX Khu B*), số sao 4.8 ⭐, khoảng cách 450m, nút **"Chọn món +"**.
  - Chân trang: `NavigationBar` M3 cố định (Active Tab Index = 0: Trang chủ).
* **3.2 Components:** `C02 Text Field`, `C03 Food Item Card`, `C04 Navigation Bar`, `C05 Top Header`, `User Dropdown Menu` (`438:5147`).
* **3.3 States:**
  - `default`: Hiển thị danh sách quán ăn, số lượng gom 42 đơn, đồng hồ đếm ngược.
  - `loading`: Hiển thị khung **Loading Shimmer** (`588:233`) cho banner và các thẻ quán ăn.
  - `empty`: Khi tìm kiếm không thấy quán nào $\rightarrow$ Hiển thị `C08 Empty State` ("Không tìm thấy món ăn phù hợp").
* **3.4 User interactions:**
  - Chạm Avatar trên header $\rightarrow$ Mở `User Dropdown Menu` (`438:5147`) gồm 7 mục chức năng.
  - Gõ ô tìm kiếm $\rightarrow$ Lọc quán/món ăn theo thời gian thực.
  - Chạm Chip khu vực (ví dụ KTX Khu B) $\rightarrow$ Lọc danh sách quán theo địa bàn.
  - Chạm nút "Chọn món +" hoặc thân thẻ quán $\rightarrow$ Điều hướng tới `S2_StoreDetailMenu`.
  - Chạm icon Giỏ hàng $\rightarrow$ Mở `S4_GroupCartCheckout`.
* **3.5 Navigation:**
  - Vào từ: Đăng nhập thành công (`S0`), hoặc quay lại từ `S9` sau đánh giá.
  - Chạm thẻ quán $\rightarrow$ `Navigator.push` sang `S2`.
  - Chạm Tab Đơn hàng $\rightarrow$ `Navigator.pushReplacement` sang `S6`.
* **3.6 Important UI constraints:**
  - Tự động ẩn bàn phím (`FocusScope.of(context).unfocus()`) khi vuốt cuộn màn hình.
  - Touch target tất cả icon và nút bấm $\ge 48\times 48\text{dp}$.

---

### S2 – S2_StoreDetailMenu (Chi tiết Quán ăn & Thực đơn)
* **3.1 Layout:**
  - `Scaffold` với `CustomScrollView` (Sliver Architecture):
    - `SliverAppBar` (cao 180dp) chứa ảnh bìa quán, nút Back và nút Tim yêu thích (icon có nền tròn mờ bảo đảm tương phản).
    - `SliverToBoxAdapter`: Thông tin quán (*Cơm Tấm Cô Ba*), đánh giá 4.8 ⭐, cự ly 450m, bảng tin thông báo từ chủ quán.
    - `SliverPersistentHeader` (Sticky): Thanh tab phân loại danh mục món (*Cơm sườn/bì/chả, Món thêm, Đồ uống*).
    - `SliverList`: Danh sách món ăn bố trí theo chiều ngang (Horizontal Cards) gồm ảnh thumbnail 80×80dp, tên món, mô tả topping, đơn giá, nút `+ Thêm`.
  - Đáy màn hình: **Bottom Floating Sticky Batch Order Cart Bar** (Component `605:381`) hiển thị số lượng món, tổng tiền tạm tính và nút "Xem giỏ hàng".
* **3.2 Components:** `C05 App Bar`, `C03 Food Item Card`, `Bottom Floating Sticky Batch Order Cart Bar` (`605:381`).
* **3.3 States:**
  - `populated`: Danh sách món ăn đầy đủ.
  - `loading`: Khung **Loading Shimmer** (`588:564`) hiển thị lúc nạp menu.
  - `soldOut`: Món hết hàng hiển thị lớp phủ mờ kèm nhãn "Hết hàng ca trưa", nút thêm bị disable.
* **3.4 User interactions:**
  - Chạm nút Tim $\rightarrow$ Đổi màu đỏ, lưu quán vào `S11_FavoriteList`.
  - Chạm nút `+ Thêm` trên món ăn $\rightarrow$ Mở Modal `S3_FoodCustomization`.
  - Chạm thanh Cart Bar `605:381` $\rightarrow$ Điều hướng tới `S4_GroupCartCheckout`.
* **3.5 Navigation:**
  - Vào từ: `S1_FoodSearchHome` hoặc `S11_FavoriteList`.
  - Bấm Back $\rightarrow$ Quay lại `S1`.
  - Bấm `+ Thêm` $\rightarrow$ Mở `S3` (Modal Bottom Sheet).
  - Bấm Cart Bar $\rightarrow$ `Navigator.push` sang `S4`.
* **3.6 Important UI constraints:**
  - Thanh Cart Bar `605:381` bám dính đáy cách lề dưới 16dp, có shadow `elevation-3`.
  - Touch target $\ge 48\text{dp}$.

---

### S3 – S3_FoodCustomization (Tùy biến món ăn)
* **3.1 Layout:**
  - Cấu trúc `showModalBottomSheet` với `isScrollControlled: true`.
  - Khung modal bo góc trên `radius-xl` (16dp), nền trắng `#FFFFFF`, chiều cao chiếm tối đa 85% màn hình, có Handle bar ở đỉnh.
  - Thân modal: `ListView` cuộn dọc:
    - Ảnh lớn món ăn tỉ lệ 16:9, Tên món (*Cơm Tấm Sườn Bì Chả*), Đơn giá cơ sở 35.000đ.
    - Nhóm 1: Chọn Size (`RadioListTile` - Size Vừa +0đ / Size Lớn +10.000đ).
    - Nhóm 2: Mức cay (`RadioListTile` - Không cay / Vừa / Nhiều).
    - Nhóm 3: Topping thêm (`CheckboxListTile` - Trứng ốp la +5k, Chả thêm +7k, Canh +6k).
    - Nhóm 4: Ghi chú (`TextFormField` nhiều dòng: "Nhiều mắm, không mỡ hành...").
    - Nhóm 5: Bộ đếm số lượng (`Row` chứa nút `-`, Text số lượng, nút `+`).
  - Đáy modal: Cố định nút CTA `FilledButton` ("Thêm vào giỏ - 40.000đ").
* **3.2 Components:** `C01 Button`, `C02 Text Field`.
* **3.3 States:**
  - `default`: Size Vừa chọn sẵn, số lượng = 1.
  - `interactive`: Khi người dùng tích thêm topping, tổng giá trên nút CTA tự động cộng dồn thời gian thực.
* **3.4 User interactions:**
  - Chạm chọn radio/checkbox $\rightarrow$ Tính lại tổng tiền ngay lập tức.
  - Chạm `-` / `+` $\rightarrow$ Thay đổi số lượng món.
  - Chạm nút CTA $\rightarrow$ Đóng modal, phát event thêm vào giỏ và cập nhật Cart Bar `605:381`.
* **3.5 Navigation:**
  - Vào từ: `S2_StoreDetailMenu` khi bấm `+ Thêm`.
  - Bấm CTA hoặc vuốt xuống $\rightarrow$ `Navigator.pop(context)` trở về `S2`.
* **3.6 Important UI constraints:**
  - Bọc bàn phím bằng `EdgeInsets.only(bottom: MediaQuery.of(context).viewInsets.bottom)`.
  - Touch target mỗi tùy chọn $\ge 48\text{dp}$.

---

### S4 – S4_GroupCartCheckout (Giỏ hàng & Thanh toán gom đơn)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` tiêu đề "Giỏ hàng & Thanh toán gom đơn".
  - Thân trang: `ListView` cuộn dọc với padding 16dp:
    - Khối cảnh báo: Banner "Đợt gom Ca Trưa sắp đóng" kèm đếm ngược.
    - **Bước 1: Điểm nhận hàng cố định (Bắt buộc):** `RadioListTile` chọn:
      1. *KTX Khu B – Trụ A1–A2* (Mặc định).
      2. *KTX Khu A – Cổng Parabol*.
      3. *Cổng Viện Môi trường Làng ĐH*.
    - **Bước 2: Chọn khung giờ theo Ca:** `RadioListTile` chọn:
      1. *Ca trưa: 11:30 – 12:00 (Chốt đơn lúc 10:45)*.
      2. *Ca tối: 18:00 – 18:30 (Chốt đơn lúc 17:15)*.
    - **Bước 3: Tóm tắt món đã chọn:** Danh sách món trong giỏ kèm bộ đếm số lượng và nút xóa.
    - Ô áp dụng mã ưu đãi (`TextFormField` + `OutlinedButton` "Áp dụng").
    - Khối Phương thức thanh toán: `RadioListTile` chọn: *Chuyển khoản VietQR* hoặc *Tiền mặt (COD)*.
    - Bảng thanh toán: Tạm tính (40.000đ), Phí gom KTX (0đ), Giảm giá (-5.000đ), Tổng thanh toán: **35.000đ** (`headline-large`).
  - Đáy màn hình: Khung Sticky chứa nút CTA chiều cao 48dp.
* **3.2 Components:** `C05 App Bar`, `C02 Text Field`, `C01 Button`, `C08 Empty State` (`438:5594`).
* **3.3 States:**
  - `populated`: Giỏ có món, cho phép chọn điểm nhận và ca giao.
  - `empty`: Khi giỏ rỗng $\rightarrow$ Hiển thị **Giỏ hàng trống** (`438:5594`) kèm nút "Khám phá món ăn" quay về `S1`.
  - `voucherApplied`: Hiển thị dòng giảm giá màu xanh lá.
* **3.4 User interactions:**
  - Thay đổi số lượng món hoặc xóa món.
  - Chọn điểm nhận và ca giao hàng.
  - Chọn hình thức thanh toán: Nếu chọn VietQR, nhãn nút đổi thành "Tiến hành thanh toán"; nếu chọn COD, nhãn nút đổi thành "Xác nhận đặt đơn".
* **3.5 Navigation:**
  - Vào từ: `S2` hoặc icon Giỏ hàng ở `S1`; hoặc quay lại từ `S5` (đổi phương thức sang COD).
  - Bấm Back $\rightarrow$ Quay lại `S2`.
  - Chọn VietQR $\rightarrow$ Bấm nút CTA $\rightarrow$ `Navigator.push` sang `S5_OnlinePayment`.
  - Chọn COD $\rightarrow$ Bấm nút CTA $\rightarrow$ Mở `S5_Success` (`438:5157`).
* **3.6 Important UI constraints:**
  - Validation: Bắt buộc chọn Điểm nhận KTX và Ca nhận trước khi bấm thanh toán.
  - Tổng tiền hiển thị font `headline-large` (28sp Bold) màu cam nổi bật.

---

### S5 – S5_OnlinePayment (Thanh toán online VietQR)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` tiêu đề "Thanh toán VietQR".
  - Thân trang cuộn dọc (`SingleChildScrollView`, padding 16dp):
    - Khung tóm tắt đơn: Mã đơn `#8829B`, Tổng tiền cần chuyển **35.000đ** (`headline-large`).
    - Khung hiển thị mã VietQR động chính giữa màn hình (mã hóa chuỗi `KTX-ORDER-8829B`, kích thước $220\times 220\text{dp}$, bo góc 12dp, viền trắng bao quanh $\ge 16\text{dp}$).
    - Nút phụ: `OutlinedButton.icon` "Tải mã QR" hoặc "Mở App Ngân hàng".
    - Bảng thông tin thụ hưởng: Tên chủ quán, Ngân hàng, Số tài khoản kèm icon Sao chép, Cú pháp chuyển khoản bắt buộc: `KTX8829B LINH`.
    - Đồng hồ đếm ngược phiên thanh toán (10:00 phút).
    - Nút liên kết chuyển đổi: `TextButton` "Gặp sự cố chuyển khoản? Đổi sang Tiền mặt (COD)".
  - Chân trang: Sticky `FilledButton` 48dp "Đã hoàn tất chuyển khoản".
* **3.2 Components:** `C05 App Bar`, `C01 Button`, `C07 Loading State`.
* **3.3 States:**
  - `default`: Đang hiển thị mã QR và đồng hồ đếm ngược.
  - `loading`: Overlay `CircularProgressIndicator` khi bấm "Đã hoàn tất chuyển khoản" để xác thực giao dịch.
* **3.4 User interactions:**
  - Bấm icon sao chép STK / Cú pháp $\rightarrow$ Copy vào clipboard, hiện `SnackBar` "Đã sao chép".
  - Bấm "Đổi sang Tiền mặt (COD)" $\rightarrow$ Quay lại `S4` và tự động tích radio COD.
  - Bấm "Đã hoàn tất chuyển khoản" $\rightarrow$ Kích hoạt loading và mở `S5_Success`.
* **3.5 Navigation:**
  - Vào từ: `S4_GroupCartCheckout` khi chọn VietQR.
  - Bấm Back hoặc Đổi sang COD $\rightarrow$ Quay lại `S4`.
  - Thanh toán hoàn tất $\rightarrow$ Mở `S5_Success` (`438:5157`).
* **3.6 Important UI constraints:**
  - Viền trắng quanh QR code $\ge 16\text{dp}$ để camera quét không bị lóa viền.

---

### S5_Success – S5_OrderSuccessDialog (Dialog/Màn Đặt hàng thành công)
* **3.1 Layout:**
  - `AlertDialog` hoặc Full-screen Overlay trên nền tối phủ mờ `rgba(0,0,0,0.5)`.
  - Khung bo góc `radius-xl` (16dp), nền trắng `#FFFFFF`, padding 24dp.
  - Cấu trúc dọc:
    - Icon minh họa checkmark tròn thành công màu xanh lá (64dp).
    - Tiêu đề: "Đặt đơn Ca Trưa thành công!" (`headlineMedium`, Bold, canh giữa).
    - Nội dung text: "Mã đơn: #8829B. Đơn hàng đang gửi tới quán. Vui lòng có mặt tại **Cổng KTX Khu B (Trụ A1–A2)** lúc **11:30** để nhận đồ ăn."
    - Nút CTA: `FilledButton` 48dp "Theo dõi đơn hàng ngay".
* **3.2 Components:** `C06 Dialog`, `C01 Button`.
* **3.3 States:** `default`: Hiển thị xác nhận đơn hàng thành công.
* **3.4 User interactions:**
  - Chạm "Theo dõi đơn hàng ngay" $\rightarrow$ Đóng overlay và chuyển sang `S6`.
  - `barrierDismissible: false` (không cho phép bấm ra ngoài để đóng).
* **3.5 Navigation:**
  - Vào từ: `S5` (sau chuyển khoản) hoặc `S4` (sau đặt COD).
  - Bấm CTA $\rightarrow$ `Navigator.pushAndRemoveUntil` tới `S6_LiveOrderTracking`.
* **3.6 Important UI constraints:**
  - Bắt buộc `barrierDismissible: false`. Nút CTA full width chiều cao 48dp.

---

### S6 – S6_LiveOrderTracking (Theo dõi Đơn hàng thời gian thực)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` hiển thị tiêu đề mã đơn `#8829B` và icon gọi Hotline hỗ trợ.
  - Thân trang cuộn dọc (`SingleChildScrollView`, padding 16dp):
    - Section 1: Bộ đếm thời gian shipper tới cổng ("Dự kiến tới Cổng KTX trong: 08 phút").
    - Section 2: Stepper tiến trình (4 bước: `Đã nhận đơn` $\rightarrow$ `Đang nấu` $\rightarrow$ `Đang gom chuyến` $\rightarrow$ `Đã tới Cổng KTX`).
    - Section 3: Thẻ thông tin shipper (`Card` bo góc 12dp gồm Avatar, Tên *Nguyễn Văn Minh*, Biển số *59-X1 839.24*, Vị trí đón *Trụ A1–A2 Cổng KTX Khu B*, nút gọi điện nhanh).
    - Section 4: Danh sách tóm tắt các món trong bọc đơn hàng.
    - Section 5: Nút phụ "Hủy đơn hàng" (vô hiệu hóa khi quán đã nấu).
    - Section 6: Nút liên kết "Báo cáo sự cố đơn hàng" (mở `S8`).
  - Chân trang: Sticky Bottom Bar chứa nút CTA lớn: **"Mở Mã QR Nhận Hàng"** (48dp).
* **3.2 Components:** `C05 App Bar`, `C01 Button`, `C04 Navigation Bar` (Active Tab Index = 2: Orders).
* **3.3 States:**
  - `cooking`: Trạng thái đang nấu, nút hủy đơn bị mờ vô hiệu hóa.
  - `arrived`: Shipper đã đến cổng $\rightarrow$ Nút "Mở Mã QR Nhận Hàng" đổi sang màu cam nổi bật và nhấp nháy.
  - `disputed`: Trạng thái đơn đổi thành "Đang chờ xử lý hoàn tiền" (sau khi gửi `S8`).
* **3.4 User interactions:**
  - Chạm nút gọi điện trên thẻ shipper $\rightarrow$ Gọi tới số tài xế qua `url_launcher`.
  - Chạm "Mở Mã QR Nhận Hàng" $\rightarrow$ Mở màn hình `S7_PickupQRCode`.
  - Chạm "Báo cáo sự cố đơn hàng" $\rightarrow$ Điều hướng tới `S8_DisputeRefund`.
* **3.5 Navigation:**
  - Vào từ: `S5_Success`, Tab Orders trên Bottom Nav, hoặc từ Push Notification.
  - Bấm Mở mã QR $\rightarrow$ Mở `S7`.
  - Bấm Báo cáo sự cố $\rightarrow$ Chuyển tới `S8`.
  - Bấm Back $\rightarrow$ Quay về Trang chủ `S1`.
* **3.6 Important UI constraints:**
  - Nút Mở QR luôn neo cố định chân màn hình để thao tác một chạm nhanh nhất.

---

### S7 – S7_PickupQRCode (Theo Dõi Đơn & Mã Nhận tại Cổng KTX)
* **3.1 Layout:**
  - **Màn hình độc lập Full-screen** (nền trắng tương phản cao, không che khuất nội dung).
  - Top Bar: Tiêu đề **"Theo Dõi Đơn & Mã Nhận"**, nút Back quay lại `S6`.
  - Thân trang bố trí canh giữa:
    - Khối thông tin: Mã đơn `#8829B`, Tòa nhà **"KTX KHU B • TÒA B3"**, **"Phòng 408"**, **"Ca Trưa: 11:30 - 12:00"**.
    - Khung chứa Mã QR kích thước lớn ($200\times 200\text{dp}$), mã hóa chuỗi `KTX-ORDER-8829B`.
    - **Vùng đối soát thủ công nổi bật dưới QR:** Dòng text mã đơn và hiển thị cỡ lớn: **"Mã PIN / Đuôi SĐT: 4829"** (font `headline-large`, Semi-Bold).
    - Huy hiệu nổi bật: **"Đã thanh toán (VietQR) • Không thu tiền"**.
    - Vị trí đón nhận: "Cổng Đón B2" / "Bàn số 2 • Cổng B" *(⚠ MÂU THUẪN NGUỒN so với S4 ghi Trụ A1-A2)*.
    - Thông tin shipper: *Nguyễn Văn Minh – 59-X1 839.24*. Quy định: *Vui lòng có mặt nhận món trong tối đa 15 phút*.
    - Danh sách món ăn đối soát tại chỗ.
  - Chân màn hình: **2 Nút tương tác song song (Khớp 100% Figma `438:1468`):**
    1. Nút bên trái: `OutlinedButton` **"Theo dõi đơn"** (quay lại `S6`).
    2. Nút bên phải: `FilledButton` **"Tăng độ sáng"** (kích hoạt max brightness).
* **3.2 Components:** `C05 App Bar`, `C01 Button`, Custom QR Widget (`qr_flutter`).
* **3.3 States:**
  - `default`: Hiển thị đầy đủ mã QR, PIN 4829 và 2 nút đáy.
* **3.4 User interactions:**
  - Xuất trình mã QR cho shipper quét.
  - Đọc mã PIN `4829` nếu camera shipper bị chói nắng.
  - Bấm "Tăng độ sáng" $\rightarrow$ Ứng dụng gọi API hệ thống `screen_brightness` kích hoạt độ sáng màn hình 100%.
  - Bấm "Theo dõi đơn" $\rightarrow$ Quay lại `S6`.
* **3.5 Navigation:**
  - Vào từ: `S6_LiveOrderTracking` khi bấm "Mở Mã QR Nhận Hàng".
  - Bấm "Theo dõi đơn" $\rightarrow$ Quay lại `S6`.
  - **Chuyển tiếp sang S9_ReviewFeedback:**  
    *(⚠ LƯU Ý ĐIỀU HƯỚNG QUAN TRỌNG: Trên Figma S7 không có nút 'Đã nhận được thức ăn' để tránh sinh viên bấm nhầm trước khi nhận hàng. Trong vận hành thực tế, khi shipper quét mã QR thành công và bấm hoàn tất đơn trên app tài xế, tín hiệu WebSocket / Push Notification sẽ tự động kích hoạt chuyển màn hình S7 sang `S9_ReviewFeedback`. Trong Figma Prototype, luồng này được mô phỏng bằng tương tác `After delay` từ S7 sang S9 để đảm bảo flow chạy xuyên suốt không ngõ cụt)*.
* **3.6 Important UI constraints:**
  - Tương phản tuyệt đối: QR đen trên nền trắng tinh khiết, mã PIN `4829` hiển thị cỡ chữ $\ge 24\text{sp}$ Bold.

---

### S8 – S8_DisputeRefund (Khiếu nại và hoàn tiền)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` tiêu đề "Khiếu nại & Hoàn tiền".
  - Thân trang cuộn dọc (`ListView`, padding 16dp):
    - Khung đơn hàng sự cố: Mã đơn `#8829B`, Quán *Cơm Tấm Cô Ba*.
    - Section 1: Chọn nguyên nhân sự cố (`CheckboxListTile` gồm 5 lựa chọn: Thức ăn đổ vỡ bao bì, Giao thiếu món, Giao sai món/khẩu vị, Thức ăn không đảm bảo vệ sinh, Shipper giao trễ ca trưa).
    - Section 2: Chọn món ăn bị ảnh hưởng (Nút "Chọn tất cả" + danh sách các món kèm checkbox).
    - Section 3: Hộp hiển thị **Số tiền yêu cầu hoàn** (tự động tính dựa trên các món được tích chọn, ví dụ: 35.000đ).
    - Section 4: Tải ảnh bằng chứng (khung chụp ảnh/chọn từ thư viện tối thiểu 1 ảnh).
    - Section 5: Mô tả chi tiết (`TextFormField` nhiều dòng).
    - Section 6: Phương thức nhận tiền hoàn (`RadioListTile` chọn: Ví KTX Food hoặc Chuyển khoản Ngân hàng).
  - Chân trang: Sticky `FilledButton` 48dp "Gửi yêu cầu khiếu nại".
* **3.2 Components:** `C05 App Bar`, `C02 Text Field`, `C01 Button`, `C09 Error State`.
* **3.3 States:**
  - `default`: Form chưa chọn món và sự cố.
  - `calculating`: Số tiền hoàn tự động cộng dồn khi tích thêm món.
  - `submitting`: Nút CTA hiển thị spinner trong lúc tải ảnh lên hệ thống.
* **3.4 User interactions:**
  - Tích chọn nguyên nhân sự cố và món ăn bị ảnh hưởng.
  - Bấm "Chọn tất cả món" để chọn nhanh toàn bộ phần ăn.
  - Chụp hoặc chọn ảnh bằng chứng từ thư viện qua `image_picker`.
  - Bấm "Gửi yêu cầu khiếu nại" $\rightarrow$ Validate form và gửi lên server.
* **3.5 Navigation:**
  - Vào từ: `S6_LiveOrderTracking` hoặc `S10_OrderHistory`.
  - Bấm Back $\rightarrow$ Quay lại màn hình trước.
  - Gửi thành công $\rightarrow$ Hiển thị màn Gửi thành công (`438:5174`) rồi chuyển sang `S8c_DisputeDetail` (hoặc quay lại `S6`/`S10` với nhãn "Đang chờ xử lý hoàn tiền").
* **3.6 Important UI constraints:**
  - Bắt buộc chọn ít nhất 1 sự cố, ít nhất 1 món ăn và tải ít nhất 1 ảnh bằng chứng.

---

### S8b & S8c – Phân hệ Lịch sử & Chi tiết Khiếu nại (Màn mới Flow 3)

#### S8b – `S8b_DisputeHistory` (`438:571`) & S8c – `S8c_DisputeDetail` (`438:478`)
* **3.1 Layout:**
  - `S8b`: `Scaffold` với `AppBar` tiêu đề "Lịch sử khiếu nại", hàng chip lọc trạng thái (*Tất cả*, *Đang xử lý*, *Đã hoàn tiền*, *Từ chối*), thân trang `ListView` các thẻ đơn khiếu nại (`#KTX-8741A`, `#KTX-8602C`, `#KTX-8420A`).
  - `S8c`: `Scaffold` với `AppBar` tiêu đề "Chi tiết khiếu nại", Stepper tiến trình thẩm định (`Đã gửi yêu cầu` $\rightarrow$ `Đang xác minh` $\rightarrow$ `Đã duyệt hoàn tiền`), khung thông tin số tiền hoàn và lý do xử lý từ ban quản trị.
* **3.2 Components:** `C05 App Bar`, `C01 Button`, `C07 Loading State`.
* **3.3 States:**
  - `S8b`: `default` (danh sách khiếu nại), `loading` (Khung **Loading Shimmer** `588:1134`).
  - `S8c`: 3 biến thể trạng thái mã đơn: `#KTX-8741A` (`438:5621` - Đang xác minh), `#KTX-8602C` (`438:5714` - Đã duyệt hoàn tiền), `#KTX-8420A` (`438:5807` - Từ chối).
* **3.4 User interactions:**
  - Chạm thẻ khiếu nại trên S8b $\rightarrow$ Mở màn hình chi tiết S8c.
* **3.5 Navigation:**
  - Vào S8b từ: User Dropdown Menu `438:5147` hoặc từ tab Orders `S10`.
  - Từ S8b $\rightarrow$ Chạm đơn mở `S8c`. Bấm Back quay lại màn hình trước.
* **3.6 Important UI constraints:**
  - Stepper thẩm định hiển thị rõ ràng ngày giờ và nguyên nhân phê duyệt/từ chối.

---

### S9 – S9_ReviewFeedback (Đánh giá và phản hồi)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` tiêu đề "Đánh giá đơn hàng" và nút "Bỏ qua" ở góc phải.
  - Thân trang cuộn dọc (`ListView`, padding 16dp):
    - Phần 1: Đánh giá Quán ăn: Tên quán *Cơm Tấm Sinh Viên Cô Ba*, Rating Bar 5 sao ⭐ chạm để chọn, hàng chip nhận xét nhanh (*Món ngon, Đúng khẩu vị, Đóng gói kỹ*), ô nhập nhận xét chi tiết.
    - Phần 2: Đánh giá Shipper: Avatar và tên tài xế *Nguyễn Văn Minh*, Rating Bar 5 sao ⭐ riêng, chip nhận xét nhanh (*Giao đúng giờ tại cổng, Thân thiện, Cẩn thận*), ô góp ý riêng cho tài xế.
  - Chân trang: Sticky `FilledButton` 48dp "Gửi đánh giá".
* **3.2 Components:** `C05 App Bar`, `C02 Text Field`, `C01 Button`.
* **3.3 States:** `default`: Mặc định sẵn 5 sao ⭐ cho cả hai đối tượng.
* **3.4 User interactions:**
  - Chạm số sao để chấm điểm riêng cho Quán và Shipper.
  - Chạm các chip nhận xét nhanh để tự động điền gợi ý.
  - Chạm "Gửi đánh giá" $\rightarrow$ Hiển thị màn hình Đánh giá thành công (`438:5577`) rồi quay về Trang chủ.
* **3.5 Navigation:**
  - Vào từ: `S7_PickupQRCode` sau khi nhận hàng xong; hoặc từ nút "Đánh giá" trong `S10_OrderHistory`.
  - Bấm "Bỏ qua" hoặc "Gửi đánh giá" $\rightarrow$ `Navigator.pushAndRemoveUntil` trở về Trang chủ `S1_FoodSearchHome`.
* **3.6 Important UI constraints:**
  - Icon sao đánh giá kích thước tối thiểu $36\times 36\text{dp}$, vùng chạm $48\times 48\text{dp}$.

---

### S10 – S10_OrderHistory (Lịch sử đơn hàng)
* **3.1 Layout:**
  - `Scaffold` với `AppBar` tiêu đề "Lịch sử đơn hàng".
  - Segmented Tabs cố định: `TabBar` (*Tất cả*, *Đang xử lý*, *Hoàn tất*, *Đã hủy*).
  - Thân trang: `TabBarView` chứa danh sách thẻ đơn hàng cũ (`ListView.separated`, padding 16dp). Mỗi thẻ hiển thị: Mã đơn `#8829B`, thời gian đặt, tên quán, tóm tắt món, tổng tiền 35.000đ, badge trạng thái (*Đã giao thành công*, *Đang xử lý hoàn tiền*, *Đã hủy*), và cặp nút hành động: "Đặt lại đơn này" (`Secondary Button`) và "Khiếu nại / Hoàn tiền" (`Outline/Danger Button`).
  - Chân trang: `NavigationBar` M3 cố định (Active Tab Index = 2: Orders).
* **3.2 Components:** `C05 App Bar`, `C01 Button`, `C04 Navigation Bar`, `C08 Empty State`.
* **3.3 States:**
  - `populated`: Danh sách các đơn hàng cũ.
  - `loading`: Khung **Loading Shimmer** (`588:820`).
  - `empty`: Khi tab không có đơn nào $\rightarrow$ Hiển thị `C08 Empty State` ("Chưa có đơn hàng nào trong mục này").
* **3.4 User interactions:**
  - Chuyển tab lọc trạng thái đơn.
  - Chạm nút "Đặt lại đơn này" $\rightarrow$ Nạp nguyên vẹn các món vào giỏ hàng và mở `S4`.
  - Chạm nút "Khiếu nại / Hoàn tiền" $\rightarrow$ Mở form `S8_DisputeRefund`.
* **3.5 Navigation:**
  - Vào từ: Tab Orders trên Bottom Navigation Bar từ bất kỳ màn hình nào.
  - Bấm "Đặt lại đơn" $\rightarrow$ Mở `S4`. Bấm "Khiếu nại" $\rightarrow$ Mở `S8`. Bấm đơn đang giao $\rightarrow$ Mở `S6`.
* **3.6 Important UI constraints:**
  - Các nút hành động trên mỗi thẻ đơn có gap $\ge 8\text{dp}$, chiều cao $\ge 40\text{dp}$ (touch target $\ge 48\text{dp}$). Hỗ trợ kéo vuốt làm mới danh sách (`RefreshIndicator`).

---

### S11, S12, S13 – Các Màn hình Hỗ trợ Cấp cao

#### S11 – `S11_FavoriteList` (`438:2822`), S12 – `S12_NotificationBoard` (`438:1710`), S13 – `S13_ProfileSettings` (`438:3979`)
* **3.1 Layout:**
  - `S11`: `Scaffold` với `AppBar` "Danh sách yêu thích", thân trang `ListView` các thẻ quán ăn ruột kèm nút "Xem thực đơn" chuyển nhanh sang S2.
  - `S12`: `Scaffold` với `AppBar` "Bảng thông báo", thân trang `ListView` các thông báo biến động đơn hàng, cảnh báo giờ chốt ca gom đơn.
  - `S13`: `Scaffold` với `AppBar` "Hồ sơ cá nhân & Cài đặt", hiển thị thông tin sinh viên **Lê Thùy Linh**, SĐT `+84 912 *** 829`, KTX Khu B, Tòa B3, Phòng 408; các mục quản lý địa chỉ nhận mặc định, STK ngân hàng, đổi mật khẩu và nút Đăng xuất.
* **3.2 Components:** `C05 App Bar`, `C01 Button`, `C04 Navigation Bar`, `C07 Loading State`.
* **3.3 States:**
  - `S11`: `loading` (Khung **Loading Shimmer** `588:1296`).
  - `S12`: `loading` (Khung **Loading Shimmer** `588:1677`).
* **3.4 User interactions:** Chuyển đổi cài đặt, xem thông báo, mở nhanh quán quen.
* **3.5 Navigation:**
  - Mở S11 và S12 từ Header và User Dropdown Menu `438:5147`. Mở S13 từ Tab Profile trên Bottom Nav. Bấm Đăng xuất từ S13 quay về `S0_StudentLogin`.
* **3.6 Important UI constraints:** Bảo mật thông tin định danh sinh viên; các toggle cài đặt đạt touch target $\ge 48\text{dp}$.

---

## 4. Hành vi Màn hình Rộng (≥600dp) Áp dụng Chung

Để đảm bảo ứng dụng hiển thị thẩm mỹ và công thái học trên máy tính bảng (Tablet) hoặc màn hình điện thoại gập (Foldables):

1. **Giới hạn độ rộng tối đa nội dung (Max Content Width Constraint):**
   - Toàn bộ nội dung thân trang (`Scaffold body`) được bọc trong widget `Center` với ràng buộc:
     `ConstrainedBox(constraints: BoxConstraints(maxWidth: 600))`
   - Vùng viền hai bên màn hình vượt quá 600dp sẽ hiển thị màu nền trung tính `surfaceBg` (#F9FAFB).
2. **Chuyển đổi Lưới hiển thị (Grid Layout Adaptation):**
   - Danh sách món ăn tại `S1` và `S2`: Chuyển từ danh sách 1 cột dọc (ở 360dp) sang lưới **2 hoặc 3 cột** (ở $\ge 600\text{dp}$) với `crossAxisCount: 2` hoặc `3` để tối ưu diện tích hiển thị.
3. **Chuyển đổi Thanh điều hướng (Navigation Rail):**
   - Khi chiều rộng màn hình $\ge 600\text{dp}$, thanh điều hướng chân trang `NavigationBar` được tự động chuyển đổi thành thanh điều hướng bên hông **`NavigationRail`** neo cố định bên trái màn hình.
4. **Hộp thoại & Modal Bottom Sheet:**
   - Các `AlertDialog` và `showModalBottomSheet` được khống chế chiều rộng tối đa `maxWidth: 480dp`, luôn canh giữa màn hình thay vì kéo giãn toàn bộ bề ngang máy tính bảng.