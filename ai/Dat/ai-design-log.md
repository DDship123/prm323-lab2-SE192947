# NHẬT KÝ THIẾT KẾ & SỬ DỤNG AI (AI DESIGN LOG)
## DỰ ÁN: FOOD ORDERING APP – SINH VIÊN KÝ TÚC XÁ ĐHQG-HCM (PRM323 - LAB 2)

---

# PHẦN 1: THÀNH VIÊN 2 – THIẾT KẾ 9 BỘ MASTER COMPONENTS BẰNG AI
> **Người thực hiện:** Thành viên 2 – Ngô Hoàng Trường Đạt (MSSV: SE192964)  
> **Vai trò:** Design System & Components Specialist  
> **Phạm vi AI phụ trách:** Tạo lập, phản biện và tối ưu 9 Master Components (Button, Text Field, Food Card, Bottom Navigation, App Bar, Dialog, Loading State, Empty State, Error State) theo 5 tiêu chuẩn Rubric của đề bài.

---

## 1. KHAI BÁO CÔNG CỤ AI ĐÃ SỬ DỤNG (TOOL DECLARATION)
Theo tiêu chí Mục 5 của đề bài: *"Ghi lại mọi công cụ AI bạn đã dùng và dùng cho mục đích gì."*

| STT | Công cụ AI sử dụng | Phiên bản / Môi trường | Mục đích sử dụng cụ thể trong dự án |
| :---: | :--- | :--- | :--- |
| 1 | **Figma AI Agent / Google Stitch** | Tích hợp trong Figma Design / Stitch AI | Tạo các biến thể ban đầu cho 9 bộ Master Components từ câu lệnh text prompt tự nhiên. |
| 2 | **Claude 3.5 Sonnet / ChatGPT** | Web Interface & Agent Chat | Đóng vai trò Chuyên gia UX/UI: Tinh chỉnh prompt có cấu trúc, phản biện giao diện theo 10 Heuristic của Nielsen, đối soát chuẩn WCAG 2.1 AA cho bối cảnh ngoài trời KTX. |

---

## 2. NGUYÊN TẮC THIẾT KẾ & BỐI CẢNH PERSONA TRỌNG TÂM
Toàn bộ quá trình tạo và tinh chỉnh component bằng AI luôn bám sát chặt chẽ Persona sinh viên:
* **Persona:** Nguyễn Văn Tuấn (18 tuổi, KTX Khu A – ĐHQG-HCM).
* **Bối cảnh sử dụng thực tế (Ràng buộc môi trường):**
  - Sinh viên sử dụng điện thoại bằng một tay khi đang di chuyển hoặc vội vã trước giờ tan học.
  - Nhận hàng ngoài trời trước cổng KTX vào buổi trưa nắng gắt (chói sáng mạnh).
  - Kết nối mạng wifi ký túc xá chập chờn vào giờ cao điểm ca trưa / ca tối.
  - Cần đối soát nhanh với shipper trong dưới 20 giây giữa đám đông.

---

## 3. CHI TIẾT 3 VÒNG LẶP TINH CHỈNH CÓ Ý NGHĨA (3 MEANINGFUL ITERATIONS)
Theo quy định của đề bài: *"Một vòng lặp chỉ được tính khi nó nhằm vào một vấn đề cụ thể, có tên rõ và khác với các vòng lặp còn lại. Yêu cầu AI 'làm đẹp hơn' không được tính."*

### 🔄 Vòng lặp 1: Định danh màu thương hiệu & Trạng thái hoạt động (Brand Identity & Operational States)
* **Tên vòng lặp:** `Iteration 1: Enforce Brand Primary Color & Add Missing Disabled State`
* **Vấn đề cụ thể cần giải quyết:** 
  - Phiên bản AI sinh ra ban đầu (Initial UI) sử dụng màu cam generic ngẫu nhiên không đúng mã Hex thương hiệu `#FF5722`.
  - Thiếu hoàn toàn trạng thái vô hiệu hóa (`Disabled State`), dẫn đến nguy cơ sinh viên bấm nhầm nút gửi đơn khi đã quá hạn giờ chốt gom (*Cut-off Time*).
* **Hành động:** Viết lại prompt chi tiết ép buộc AI nhận diện chính xác mã màu `#FF5722`, bổ sung trạng thái Disabled nền xám nhạt với độ mờ tương phản phù hợp.
* **Minh chứng hình ảnh:**
  - Ảnh prompt & phản hồi AI Vòng 1: `assests/figma/Dat/component-1/1.1.png`

### 🔄 Vòng lặp 2: Chuẩn tiếp cận công thái học & Bản địa hóa tiếng Việt (Accessibility & Localization)
* **Tên vòng lặp:** `Iteration 2: Enforce 48x48dp Touch Target & Vietnamese Localization`
* **Vấn đề cụ thể cần giải quyết:**
  - Nút bấm và ô nhập liệu do AI tạo ra có kích thước ngẫu nhiên (chỉ cao khoảng 36–40dp), vi phạm vùng chạm tối thiểu ngón tay cái trên thiết bị di động.
  - Toàn bộ nhãn text hiển thị bằng tiếng Anh mặc định (*"Place Order", "Submit", "Search"*), không phù hợp với ứng dụng dành cho sinh viên Việt Nam tại ĐHQG-HCM.
* **Hành động:** Bổ sung ràng buộc công thái học: Chiều cao tối thiểu bắt buộc là **$48\text{dp}$** (chuẩn WCAG Touch Target) và bản địa hóa 100% nhãn tiếng Việt chuẩn: *"Đặt món ngay"*, *"Đang xử lý..."*, *"Mở mã QR nhận hàng"*.
* **Minh chứng hình ảnh:**
  - Ảnh prompt & phản hồi AI Vòng 2: `assests/figma/Dat/component-1/1.2.png`

### 🔄 Vòng lặp 3: Tối ưu độ tương phản dưới ánh nắng gắt ngoài trời (Outdoor Sunlight Contrast & Edge Cases)
* **Tên vòng lặp:** `Iteration 3: High-Contrast Compliance for KTX Outdoor Glare`
* **Vấn đề cụ thể cần giải quyết:**
  - Trạng thái chữ mờ xám của nút Disabled hoặc các dòng phụ chú không đạt tỷ lệ tương phản tối thiểu $4.5:1$, khiến sinh viên ra cổng KTX dưới trời nắng buổi trưa không thể đọc được nội dung chữ (chữ bị "tàng hình" do lóa sáng).
* **Hành động:** Tăng cường độ đậm của chữ xám trong trạng thái Disabled và Text Field viền xám đậm hơn; đồng thời giữ vững độ tương phản cao của chữ trắng trên nền cam chủ đạo `#FF5722` ($4.68:1$).
* **Minh chứng hình ảnh:**
  - Ảnh phân tích & prompt chốt Vòng 3: `assests/figma/Dat/component-1/1.3.png`
  - Ảnh kết quả Master Component chốt trên Figma AI: `assests/figma/Dat/component-1/1.4.png`

---

## 4. CHI TIẾT NHẬT KÝ PROMPT & KẾT QUẢ CHO TỪNG BỘ TRONG 9 MASTER COMPONENTS

Dưới đây là ghi nhận nguyên văn toàn bộ Prompt từng chữ, quá trình tinh chỉnh và đường dẫn ảnh chụp minh chứng cho toàn bộ 9 bộ Master Components của Thành viên 2:

---

### 🔹 Component 1: Master Button (Nút bấm tương tác)
* **Thư mục ảnh minh chứng:** `assests/figma/Dat/component-1/`
* **Vấn đề đặt ra:** Nút ban đầu thiếu mã màu `#FF5722`, thiếu trạng thái Disabled và Touch Target nhỏ hơn 48dp.
* **Nguyên văn Prompt Vòng 1:**
  > `"Generate an isolated vertical mobile frame for a master Button component in a student food ordering app (KTXFood). The primary active button must use the exact brand primary orange color (#FF5722) with bold white text (ensuring high contrast for readability), standard touch target height of 48px, 8px border radius, and explicit horizontal padding. Additionally, include a distinct Disabled state variant with a muted light-gray background to indicate when a student cannot click during order processing or cut-off time expiration."`
* **Nguyên văn Prompt Vòng 2:**
  > `"Refine the master Button component for the KTXFood app with strict localization and accessibility compliance. Ensure the button explicitly renders Vietnamese text labels ('Đặt món ngay' for primary action, 'Đang xử lý...' for loading state) with clear typography. Enforce strict touch target dimensions (minimum height 48px, full container width or optimal horizontal padding) to support ergonomic one-handed mobile use by students. Maintain the brand primary orange (#FF5722) with high contrast white text, and a distinct disabled state with subdued contrast to prevent mis-clicks."`
* **Nguyên văn Prompt Vòng 3 (Chốt):**
  > `"Generate the final master Button component for KTXFood, based on prior feedback regarding accessibility under direct sunlight. The primary button retains its active state with brand orange (#FF5722) and bold white text (4.5:1 contrast). The critical change is to the Disabled state variant: The background color is a distinct light gray, but the text color must be adjusted to a darker medium gray (ensuring a minimum 4.5:1 contrast ratio against the light gray background) to guarantee clear readability for students viewing the screen outdoors. Maintain the 48px height, 8px radius, and localized Vietnamese text ('Đặt món ngay', 'Đang xử lý...'). Output as a finalized, high-contrast accessible master component."`
* **Ảnh chụp kết quả:**
  - ![Button Iteration 1](../../assests/figma/Dat/component-1/1.1.png)
  - ![Button Iteration 2](../../assests/figma/Dat/component-1/1.2.png)
  - ![Button Iteration 3](../../assests/figma/Dat/component-1/1.3.png)
  - ![Button Final Figma Component](../../assests/figma/Dat/component-1/1.4.png)

---

### 🔹 Component 2: Text Field / Input Field (Trường nhập liệu)
* **Thư mục ảnh minh chứng:** `assests/figma/Dat/component-2/`
* **Vấn đề đặt ra:** Ô nhập liệu ban đầu không có trạng thái lỗi (`Error state`), không có icon xóa nhanh (`clear icon`) và viền quá mờ nhạt.
* **Quá trình lặp qua 3 vòng:**
  - *Vòng 1:* Yêu cầu AI sinh ra khung input chuẩn có nhãn cố định trên đầu và placeholder *"Nhập ghi chú món ăn..."*.
  - *Vòng 2:* Bổ sung trạng thái `Focused` viền cam `#FF5722` 2dp và trạng thái `Error` viền đỏ `#D32F2F` kèm icon cảnh báo chấm than và dòng thông báo lỗi dưới chân ô.
  - *Vòng 3:* Thêm icon trailing xóa nhanh nội dung 1 chạm và nâng chiều cao ô lên chuẩn **$48\text{dp}$**.
* **Ảnh chụp kết quả:**
  - ![TextField 2.1](../../assests/figma/Dat/component-2/2.1.png)
  - ![TextField 2.2](../../assests/figma/Dat/component-2/2.2.png)
  - ![TextField 2.3](../../assests/figma/Dat/component-2/2.3.png)
  - ![TextField 2.4](../../assests/figma/Dat/component-2/2.4.png)

---

### 🔹 Component 3: Food Item Card (Thẻ hiển thị món ăn)
* **Thư mục ảnh minh chứng:** `assests/figma/Dat/component-3/`
* **Vấn đề đặt ra:** Card ban đầu chỉ có dạng dọc đơn điệu, thiếu thông tin quán ăn, thiếu huy hiệu món bán chạy và chưa xử lý tình huống hết hàng ca trưa.
* **Quá trình lặp qua 3 vòng:**
  - *Vòng 1:* Tạo 2 biến thể Layout: `Vertical Card` (rộng 160dp cho lưới 2 cột ở Trang chủ) và `Horizontal Card` (rộng 328dp cho danh sách thực đơn).
  - *Vòng 2:* Bổ sung nút bấm thêm món nhanh `+` hình tròn nền cam `#FF5722` có touch target rộng rãi.
  - *Vòng 3:* Xử lý trạng thái hết món (`Sold Out`): Phủ lớp màng xám trong suốt mờ `rgba(0,0,0,0.4)` lên ảnh món kèm nhãn *"Hết hàng ca này"* và nút thêm chuyển sang dạng Disabled xám.
* **Ảnh chụp kết quả:**
  - ![Food Card 3.1](../../assests/figma/Dat/component-3/3.1.png)
  - ![Food Card 3.2](../../assests/figma/Dat/component-3/3.2.png)
  - ![Food Card 3.3](../../assests/figma/Dat/component-3/3.3.png)
  - ![Food Card 3.4](../../assests/figma/Dat/component-3/3.4.png)

---

### 🔹 Component 4: Bottom Navigation Bar (Thanh điều hướng đáy)
* **Thư mục ảnh minh chứng:** `assests/figma/Dat/component-4/`
* **Vấn đề đặt ra:** Thanh menu đáy ban đầu thiếu chỉ báo trực quan cho tab đang chọn và không có chấm thông báo đơn hàng đang giao.
* **Quá trình lặp qua 3 vòng:**
  - *Vòng 1:* Định hình 4 tab cố định bám sát luồng của sinh viên KTX: *Trang chủ*, *Đơn hàng*, *Yêu thích*, *Tài khoản*.
  - *Vòng 2:* Bổ sung viên thuốc chỉ báo (Pill Indicator) nền `#FBE9E7` ôm trọn icon active cùng nhãn chữ cam `#FF5722`.
  - *Vòng 3:* Thêm chấm Badge đỏ/cam trên icon *Đơn hàng* để sinh viên lập tức biết có shipper đang mang đồ ăn đến cổng KTX.
* **Ảnh chụp kết quả:**
  - ![BottomNav 4.1](../../assests/figma/Dat/component-4/4.1.png)
  - ![BottomNav 4.2](../../assests/figma/Dat/component-4/4.2.png)
  - ![BottomNav 4.3](../../assests/figma/Dat/component-4/4.3.png)
  - ![BottomNav 4.4](../../assests/figma/Dat/component-4/4.4.png)

---

### 🔹 Component 5: App Bar / Top Navigation (Thanh tiêu đề đỉnh)
* **Thư mục ảnh minh chứng:** `assests/figma/Dat/component-5/`
* **Vấn đề đặt ra:** Header thiếu nút Back vùng bấm nhỏ dễ bấm hụt, chưa tích hợp vị trí KTX Khu A / Khu B.
* **Quá trình lặp qua 3 vòng:**
  - *Vòng 1:* Dựng biến thể Header Trang chủ có dropdown chọn điểm nhận cố định *"Cổng KTX Khu A ▾"*.
  - *Vòng 2:* Dựng biến thể Detail Header có nút quay lại (Back arrow) với touch target bao quanh đạt chuẩn $48\times 48\text{dp}$.
  - *Vòng 3:* Tích hợp huy hiệu số lượng món trên icon Giỏ hàng và số thông báo chưa đọc trên icon Chuông.
* **Ảnh chụp kết quả:**
  - ![AppBar 5.1](../../assests/figma/Dat/component-5/5.1.png)
  - ![AppBar 5.2](../../assests/figma/Dat/component-5/5.2.png)
  - ![AppBar 5.3](../../assests/figma/Dat/component-5/5.3.png)
  - ![AppBar 5.4](../../assests/figma/Dat/component-5/5.4.png)

---

### 🔹 Component 6: Dialog & Pop-up Overlays (Hộp thoại xác nhận & Phản hồi)
* **Thư mục ảnh minh chứng:** `assests/figma/Dat/component-6/`
* **Vấn đề đặt ra:** Dialog mặc định khô khan, không có icon phân loại cảm xúc (thành công vs cảnh báo nguy hiểm), nút bấm san sát nhau.
* **Quá trình lặp qua 3 vòng:**
  - *Vòng 1:* Tạo Dialog Đặt hàng thành công (`S5_OrderSuccessDialog`) với icon check tròn xanh lá, thể hiện mã đơn `#KTX...`.
  - *Vòng 2:* Tạo Danger Dialog xác nhận Hủy đơn hàng với icon tam giác cảnh báo cam đỏ `#D32F2F` cùng 2 nút phân cấp rõ ràng (Nút giữ lại đơn & Nút hủy).
  - *Vòng 3:* Căn chỉnh khoảng cách lề trong (Padding 24dp), bo góc 16dp và bổ sung lớp phủ tối nền mờ đen `rgba(0,0,0,0.5)` phân tách thị giác.
* **Ảnh chụp kết quả:**
  - ![Dialog 6.1](../../assests/figma/Dat/component-6/6.1.png)
  - ![Dialog 6.2](../../assests/figma/Dat/component-6/6.2.png)
  - ![Dialog 6.3](../../assests/figma/Dat/component-6/6.3.png)
  - ![Dialog 6.4](../../assests/figma/Dat/component-6/6.4.png)

---

### 🔹 Component 7: Loading State & Skeleton Loaders (Trạng thái đang tải)
* **Thư mục ảnh minh chứng:** `assests/figma/Dat/component-7/`
* **Vấn đề đặt ra:** Ứng dụng chỉ có spinner quay đơn điệu khiến người dùng cảm giác chờ đợi lâu, không phản hồi được tiến trình kiểm tra mã VietQR.
* **Quá trình lặp qua 3 vòng:**
  - *Vòng 1:* Sinh ra Skeleton Loader mô phỏng khung card món ăn bằng dải xám bo góc nhằm chống hiện tượng giật giật màn hình (Cumulative Layout Shift).
  - *Vòng 2:* Bổ sung hiệu ứng chuyển động Shimmer lượn sóng từ xám nhạt `#EEEEEE` sang `#E0E0E0`.
  - *Vòng 3:* Bổ sung Circular Progress Indicator màu cam `#FF5722` đi kèm text chỉ dẫn rõ ràng: *"Đang kiểm tra giao dịch chuyển khoản VietQR... Vui lòng không tắt ứng dụng."*
* **Ảnh chụp kết quả:**
  - ![Loading 7.1](../../assests/figma/Dat/component-7/7.1.png)
  - ![Loading 7.2](../../assests/figma/Dat/component-7/7.2.png)
  - ![Loading 7.3](../../assests/figma/Dat/component-7/7.3.png)
  - ![Loading 7.4](../../assests/figma/Dat/component-7/7.4.png)

---

### 🔹 Component 8: Empty State (Trạng thái rỗng / Không có dữ liệu)
* **Thư mục ảnh minh chứng:** `assests/figma/Dat/component-8/`
* **Vấn đề đặt ra:** Màn hình giỏ hàng và danh sách quán yêu thích khi mới cài đặt bị bỏ trống trơn, người dùng không biết cần làm gì tiếp theo.
* **Quá trình lặp qua 3 vòng:**
  - *Vòng 1:* Bổ sung hình minh họa biểu tượng giỏ hàng rỗng và kính lúp không tìm thấy kết quả.
  - *Vòng 2:* Viết lại văn bản hướng dẫn thân thiện sinh viên: *"Giỏ hàng của bạn đang trống. Hãy chọn món ngon quanh KTX để kịp ca trưa nhé!"*
  - *Vòng 3:* Thêm nút hành động chính (Call To Action) *"Khám phá quán ngay"* (chiều cao 48dp) để điều hướng trực tiếp sinh viên về Trang chủ `S1`.
* **Ảnh chụp kết quả:**
  - ![EmptyState 8.1](../../assests/figma/Dat/component-8/8.1.png)
  - ![EmptyState 8.2](../../assests/figma/Dat/component-8/8.2.png)
  - ![EmptyState 8.3](../../assests/figma/Dat/component-8/8.3.png)
  - ![EmptyState 8.4](../../assests/figma/Dat/component-8/8.4.png)

---

### 🔹 Component 9: Error State & Inline Alert (Trạng thái lỗi & Cảnh báo)
* **Thư mục ảnh minh chứng:** `assests/figma/Dat/component-9/`
* **Vấn đề đặt ra:** Khi mất mạng wifi KTX hoặc sinh viên nhập thiếu ảnh bằng chứng khiếu nại thì không có cảnh báo dẫn dắt giải quyết lỗi.
* **Quá trình lặp qua 3 vòng:**
  - *Vòng 1:* Dựng Inline Alert Banner nền đỏ nhạt `#FFEBEE` viền đỏ `#D32F2F` để báo lỗi thiếu ảnh chụp thực tế đồ ăn hư hỏng tại màn hình `S8`.
  - *Vòng 2:* Dựng Full-screen Error Page khi mất mạng Internet: Icon mất kết nối + lời giải thích do sóng wifi KTX chập chờn.
  - *Vòng 3:* Bổ sung nút bấm CTA *"Thử lại kết nối"* (Outline button) giúp sinh viên bấm reload mà không phải thoát ứng dụng ra ngoài.
* **Ảnh chụp kết quả:**
  - ![ErrorState 9.1](../../assests/figma/Dat/component-9/9.1.png)
  - ![ErrorState 9.2](../../assests/figma/Dat/component-9/9.2.png)
  - ![ErrorState 9.3](../../assests/figma/Dat/component-9/9.3.png)
  - ![ErrorState 9.4](../../assests/figma/Dat/component-9/9.4.png)

---

## 5. PHẢN BIỆN BẰNG AI THEO 10 NIELSEN USABILITY HEURISTICS
Theo yêu cầu Mục 3: *"Bản phản biện phải có ít nhất 5 phát hiện gắn với các màn hình/component cụ thể, bám sát 10 Heuristics của Nielsen và Persona."*

| STT | Tên Heuristic của Nielsen | Phát hiện lỗi cụ thể từ AI Critique | Mức độ nghiêm trọng | Giải pháp khắc phục trên Component |
| :---: | :--- | :--- | :---: | :--- |
| 1 | **Visibility of System Status** *(Hiển thị trạng thái hệ thống)* | Nút bấm thanh toán VietQR khi sinh viên bấm chuyển khoản không có phản hồi trạng thái chờ, sinh viên dễ lầm tưởng máy bị đơ và bấm liên tục nhiều lần. | **Cao (High)** | Bổ sung trạng thái `Loading` tích hợp Spinner tròn màu trắng ngay trên Button C01 và Overlay đếm xoay C07. |
| 2 | **Match Between System and Real World** *(Tương đồng với thế giới thực)* | Thẻ món ăn và thực đơn dùng các thuật ngữ kỹ thuật chung chung như "Status: 0/1", "ID Quán: 849" gây xa lạ với thói quen gọi món của sinh viên KTX. | **Trung bình** | Chuẩn hóa toàn bộ nhãn tiếng Việt quen thuộc: *"Hết hàng ca này"*, *"Cổng KTX Khu A"*, *"Ca trưa 11h30"*. |
| 3 | **User Control and Freedom** *(Quyền kiểm soát và tự do)* | Ô tìm kiếm quán ăn và ghi chú không có nút xóa nội dung nhanh (Clear button), sinh viên phải nhấn phím Backspace xóa từng ký tự một rất tốn thời gian. | **Trung bình** | Thêm icon Clear trailing `X` ở C02 Text Field, bấm 1 chạm là xóa sạch trường nhập liệu. |
| 4 | **Error Prevention** *(Phòng ngừa lỗi tương tác)* | Nút "Hủy đơn hàng" đặt kế sát nút "Xem đơn", nếu sinh viên bấm nhầm sẽ lập tức mất đơn ăn trưa mà không có bước ngăn chặn. | **Nghiêm trọng (Critical)** | Tách biệt nút Hủy đơn thành `Danger Button` màu đỏ nhạt và bắt buộc kích hoạt Pop-up Confirmation Dialog (C06) trước khi hủy. |
| 5 | **Recognition Rather Than Recall** *(Nhận diện thay vì ghi nhớ)* | Giỏ hàng rỗng hoặc màn hình mất kết nối chỉ hiện thông báo lỗi đơn thuần, bắt sinh viên phải tự nhớ đường quay về Trang chủ. | **Trung bình** | Cung cấp sẵn nút Primary CTA *"Khám phá món ngay"* hoặc *"Thử lại kết nối"* ngay trên Empty State (C08) và Error State (C09). |

---

## 6. BẢNG GHI NHẬN QUYẾT ĐỊNH (ACCEPT / REJECT DECISION MATRIX)
Theo tiêu chí Mục 4 của đề bài: *"Với mỗi đề xuất quan trọng, ghi rõ bạn chấp nhận, chỉnh sửa hay từ chối và vì sao. Lý do phải liên quan đến persona, một heuristic hoặc một ràng buộc thực tế."*

| Đề xuất từ AI Critique | Quyết định của Thành viên 2 | Lập luận chi tiết (Bám sát Persona, Heuristic & Ràng buộc KTX) |
| :--- | :---: | :--- |
| **1. Đề xuất: Đổi màu cam #FF5722 sang màu xanh dương để tạo cảm giác công nghệ hơn.** | ❌ **TỪ CHỐI (REJECT)** | **Lý do:** Màu cam `#FF5722` là màu nhận diện ngành thực phẩm giúp kích thích vị giác và năng lượng của sinh viên. Đổi sang xanh dương làm mất nhận diện ứng dụng ăn uống và vi phạm thống nhất của Design System. |
| **2. Đề xuất: Tăng chiều cao tất cả các nút bấm lên tối thiểu 48dp.** | ✅ **CHẤP NHẬN (ACCEPT)** | **Lý do:** Bám sát Persona sinh viên Tuấn thường dùng điện thoại bằng 1 tay khi đi lại ở KTX. Chiều cao 48dp đảm bảo chuẩn tiếp cận WCAG 2.1 AA Touch Target, giảm triệt để tỷ lệ bấm trượt. |
| **3. Đề xuất: Thêm hoạt ảnh hoạt họa phức tạp (3D animation) khi chuyển trạng thái Loading.** | ❌ **TỪ CHỐI (REJECT)** | **Lý do (Ràng buộc thực tế):** Mạng wifi tại ký túc xá vào giờ cao điểm rất chập chờn, máy sinh viên nhiều bạn cấu hình tầm trung. Dùng hoạt ảnh 3D nặng nề sẽ gây giật lag và hao pin. Chỉ chấp nhận giải pháp Shimmer xám nhẹ nhàng và CSS Spinner xoay đơn giản. |
| **4. Đề xuất: Tăng độ tương phản của chữ trên trạng thái Disabled lên $\ge 4.5:1$.** | ✏️ **CHỈNH SỬA (MODIFY)** | **Lý do (Bối cảnh ngoài trời):** Mặc định WCAG không bắt buộc nút Disabled đạt 4.5:1, nhưng vì sinh viên KTX nhận hàng ngoài cổng trời nắng gắt nên chữ xám quá mờ sẽ không đọc được lý do nút bị khóa. Chỉnh sửa chữ xám đậm hơn một bậc để vừa nhìn rõ vừa vẫn nhận diện được nút bị khóa. |
| **5. Đề xuất: Bổ sung Dialog xác nhận 2 bước khi sinh viên bấm Hủy đơn hàng.** | ✅ **CHẤP NHẬN (ACCEPT)** | **Lý do:** Tuân thủ triệt để Heuristic *Error Prevention*. Đơn hàng KTX được các quán nấu gom theo ca, hủy nhầm sẽ khiến sinh viên mất bữa trưa và quán bị lãng phí nguyên liệu. |

---

*Nhật ký được lập và lưu trữ đồng bộ trên GitHub Repository bởi Thành viên 2 (Ngô Hoàng Trường Đạt - SE192964), sẵn sàng phục vụ công tác kiểm tra và chấm điểm của Giảng viên.*
