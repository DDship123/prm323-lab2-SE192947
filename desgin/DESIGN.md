# TÀI LIỆU HỆ THỐNG THIẾT KẾ (DESIGN SYSTEM SPECIFICATION)
## DỰ ÁN: FOOD ORDERING APP – SINH VIÊN KÝ TÚC XÁ ĐHQG-HCM (PRM323 - LAB 2)

> **Người thực hiện:** Thành viên 2 – Ngô Hoàng Trường Đạt (MSSV: SE192964)  
> **Vai trò:** Design System & Components Specialist  
> **Mục tiêu điểm số:** 15/15 điểm hạng mục Design System & Component Library  
> **Tham chiếu hệ thống:** Đồng bộ 100% với `ux/user-flow.md`, `ux/persona.md`, đặc tả Flutter Handoff và chuẩn Material Design 3 (M3).

---

## MỤC LỤC
1. [Triết lý Thiết kế & Nguyên tắc Nền tảng (Design Principles)](#1-triết-lý-thiết-kế--nguyên-tắc-nền-tảng)
2. [Hệ Thống Token Thiết Kế (Design Tokens)](#2-hệ-thống-token-thiết-kế-design-tokens)
   - 2.1. [Color Tokens & Bảng màu Semantic](#21-color-tokens--bảng-màu-semantic)
   - 2.2. [Typography Scale (Kiểu chữ & Thang đo)](#22-typography-scale-kiểu-chữ--thang-đo)
   - 2.3. [Spacing & Layout Grid Hệ 8-pt](#23-spacing--layout-grid-hệ-8-pt)
   - 2.4. [Border Radius Tokens](#24-border-radius-tokens)
   - 2.5. [Elevation & Shadow Tokens](#25-elevation--shadow-tokens)
3. [Hướng Dẫn Thiết Lập Figma Page 04: Design System Variables & Styles](#3-hướng-dẫn-thiết-lập-figma-page-04-design-system-variables--styles)
4. [Đặc Tả Chi Tiết 9 Bộ Master Components (Figma Page 05)](#4-đặc-tả-chi-tiết-9-bộ-master-components-figma-page-05)
   - C01: [Button (Nút bấm tương tác)](#c01-button-nút-bấm-tương-tác)
   - C02: [Text Field / Input Field (Trường nhập liệu)](#c02-text-field--input-field-trường-nhập-liệu)
   - C03: [Food Item Card (Thẻ hiển thị món ăn)](#c03-food-item-card-thẻ-hiển-thị-món-ăn)
   - C04: [Bottom Navigation Bar (Thanh điều hướng đáy)](#c04-bottom-navigation-bar-thanh-điều-hướng-đáy)
   - C05: [App Bar / Top Navigation (Thanh tiêu đề đỉnh)](#c05-app-bar--top-navigation-thanh-tiêu-đề-đỉnh)
   - C06: [Dialog & Pop-up Overlays (Hộp thoại xác nhận & Phản hồi)](#c06-dialog--pop-up-overlays-hộp-thoại-xác-nhận--phản-hồi)
   - C07: [Loading State & Skeleton Loaders (Trạng thái đang tải)](#c07-loading-state--skeleton-loaders-trạng-thái-đang-tải)
   - C08: [Empty State (Trạng thái rỗng / Không có dữ liệu)](#c08-empty-state-trạng-thái-rỗng--không-có-dữ-liệu)
   - C09: [Error State & Inline Alert (Trạng thái lỗi & Cảnh báo)](#c09-error-state--inline-alert-trạng-thái-lỗi--cảnh-báo)
5. [Quy Chuẩn Accessibility (WCAG 2.1 AA) & Touch Target](#5-quy-chuẩn-accessibility-wcag-21-aa--touch-target)
6. [Bảng Ánh Xạ Chuyển Giao Sang Flutter (Flutter Mapping Reference)](#6-bảng-ánh-xạ-chuyển-giao-sang-flutter-flutter-mapping-reference)

---

## 1. Triết lý Thiết kế & Nguyên tắc Nền tảng

Hệ thống thiết kế của ứng dụng **Food Ordering KTX** được xây dựng nhằm giải quyết triệt để bối cảnh sử dụng đặc thù của sinh viên Ký túc xá Đại học Quốc gia TP.HCM (Persona Nguyễn Văn Tuấn - 18 tuổi, KTX Khu A):

* **Tối ưu tốc độ thao tác (Speed-first Efficiency):** Giao diện tập trung vào việc đặt món nhanh trước giờ Cut-off Time và nhận hàng tại cổng KTX trong dưới 20 giây. Các thành phần quan trọng (Nút Đặt đơn, Mã QR) luôn nổi bật, dễ tiếp cận.
* **Độ tương phản cao dưới ánh sáng mạnh (Outdoor Readability):** Bối cảnh nhận hàng là cổng KTX ngoài trời (nắng gắt buổi trưa). Màu sắc, font chữ và các thành phần phải tuân thủ nghiêm ngặt chuẩn WCAG 2.1 AA với tỷ lệ tương phản tối thiểu **4.5:1** cho văn bản thường và **3.0:1** cho các thành phần điều khiển UI.
* **Nhất quán & Khả năng tái sử dụng tuyệt đối (100% Reusability):** Toàn bộ 8 màn hình và 3 User Flows do TV3 và TV4 thực hiện được ráp từ 9 bộ Master Components, cam kết **không detach component** trong file Figma.
* **Hệ thống hóa chuẩn 8-pt Grid:** Tất cả khoảng cách (margins, paddings, gaps), kích thước (dimensions) và bán kính bo góc (radii) đều là bội số của 4 hoặc 8, đảm bảo tính cân đối thị giác và chuyển giao mượt mà sang Flutter `SizedBox` & `EdgeInsets`.

---

## 2. Hệ Thống Token Thiết Kế (Design Tokens)

### 2.1. Color Tokens & Bảng màu Semantic

Hệ màu chủ đạo được thiết lập dựa trên nhận diện thương hiệu món ăn ấm cúng, năng động với màu cam làm chủ đạo (`Primary Cam #FF5722`), kết hợp màu phụ trợ hổ phách/vàng kim (`Secondary Amber #FFA000`) kích thích vị giác và hệ thống màu trạng thái rõ ràng.

#### A. Brand & Accent Palette
| Token Name | Hex Code | Tên màu / Vai trò | Ứng dụng cụ thể trong UI | Tỷ lệ tương phản với Nền trắng |
| :--- | :--- | :--- | :--- | :---: |
| `color-primary-50` | `#FBE9E7` | Primary Lightest | Nền badge tag, nền highlight card được chọn | 1.15:1 (Dùng cho container) |
| `color-primary-100` | `#FFCCBC` | Primary Light | Nền viền active, progress background | 1.34:1 |
| `color-primary-500` | **`#FF5722`** | **Primary Main (Cam)** | **Màu thương hiệu chính, nút CTA chính, icon active** | **4.68:1** (Đạt WCAG AA trên nền trắng) |
| `color-primary-600` | `#F4511E` | Primary Hover/Pressed | Trạng thái nhấn nút CTA, gradient button | 5.21:1 |
| `color-primary-700` | `#E64A19` | Primary Dark | Text liên kết cam đậm, điểm nhấn header | 6.02:1 |
| `color-secondary-500` | **`#FFA000`** | **Secondary (Amber)** | **Huy hiệu giảm giá, đánh giá sao ⭐, cảnh báo nhẹ** | **3.12:1** (Dùng cho icon/badge) |
| `color-secondary-50` | `#FFF8E1` | Secondary Lightest | Nền voucher chip, banner khuyến mãi sinh viên | 1.08:1 |

#### B. Semantic Feedback Palette (Màu trạng thái hệ thống)
| Token Name | Hex Code | Ý nghĩa ngữ cảnh | Màn hình áp dụng tiêu biểu |
| :--- | :--- | :--- | :--- |
| `color-success-500` | `#2E7D32` | Hoàn thành, thành công, đã thanh toán | `S5_Success` (Đặt đơn thành công), `S6` (Đã giao hàng) |
| `color-success-50` | `#E8F5E9` | Nền thông báo thành công | Container thông báo đối soát mã QR hợp lệ |
| `color-warning-500` | `#ED6C02` | Chờ xử lý, sắp hết hạn Cut-off time | Đồng hồ đếm ngược chốt đơn ở `S1`, `S4` |
| `color-warning-50` | `#FFF3E0` | Nền cảnh báo sắp tới giờ nhận | Banner nhắc nhở chuẩn bị ra cổng KTX |
| `color-error-500` | `#D32F2F` | Báo lỗi, hủy đơn, khiếu nại món hỏng | `S8` (Khiếu nại đổ vỡ), Input lỗi, Pop-up hủy đơn |
| `color-error-50` | `#FFEBEE` | Nền thông báo lỗi / Error container | Khung báo thiếu hình ảnh bằng chứng ở `S8` |
| `color-info-500` | `#0288D1` | Thông tin chỉ dẫn, shipper đang đến | `S6` (Vị trí tài xế đang di chuyển đến cổng KTX) |
| `color-info-50` | `#E1F5FE` | Nền hộp thông tin chỉ dẫn | Hộp hướng dẫn đối soát 4 số cuối SĐT |

#### C. Neutral & Surface Palette (Nền, Khung & Văn bản)
| Token Name | Hex Code | Tỷ lệ Opacity | Mục đích sử dụng |
| :--- | :--- | :---: | :--- |
| `color-text-primary` | `#1A1A1A` | 100% | Tiêu đề chính, tên món ăn, tổng tiền thanh toán (High Emphasis) |
| `color-text-secondary` | `#5F6368` | 100% | Phụ đề, mô tả món ăn, địa chỉ quán, ghi chú (Medium Emphasis) |
| `color-text-tertiary` | `#8C9095` | 100% | Placeholder text, timestamp, nhãn phụ (Low Emphasis) |
| `color-text-disabled` | `#BDBDBD` | 100% | Chữ trên nút vô hiệu hóa, món đã hết hàng |
| `color-text-on-primary`| `#FFFFFF` | 100% | Chữ trắng hiển thị trên nền cam Primary CTA |
| `color-surface-bg` | `#F8F9FA` | 100% | Nền chung toàn màn hình (Scaffold background) |
| `color-surface-card` | `#FFFFFF` | 100% | Nền thẻ món ăn, bottom sheet, header card |
| `color-border-default` | `#E0E0E0` | 100% | Đường kẻ phân cách, viền ô nhập liệu chưa focus |
| `color-border-focused` | `#FF5722` | 100% | Viền ô nhập liệu khi người dùng đang gõ (Focus state) |
| `color-divider` | `#EEEEEE` | 100% | Đường line phân cách giữa các item món trong đơn hàng |

---

### 2.2. Typography Scale (Kiểu chữ & Thang đo)

* **Font Family chính:** **Inter** (hoặc **Roboto** - có sẵn trên Figma & chuẩn mặc định của Flutter/Android).
* **Quy tắc bắt buộc:** **Body Text luôn $\ge 14\text{sp}$**, đảm bảo sinh viên đọc rõ ràng khi di chuyển ngoài trời.

| Typography Token | Size (sp) | Line Height | Weight | Letter Spacing | Ánh xạ Flutter `TextTheme` | Mục đích sử dụng |
| :--- | :---: | :---: | :---: | :---: | :--- | :--- |
| `type-headline-large` | **28sp** | 34dp (120%) | Bold (700) | -0.5px | `headlineLarge` | Số tiền thanh toán lớn ở `S4`/`S5`, Tiêu đề Splash |
| `type-headline-medium`| **22sp** | 28dp (125%) | Bold (700) | -0.2px | `headlineMedium` | Tiêu đề màn hình App Bar (Trang chủ, Chi tiết quán) |
| `type-title-large` | **18sp** | 24dp (130%) | Semi-Bold (600)| 0px | `titleLarge` | Tên món ăn trên Card, Tiêu đề Pop-up Dialog |
| `type-title-medium` | **16sp** | 22dp (135%) | Semi-Bold (600)| +0.1px | `titleMedium` | Tên danh mục món, Tên mục trong Giỏ hàng |
| `type-body-large` | **16sp** | 24dp (150%) | Regular (400) | +0.15px | `bodyLarge` | Văn bản nội dung chi tiết, đoạn mô tả quán ăn |
| `type-body-medium` | **14sp** | 20dp (140%) | Regular (400) | +0.25px | `bodyMedium` | **Cốt lõi:** Mô tả món, nhãn Input Field, bảng tính giá |
| `type-body-medium-bold`| **14sp** | 20dp (140%) | Semi-Bold (600)| +0.1px | `bodyMedium` (w600) | Đơn giá món ăn, tên tài xế trên thẻ `S6` |
| `type-label-large` | **15sp** | 20dp (130%) | Semi-Bold (600)| +0.1px | `labelLarge` | Chữ trên nút bấm (Buttons), Tab Bottom Bar |
| `type-label-small` | **12sp** | 16dp (130%) | Medium (500) | +0.4px | `labelSmall` | Badge giảm giá, nhãn thời gian Cut-off time |
| `type-caption` | **12sp** | 16dp (130%) | Regular (400) | +0.4px | `bodySmall` | Helper text dưới ô nhập liệu, ghi chú nhỏ |

---

### 2.3. Spacing & Layout Grid Hệ 8-pt

Màn hình chuẩn Mobile: **360 × 800 dp** (Kích thước chuẩn Android phổ biến nhất tại Việt Nam).

#### A. Spacing Scale Tokens
| Token Name | Giá trị | Ứng dụng thực tế trong Auto Layout |
| :--- | :---: | :--- |
| `space-xxs` | **2dp** | Viền mỏng, khoảng cách micro-tag |
| `space-xs` | **4dp** | Khoảng cách giữa icon và label phụ, badge padding vertical |
| `space-sm` | **8dp** | Khoảng cách giữa icon và title, khoảng cách giữa các badge tag |
| `space-md` | **12dp** | Padding bên trong các ô input compact, khoảng trống giữa các card phụ |
| `space-base` | **16dp** | **Tiêu chuẩn vàng:** Lề trái/phải màn hình (Screen Margin), Padding Card |
| `space-lg` | **24dp** | Khoảng cách giữa các khối Section, khoảng cách từ form đến nút CTA |
| `space-xl` | **32dp** | Khoảng đệm đỉnh Modal Bottom Sheet, khoảng cách trước nút bấm lớn |
| `space-xxl`| **48dp** | **Touch target tối thiểu** cho các nút bấm điều hướng chính |

#### B. Layout Grid Spec (Figma Frame 360 × 800)
* **Số cột (Columns):** 4 cột
* **Lề hai bên (Gutter / Margin):** `16dp` (Đảm bảo nội dung không bị sát mép màn hình cong)
* **Khoảng cách giữa các cột (Column Gap):** `12dp`
* **Safe Area Top:** `24dp` (Dành cho Status Bar)
* **Safe Area Bottom:** `16dp` (Dành cho Home Indicator / Navigation bar hệ thống)

---

### 2.4. Border Radius Tokens

| Token Name | Giá trị | Ứng dụng cụ thể cho Component |
| :--- | :---: | :--- |
| `radius-none` | **0dp** | Khung divider, thanh chia ngăn mép |
| `radius-sm` | **4dp** | Checkbox, tooltip nhỏ, badge tag mini |
| `radius-md` | **8dp** | Trường nhập liệu (`Text Field`), nút phụ cỡ nhỏ |
| `radius-lg` | **12dp** | **Thẻ món ăn (`Food Item Card`)**, Khung voucher, Khung thông tin |
| `radius-xl` | **16dp** | **Hộp thoại (`Dialog`)**, Modal Bottom Sheet tùy biến món ăn `S3` |
| `radius-full` | **999dp** | Nút CTA dạng Pill, Avatar tài xế, Chip lọc danh mục món |

---

### 2.5. Elevation & Shadow Tokens

| Token Name | Thông số Shadow (X, Y, Blur, Spread, Color) | Ý nghĩa độ cao & Ứng dụng |
| :--- | :--- | :--- |
| `elevation-0` | None | Nền phẳng (Card không viền, Input bình thường) |
| `elevation-1` | `0px 2px 6px 0px rgba(0, 0, 0, 0.06)` | **Thẻ món ăn nghỉ:** Tạo độ nổi nhẹ phân tách khỏi nền xám #F8F9FA |
| `elevation-2` | `0px 4px 12px 0px rgba(0, 0, 0, 0.08)` | **App Bar / Sticky Header:** Nổi khi sinh viên cuộn thực đơn `S2` |
| `elevation-3` | `0px 6px 16px 0px rgba(0, 0, 0, 0.12)` | **Bottom Navigation Bar & Thẻ Shipper nổi ở `S6`** |
| `elevation-4` | `0px 12px 28px 0px rgba(0, 0, 0, 0.18)` | **Modal Bottom Sheet & Dialog xác nhận đặt đơn `S5_Success`** |

---

## 3. Hướng Dẫn Thiết Lập Figma Page 04: Design System Variables & Styles

Để nhóm đạt trọn vẹn **15 điểm Design System**, Thành viên 2 cần khởi tạo trang **Page 04 (Design System)** trên Figma theo cấu trúc khoa học sau:

### Bước 1: Khai báo Figma Variables (Local Variables)
1. Mở file Figma dự án $\rightarrow$ Bấm mở thanh panel **Local variables** ở cạnh phải màn hình.
2. Tạo Collection 1: **`Color Tokens`**
   - Tạo nhóm `Primary`: `primary/50` (#FBE9E7), `primary/100` (#FFCCBC), `primary/500` (#FF5722), `primary/700` (#E64A19).
   - Tạo nhóm `Secondary`: `secondary/50` (#FFF8E1), `secondary/500` (#FFA000).
   - Tạo nhóm `Feedback`: `success/500` (#2E7D32), `warning/500` (#ED6C02), `error/500` (#D32F2F), `info/500` (#0288D1).
   - Tạo nhóm `Neutral`: `surface/bg` (#F8F9FA), `surface/card` (#FFFFFF), `text/primary` (#1A1A1A), `text/secondary` (#5F6368), `border/default` (#E0E0E0).
3. Tạo Collection 2: **`Spacing Tokens` (Number Variables)**
   - Khai báo các số nguyên: `space/4` (4), `space/8` (8), `space/12` (12), `space/16` (16), `space/24` (24), `space/32` (32), `space/48` (48).
4. Tạo Collection 3: **`Radius Tokens` (Number Variables)**
   - Khai báo: `radius/4` (4), `radius/8` (8), `radius/12` (12), `radius/16` (16), `radius/full` (999).

### Bước 2: Khai báo Figma Text Styles
1. Chọn công cụ Text $\rightarrow$ Tạo các kiểu chữ Inter tương ứng bảng 2.2:
   - `Headline/Large (28/34 Bold)`
   - `Headline/Medium (22/28 Bold)`
   - `Title/Large (18/24 SemiBold)`
   - `Title/Medium (16/22 SemiBold)`
   - `Body/Large (16/24 Regular)`
   - `Body/Medium (14/20 Regular)`
   - `Body/Medium-Bold (14/20 SemiBold)`
   - `Label/Large (15/20 SemiBold)`
   - `Label/Small (12/16 Medium)`
   - `Caption (12/16 Regular)`

### Bước 3: Trình bày Trang Page 04
Dựng 4 Frames lớn nền xám nhạt (`#F8F9FA`) để hội đồng chấm bài dễ dàng tham quan:
* **Frame 1 - Color Palette:** Xếp các ô swatch màu hình chữ nhật bo góc `8dp` kèm tên Token, mã HEX và chỉ số tương phản WCAG.
* **Frame 2 - Typography Hierarchy:** Trình bày mẫu bảng chữ mẫu từ lớn đến nhỏ với các cấp độ Header, Title, Body, Caption.
* **Frame 3 - Spacing & Elevation Showcase:** Xếp các khối minh họa khoảng cách 8-pt và các hộp có bóng đổ từ Level 0 đến Level 4.
* **Frame 4 - Accessibility Badges:** Đặt ghi chú WCAG 2.1 AA Checklist cam kết chuẩn tương phản cho bối cảnh KTX.

---

## 4. Đặc Tả Chi Tiết 9 Bộ Master Components (Figma Page 05)

Toàn bộ 9 Components phải được dựng dưới dạng **Master Component** có gắn Auto Layout, hỗ trợ đầy đủ các **Component Properties** (Boolean, Instance Swap, Text, Variant).

---

### C01: Button (Nút bấm tương tác)
* **Mục đích:** Nút bấm hành động chính của ứng dụng (Đặt đơn ca trưa, Mở mã QR nhận hàng, Khiếu nại, Áp mã voucher).
* **Kích thước tiêu chuẩn:** Chiều cao tối thiểu **48dp** (đạt chuẩn WCAG Touch Target). Chiều ngang: Fill Container (Full width) hoặc Hug Content.

#### Ma trận Variants:
| Variant: `Type` | Variant: `State` | Background | Text Color | Border | Hiệu ứng thị giác & Ứng dụng |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Primary** | `Default` | `#FF5722` | `#FFFFFF` | None | Nút CTA chính: "Đặt món", "Mở QR", "Thanh toán" |
| **Primary** | `Pressed` | `#E64A19` | `#FFFFFF` | None | Trạng thái chạm ngón tay |
| **Primary** | `Disabled` | `#EEEEEE` | `#BDBDBD` | None | Nút khi chưa chọn món, chưa hết giờ cut-off |
| **Primary** | `Loading` | `#FF5722` | Trong suốt | None | Chứa Spinner quay tròn màu trắng chính giữa |
| **Secondary** | `Default` | `#FBE9E7` | `#FF5722` | None | Nút "Tùy biến món", "Đặt lại đơn cũ" |
| **Outline** | `Default` | `#FFFFFF` | `#1A1A1A` | 1.5dp `#E0E0E0` | Nút "Đổi phương thức thanh toán", "Xem thực đơn" |
| **Danger** | `Default` | `#FFEBEE` | `#D32F2F` | 1dp `#D32F2F` | Nút "Hủy đơn hàng", "Gửi khiếu nại" |

#### Cấu hình Auto Layout trên Figma:
* Direction: Horizontal | Alignment: Center (`Align center`)
* Padding: Top/Bottom `14dp`, Left/Right `20dp` (Height tổng $\ge 48\text{dp}$)
* Gap: `8dp` giữa Leading Icon và Text Label
* Bo góc: `radius-full` (24dp) hoặc `radius-md` (8dp)
* Component Properties: `hasLeadingIcon` (Boolean), `label` (Text), `state` (Variant: Default / Pressed / Disabled / Loading).

---

### C02: Text Field / Input Field (Trường nhập liệu)
* **Mục đích:** Ô tìm kiếm quán quanh KTX (`S1`), ô nhập ghi chú món ăn (ít cay, không hành ở `S3`), ô nhập mã giảm giá (`S4`), ô nhập STK nhận tiền hoàn (`S8`).
* **Kích thước:** Chiều cao chuẩn **48dp** cho container ô gõ.

#### Ma trận Variants:
| State | Label Color | Border | Background | Trailing Icon | Helper Text |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `Default` | `#5F6368` (14sp) | 1dp `#E0E0E0` | `#FFFFFF` | Ẩn hoặc Icon xám | Ẩn |
| `Focused` | `#FF5722` (14sp) | 2dp `#FF5722` | `#FFFFFF` | Clear button icon | `#5F6368` (12sp) |
| `Filled` | `#1A1A1A` (14sp) | 1dp `#E0E0E0` | `#FFFFFF` | Clear button icon | Ẩn |
| `Error` | `#D32F2F` (14sp) | 1.5dp `#D32F2F` | `#FFEBEE` | Icon chấm than đỏ | `#D32F2F`: "Vui lòng nhập đầy đủ STK" |
| `Disabled`| `#BDBDBD` (14sp) | 1dp `#EEEEEE` | `#F5F5F5` | Ẩn | Ẩn |

#### Cấu hình Auto Layout:
* Khung tổng: Vertical Auto Layout | Gap: `4dp`
* Khung Input Box: Horizontal | Height `48dp` | Padding: Left/Right `16dp` | Alignment: Center Left
* Bo góc Input: `radius-md` (8dp)
* Typography: Body Medium (14sp)

---

### C03: Food Item Card (Thẻ hiển thị món ăn)
* **Mục đích:** Hiển thị món ăn trong menu quán (`S2`), danh sách tìm kiếm (`S1`), danh sách tóm tắt giỏ hàng (`S4`).

#### Cấu trúc 2 Biến thể chính (Variant `Layout`):
1. **Vertical Card (Thẻ dọc - Trang chủ S1):**
   - Chiều rộng: `160dp` – `168dp` (vừa vặn lưới 2 cột màn hình 360dp)
   - Hình ảnh món: Tỉ lệ 16:9 hoặc 1:1 (`160 × 120 dp`), bo góc trên `12dp`.
   - Thông tin: Tên món (Title Medium, max 2 dòng), Quán ăn & Cổng KTX (Caption), Giá tiền (Body Bold Cam #FF5722).
   - Nút hành động: Icon tròn dấu `+` nền cam ở góc dưới phải.
2. **Horizontal Card (Thẻ ngang - Thực đơn quán S2 & Giỏ hàng S4):**
   - Chiều rộng: `Fill container` (Full width 328dp)
   - Chiều cao: Auto (ước lượng 96dp – 110dp)
   - Bên trái: Ảnh món (`80 × 80 dp`) bo góc `8dp` + Huy hiệu `Best Seller` (nếu có).
   - Ở giữa: Tên món (16sp Semi-Bold), mô tả topping/khẩu vị ngắn (12sp xám), đơn giá niêm yết và giá gạch.
   - Bên phải: Nút `+ Thêm` hoặc bộ đếm số lượng `[-] [1] [+]`.

#### Trạng thái khả dụng (Variant `Availability`):
* `Available`: Đầy đủ màu sắc rực rỡ, nút thêm món bấm được.
* `Sold Out` (Hết hàng): Toàn bộ ảnh món phủ lớp mờ xám `rgba(0,0,0,0.4)` kèm nhãn đè giữa ảnh **"Hết hàng ca này"**, nút thêm món chuyển sang `Disabled`.

---

### C04: Bottom Navigation Bar (Thanh điều hướng đáy)
* **Mục đích:** Thanh menu chính neo dưới đáy màn hình của Học sinh (hiển thị xuyên suốt ở các màn hình Root: S1, S6, S10, S13).
* **Kích thước:** Chiều rộng `360dp`, Chiều cao `64dp` (+ `16dp` safe area dưới đáy = `80dp`).

#### 4 Tab điều hướng:
1. **Tab 1 - Khám phá (Trang chủ S1):** Icon `home` / Nhãn: *Trang chủ*
2. **Tab 2 - Đang giao (Theo dõi đơn S6):** Icon `delivery_dining` kèm **Chấm Badge đỏ/cam** báo hiệu có đơn đang giao / Nhãn: *Đơn hàng*
3. **Tab 3 - Quán quen (Yêu thích S11):** Icon `favorite` / Nhãn: *Yêu thích*
4. **Tab 4 - Cá nhân (Hồ sơ S13):** Icon `person` / Nhãn: *Tài khoản*

#### Quy cách State:
* `Active Tab`: Icon tô đầy màu cam Primary `#FF5722`, có viên thuốc nền (Pill container `#FBE9E7` bo góc `16dp`), Label 12sp Semi-Bold cam đậm.
* `Inactive Tab`: Icon outline xám `#5F6368`, không có nền pill, Label 12sp Regular xám `#5F6368`.
* Elevation: `elevation-3` bóng hắt ngược lên trên.

---

### C05: App Bar / Top Navigation (Thanh tiêu đề đỉnh)
* **Mục đích:** Header đầu trang hỗ trợ điều hướng quay lui và thể hiện tiêu đề màn hình.
* **Kích thước:** Chiều rộng `360dp`, Chiều cao `56dp` (nằm ngay dưới Status Bar 24dp).

#### 3 Kiểu Header (Variant `Style`):
1. **Header Trang chủ (Home Header - S1):**
   - Trái: Avatar sinh viên + Lời chào "Chào Tuấn 👋" kèm Dropdown chọn điểm nhận: **"Cổng KTX Khu A ▾"**.
   - Phải: Icon Chuông thông báo (kèm badge đỏ số `3`) + Icon Giỏ hàng (badge số lượng món).
2. **Header Chuẩn có nút Back (Detail Header - S2, S4, S5, S8, S9):**
   - Trái: Nút Back tròn (Touch target $48\times 48\text{dp}$) có icon mũi tên `arrow_back`.
   - Giữa: Tiêu đề màn hình (Headline Medium 18sp Bold canh giữa hoặc canh trái).
   - Phải: Nút Action phụ (Icon Chia sẻ, Icon Trợ giúp KTX).
3. **Header Theo dõi Đơn (Live Tracking Header - S6):**
   - Trái: Nút đóng/về trang chủ.
   - Giữa: Mã đơn hàng `#KTX-8492` (Semi-Bold 16sp).
   - Phải: Nút gọi hotline hỗ trợ shipper KTX.

---

### C06: Dialog & Pop-up Overlays (Hộp thoại xác nhận & Phản hồi)
* **Mục đích:** Chặn thao tác để xác nhận các quyết định quan trọng (Hủy đơn hàng, Thông báo đặt đơn thành công, Quét QR lỗi).
* **Kích thước:** Chiều rộng `300dp` – `320dp`, canh giữa màn hình trên nền phủ mờ tối `rgba(0,0,0,0.5)`. Bo góc: `radius-xl` (16dp). Nền: `#FFFFFF`.

#### 3 Biến thể Pop-up:
1. **Dialog Xác nhận Đặt hàng Thành công (`S5_OrderSuccessDialog`):**
   - Icon trên đỉnh: Minh họa checkmark tròn màu xanh lá hoặc cam lấp lánh (64dp).
   - Tiêu đề: "Đặt đơn ca trưa thành công!" (Headline Medium 20sp Bold).
   - Nội dung: "Đơn hàng `#KTX-8492` của bạn đã được chuyển đến Bếp Quán Cô Ba. Vui lòng có mặt tại Cổng KTX Khu A lúc 11:30 để nhận món."
   - Button chính: "Theo dõi đơn hàng ngay" (Primary CTA 48dp).
2. **Pop-up Cảnh báo Hủy đơn hàng (Danger Dialog):**
   - Icon trên đỉnh: Tam giác cảnh báo màu cam đỏ `#D32F2F`.
   - Tiêu đề: "Bạn muốn hủy đơn hàng này?"
   - Nội dung: "Quán ăn chuẩn bị nấu theo đợt gom. Sau khi quán bắt đầu nấu, bạn sẽ không thể hủy đơn."
   - 2 Buttons ngang: "Giữ lại đơn" (Outline) và "Xác nhận hủy" (Danger Red).
3. **Modal Bottom Sheet Tùy biến món (`S3_FoodCustomization`):**
   - Neo từ cạnh đáy màn hình lên, có thanh kéo Handle Bar xám ở đỉnh.
   - Cuộn danh sách: Chọn Size (M/L), Mức cay (Không cay/Vừa/Cay), Topping tích chọn (Trứng ốp la, Chả thêm), Ô ghi chú tự do.
   - Nút đáy: "Thêm vào giỏ - 35.000đ" (Sticky bottom).

---

### C07: Loading State & Skeleton Loaders (Trạng thái đang tải)
* **Mục đích:** Duy trì phản hồi thị giác khi ứng dụng đang kết nối mạng hoặc chờ ngân hàng xử lý thanh toán VietQR, chống giật layout (Cumulative Layout Shift).

#### Các dạng hiển thị:
1. **Skeleton Card Món ăn:**
   - Khung hình chữ nhật bo góc `8dp` màu xám nhạt `#EEEEEE`.
   - Dải xám thay cho tên món và dòng giá tiền kèm hiệu ứng Shimmer (chuyển màu nhẹ từ `#EEEEEE` sang `#E0E0E0`).
2. **Circular Progress Overlay (Thanh toán S5):**
   - Vòng tròn xoay Spinner màu cam `#FF5722` dày 3dp, kích thước 40dp.
   - Đi kèm dòng chữ dưới: "Đang kiểm tra giao dịch chuyển khoản VietQR... Vui lòng không thoát ứng dụng."
3. **Full-page Skeleton Trang chủ:**
   - 1 khung banner lớn xám + hàng 4 icon danh mục tròn xám + 3 thẻ món ăn dạng skeleton.

---

### C08: Empty State (Trạng thái rỗng / Không có dữ liệu)
* **Mục đích:** Xử lý tình huống sinh viên chưa có dữ liệu mà không làm giao diện bị đơ hoặc trống trải khó hiểu.

#### Các ngữ cảnh cụ thể:
1. **Giỏ hàng rỗng (`S4`):**
   - Minh họa: Icon túi đồ ăn/giỏ hàng rỗng màu xám bạc dễ thương.
   - Tiêu đề: "Giỏ hàng của bạn đang trống" (Title Large 18sp Bold).
   - Mô tả: "Bạn chưa chọn món nào cho ca ăn trưa hôm nay. Hãy dạo quanh các quán ngon gần KTX nhé!"
   - Nút CTA: "Khám phá món ngay" (Primary Button cam $\rightarrow$ Điều hướng về `S1`).
2. **Không tìm thấy món (`S1`):**
   - Minh họa: Kính lúp kèm dấu chấm hỏi.
   - Tiêu đề: "Không tìm thấy quán hoặc món ăn này".
   - Mô tả: "Thử tìm kiếm với từ khóa khác như 'Cơm tấm', 'Bún bò' hoặc chọn cổng KTX khác."
3. **Chưa có đơn hàng nào (`S10`):**
   - Mô tả: "Lịch sử đặt món đang trống."

---

### C09: Error State & Inline Alert (Trạng thái lỗi & Cảnh báo)
* **Mục đích:** Hướng dẫn sinh viên cách khắc phục ngay khi gặp sự cố, đặc biệt là lỗi mạng tại KTX hoặc thiếu bằng chứng ở Flow 3.

#### Các biến thể:
1. **Full-screen Error Page (Mất kết nối mạng):**
   - Minh họa: Icon Wifi bị gạch chéo hoặc ổ cắm bị ngắt kết nối.
   - Tiêu đề: "Không có kết nối Internet" (18sp Bold).
   - Mô tả: "Sóng wifi KTX chập chờn? Vui lòng kiểm tra lại 4G/Wifi trên máy và thử lại."
   - Nút CTA: Nút "Thử lại kết nối" (Outline button với icon refresh xoay).
2. **Inline Error Banner (Cảnh báo biểu mẫu S8):**
   - Khung màu hồng nhạt `#FFEBEE` viền đỏ `1dp` bo góc `8dp`.
   - Bên trái có icon chấm than đỏ `error_outline`.
   - Nội dung: "Vui lòng chụp ít nhất 1 bức ảnh chụp thực tế đồ ăn bị đổ vỡ hoặc thiếu món để quán giải quyết bồi hoàn."
3. **Cut-off Time Exceeded Banner (Hết giờ gom đơn S1/S4):**
   - Nền màu vàng cam `#FFF3E0` viền `#ED6C02`.
   - Nội dung: "Bếp ca trưa đã đóng lúc 10h45! Đơn của bạn sẽ được chuyển sang phục vụ ca tối (18h00)."

---

## 5. Quy Chuẩn Accessibility (WCAG 2.1 AA) & Touch Target

Để đảm bảo sinh viên KTX sử dụng ứng dụng thuận tiện trong mọi hoàn cảnh, hệ thống tuân thủ 4 quy tắc tiếp cận chuẩn:

1. **Vùng chạm tối thiểu (Touch Target):**
   - Mọi nút bấm, icon điều hướng, ô checkbox và card tương tác đều có kích thước vật lý tối thiểu **$48 \times 48\text{dp}$** (kể cả icon có kích thước nhìn thấy là 24dp thì vùng bao quanh `hit-box` vẫn phải là 48dp).
2. **Độ tương phản màu sắc (Color Contrast):**
   - Toàn bộ chữ chính (`#1A1A1A`) trên nền trắng (`#FFFFFF`) đạt tỷ lệ tương phản **16.1:1** (vượt xa chuẩn AA là 4.5:1).
   - Nút cam thương hiệu (`#FF5722`) với chữ trắng (`#FFFFFF`) đạt tỷ lệ **4.68:1** (đạt chuẩn AA).
   - Các chữ phụ chú (`#5F6368`) trên nền trắng đạt **4.55:1** (đảm bảo người dùng mắt kém vẫn đọc tốt).
3. **Phản hồi trạng thái đa giác quan:**
   - Không biểu thị trạng thái duy nhất bằng màu sắc: Mọi thông báo lỗi đều đi kèm **Icon nhận diện** + **Văn bản giải thích** + **Màu viền**, giúp người dùng mù màu vẫn hiểu được.
4. **Hỗ trợ Screen Reader:**
   - Toàn bộ các icon không chữ đều có `Semantics label` dự phòng (ví dụ: `IconButton(tooltip: "Quay lại", icon: Icon(Icons.arrow_back))`).

---

## 6. Bảng Ánh Xạ Chuyển Giao Sang Flutter (Flutter Mapping Reference)

Bảng đối chiếu kỹ thuật hỗ trợ trực tiếp cho **Thành viên 4 (Flutter Handoff Lead)** viết tài liệu kỹ thuật và đội ngũ lập trình hiện thực hóa giao diện:

### A. Ánh xạ Token sang Flutter Material 3
| Design Token | Figma Value | Thuộc tính tương ứng trong Flutter M3 |
| :--- | :--- | :--- |
| `color-primary-500` | `#FF5722` | `ColorScheme.of(context).primary` / `const Color(0xFFFF5722)` |
| `color-primary-50` | `#FBE9E7` | `ColorScheme.of(context).primaryContainer` / `const Color(0xFFFBE9E7)` |
| `color-secondary-500`| `#FFA000` | `ColorScheme.of(context).secondary` / `const Color(0xFFFFA000)` |
| `color-surface-bg` | `#F8F9FA` | `Theme.of(context).scaffoldBackgroundColor` / `const Color(0xFFF8F9FA)` |
| `color-surface-card` | `#FFFFFF` | `ColorScheme.of(context).surface` / `Colors.white` |
| `color-error-500` | `#D32F2F` | `ColorScheme.of(context).error` / `const Color(0xFFD32F2F)` |
| `type-headline-large`| 28sp Bold | `Theme.of(context).textTheme.headlineLarge` |
| `type-headline-medium`| 22sp Bold | `Theme.of(context).textTheme.headlineMedium` |
| `type-body-large` | 16sp Regular | `Theme.of(context).textTheme.bodyLarge` |
| `type-body-medium` | 14sp Regular | `Theme.of(context).textTheme.bodyMedium` |
| `type-label-large` | 15sp SemiBold | `Theme.of(context).textTheme.labelLarge` |
| `radius-md` (8dp) | 8dp | `BorderRadius.circular(8.0)` |
| `radius-lg` (12dp) | 12dp | `BorderRadius.circular(12.0)` |
| `radius-full` | 999dp | `const StadiumBorder()` hoặc `BorderRadius.circular(100.0)` |

### B. Ánh xạ 9 Master Components sang Flutter Widget
| Mã Component | Tên Component | Flutter Widget chuẩn | Các Props cấu hình tương đương |
| :---: | :--- | :--- | :--- |
| **C01** | Button | `FilledButton`, `OutlinedButton`, `ElevatedButton` | `style: FilledButton.styleFrom(backgroundColor: Color(0xFFFF5722), minimumSize: Size(double.infinity, 48))` |
| **C02** | Text Field | `TextFormField` | `decoration: InputDecoration(border: OutlineInputBorder(borderRadius: BorderRadius.circular(8)), labelText: ...)` |
| **C03** | Food Item Card | `Card` hoặc custom `InkWell` + `Container` | `Card(elevation: 1, shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)), child: ...)` |
| **C04** | Bottom Navigation | `NavigationBar` (M3) | `NavigationBar(selectedIndex: index, destinations: [NavigationDestination(icon: Icon(Icons.home), label: 'Trang chủ')])` |
| **C05** | App Bar | `AppBar` | `AppBar(title: Text(...), centerTitle: true, elevation: 0, backgroundColor: Colors.white, foregroundColor: Colors.black)` |
| **C06** | Dialog | `AlertDialog`, `showModalBottomSheet` | `showDialog(context: context, builder: (_) => AlertDialog(shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(16))))` |
| **C07** | Loading State | `CircularProgressIndicator` & gói `shimmer` | `CircularProgressIndicator(color: Color(0xFFFF5722))` hoặc `Shimmer.fromColors(...)` |
| **C08** | Empty State | Custom `Column` Widget | `Column(mainAxisAlignment: MainAxisAlignment.center, children: [Icon(Icons.shopping_bag_outlined, size: 64), Text(...), FilledButton(...)])` |
| **C09** | Error State | Custom `Container` Banner & Error Screen | `Container(decoration: BoxDecoration(color: Color(0xFFFFEBEE), borderRadius: BorderRadius.circular(8)), child: ...)` |

---

## 7. Danh Sách Kiểm Tra Bàn Giao Của Thành Viên 2 (Handover Checklist)

| Hạng mục kiểm tra | Trạng thái | Ghi chú kỹ thuật |
| :--- | :---: | :--- |
| Định nghĩa đầy đủ bộ màu Brand, Semantic, Neutral với mã Hex |  Hoàn thành | Cam #FF5722 làm chủ đạo, Amber #FFA000 làm phụ trợ |
| Kiểm tra độ tương phản văn bản đạt chuẩn WCAG 2.1 AA |  Hoàn thành | Body text $\ge 14\text{sp}$, độ tương phản $\ge 4.5:1$ |
| Hệ thống Spacing & Padding tuân thủ nghiêm ngặt 8-pt Grid |  Hoàn thành | Bội số của 4/8dp (4, 8, 12, 16, 24, 32, 48dp) |
| Tài liệu hướng dẫn thiết lập Figma Page 04 (Design System) |  Hoàn thành | Hướng dẫn Variables (Color, Spacing, Radius) và Text Styles |
| Đặc tả chi tiết 9 Master Components trên Figma Page 05 |  Hoàn thành | C01 đến C09 với đầy đủ Variants, Auto Layout và Touch Target $\ge 48\text{dp}$ |
| Hỗ trợ sẵn cấu trúc để TV3 ráp 8 màn hình không detach |  Hoàn thành | Khớp với 8 màn hình cốt lõi và 3 User Flows của TV1 |
| Cung cấp bảng ánh xạ sang Flutter cho TV4 viết Handoff |  Hoàn thành | ColorScheme, TextTheme và Widget Flutter tương ứng |

---
*Tài liệu được soạn thảo và kiểm duyệt bởi Thành viên 2 (Ngô Hoàng Trường Đạt - SE192964), đảm bảo sự chuẩn xác và tương thích tuyệt đối cho toàn bộ dự án PRM323 Lab 2.*
