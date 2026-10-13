# Design Decisions – Food Ordering App KTX

> **Dự án:** Food Ordering App cho Sinh viên Ký túc xá ĐHQG-HCM (PRM323 – Lab 2)  
> **Người thực hiện:** Thành viên 4 – Trần Sanh Điền - Prototyping & Flutter Handoff Lead  
> **Tài liệu tham chiếu:** `ux/persona.md`, `ux/user-flow.md`, `design/DESIGN.md`, `food_ordering_app_srs.md` (Mục 2, 3 & 4.A), Figma Prototype (File chính key `84O0L9O6Z5TVkMjBvMRn33`, File phụ key `ALDYFWUZ72BaeyulpVi7uY`).

---

## 1. Các quyết định thiết kế cốt lõi

Dưới đây là 10 quyết định thiết kế quan trọng nhất được áp dụng xuyên suốt hệ thống UI và User Flows, giải quyết triệt để các bài toán thực tế của sinh viên KTX ĐHQG-HCM:

### Quyết định 1: Tích hợp đồng hồ đếm ngược giờ chốt ca gom đơn (Cut-off Time Countdown)
* **Nội dung quyết định:** Hiển thị đồng hồ đếm ngược trực quan đến hạn chót đặt món (ví dụ: Ca trưa chốt lúc 10h45 để giao lúc 11h30) ngay tại Banner đầu trang Trang chủ (`S1`) và phần chọn ca nhận tại Giỏ hàng (`S4`).
* **Lý do căn cứ:**
  - *Gắn pain point Persona Nguyễn Văn Tuấn:* Sinh viên thường xuyên mải học đại cương hoặc chơi game trên điện thoại dẫn đến quên giờ ăn hoặc lỡ bữa.
  - *Gắn Success Metric:* Đảm bảo sinh viên hoàn tất chọn món và gửi đơn trước Cut-off time dưới 30 giây.
  - *Heuristic Nielsen #1 (Visibility of System Status):* Cung cấp phản hồi liên tục về trạng thái tiếp nhận đơn của các quán ăn quanh KTX, giúp người dùng chủ động thời gian.
* **Phương án đã loại:** Cho phép sinh viên đặt món theo thời gian tùy ý bất kỳ lúc nào (On-demand) như Grab/ShopeeFood.  
  *Lý do loại:* Các quán bình dân quanh KTX không thể điều xe giao lẻ tẻ từng hộp cơm với chi phí thấp; gom đơn theo khung giờ cố định là điều kiện tiên quyết để giữ giá bình dân và miễn/giảm phí ship.
* **Nơi thấy trên Figma:** File chính "Prototype", Page Student Screens: node `4:1539` (`S1`) và node `3:2` (`S4`).
* **Màn ảnh hưởng:** `S1_FoodSearchHome`, `S4_GroupCartCheckout`.

---

### Quyết định 2: Điểm giao nhận cố định tại Cổng KTX thay vì giao tận phòng
* **Nội dung quyết định:** Buộc sinh viên chọn địa điểm nhận đồ ăn cố định là Cổng KTX Khu A hoặc Cổng KTX Khu B, không hỗ trợ nhập địa chỉ tự do hay giao tận phòng ký túc xá.
* **Lý do căn cứ:**
  - *Ràng buộc thực tế & Quy định Ban Quản lý KTX ĐHQG:* Nội quy KTX nghiêm cấm người lạ/shipper tự do ra vào khuôn viên các tòa nhà ký túc xá vì lý do an ninh, trật tự.
  - *Tối ưu chi phí & gom chuyến:* Shipper vận chuyển khối lượng lớn (15–20 đơn/chuyến) chỉ dừng 1 điểm tập trung để trả hàng hàng loạt trong ca 11h30–12h00.
* **Phương án đã loại:** Tích hợp bản đồ GPS định vị chính xác vị trí phòng ở sinh viên (nhập Số phòng, Tòa nhà như AH1, BA4...).  
  *Lý do loại:* Giao tận phòng làm vỡ quy trình gom đơn theo ca, tăng thời gian giao hàng lên gấp nhiều lần và vi phạm nội quy nội trú.
* **Nơi thấy trên Figma:** File chính "Prototype", Page Student Screens: node `4:1539` (Header `S1`), node `3:2` (Radio chọn cổng tại `S4`).
* **Màn ảnh hưởng:** `S1_FoodSearchHome`, `S4_GroupCartCheckout`, `S6_LiveOrderTracking`, `S7_PickupQRCode`.

---

### Quyết định 3: Dialog Phản hồi tức thì Xác nhận Đặt hàng thành công (`S5_Success`)
* **Nội dung quyết định:** Sử dụng Pop-up Modal hiển thị ngay sau khi bấm thanh toán (VietQR hoặc COD) để chúc mừng, xác nhận mã đơn `#KTX-...` và nhắc nhở thời gian có mặt tại cổng KTX nhận hàng trước khi chuyển tiếp sang màn hình Theo dõi đơn (`S6`).
* **Lý do căn cứ:**
  - *Heuristic Nielsen #1 (Visibility of System Status):* Cung cấp phản hồi tức thì và dứt khoát rằng giao dịch đặt hàng đã được ghi nhận thành công, loại bỏ cảm giác hoang mang sợ bị trừ tiền mà đơn chưa gửi.
  - *Heuristic Nielsen #5 (Error Prevention):* Nhắc nhở rõ ràng sinh viên cần có mặt tại cổng đúng giờ ca nhận (11h30), tránh tình trạng sinh viên đặt xong rồi quên ra nhận khiến thức ăn bị nguội hoặc bị hủy.
* **Phương án đã loại:** Chuyển trang trực tiếp tức thì từ `S4`/`S5` sang `S6_LiveOrderTracking` mà không có bước dialog xác nhận trung gian.  
  *Lý do loại:* Chuyển trang đột ngột dễ làm người dùng lúng túng, không kịp đọc mã đơn hàng và giờ hẹn giao nhận quan trọng.
* **Nơi thấy trên Figma:** File phụ "Lab 2 Food Ordering App", Page Prototype: node `192:2` (`S5_OrderSuccessDialog`).  
  *(⚠ MÂU THUẪN NGUỒN (d): Trong File chính Page Components chỉ có component `123:72` "Dialog / Xác nhận giao hàng KTX", dialog đặt hàng thành công này ở file phụ chưa có master component trong file chính).*
* **Màn ảnh hưởng:** `S4_GroupCartCheckout`, `S5_OnlinePayment`, `S5_OrderSuccessDialog`, `S6_LiveOrderTracking`.

---

### Quyết định 4: Cơ chế thanh toán tiền mặt (COD) thay thế dự phòng khi VietQR gặp sự cố
* **Nội dung quyết định:** Tại màn hình thanh toán VietQR (`S5`), bố trí nút liên kết quay lại đổi sang phương thức "Tiền mặt khi nhận hàng (COD)" và tại `S4` cho phép chọn song song cả hai hình thức.
* **Lý do căn cứ:**
  - *Heuristic Nielsen #9 (Help users recognize, diagnose, and recover from errors):* Cung cấp lối thoát an toàn và đường lui (Exit route) khi ứng dụng ngân hàng bị bảo trì, mạng Internet KTX chập chờn hoặc tài khoản sinh viên không đủ số dư.
  - *Heuristic Nielsen #3 (User Control and Freedom):* Người dùng tự do đổi ý về phương thức trả tiền mà không bị kẹt cứng ở màn hình chờ chuyển khoản.
* **Phương án đã loại:** Bắt buộc 100% thanh toán trả trước qua cổng ngân hàng/ví điện tử, không hỗ trợ tiền mặt.  
  *Lý do loại:* Nhiều sinh viên cuối tháng hết tiền trong tài khoản hoặc ngân hàng lỗi sẽ bị chặn đứng hoàn toàn việc đặt bữa trưa.
* **Nơi thấy trên Figma:** File chính "Prototype", Page Student Screens: node `3:2` (Lựa chọn radio tại `S4`) và node `8:7969` (Nút đổi sang COD tại `S5`).
* **Màn ảnh hưởng:** `S4_GroupCartCheckout`, `S5_OnlinePayment`.

---

### Quyết định 5: Mã QR Nhận hàng tích hợp hiển thị nổi bật 4 số cuối SĐT đối soát thủ công khi chói nắng
* **Nội dung quyết định:** Trên màn hình/thẻ nhận hàng `S7`, ngoài mã QR kích thước lớn để shipper quét camera, bố trí thêm một dòng văn bản in đậm kích thước lớn hiển thị **4 số cuối Số điện thoại** của sinh viên (`•••• 2947`).
* **Lý do căn cứ:**
  - *Gắn pain point Persona Nguyễn Văn Tuấn:* Bối cảnh nhận hàng là cổng KTX Khu A giữa trưa (11h30–12h00) nắng gắt ngoài trời; màn hình điện thoại sinh viên bị chói sáng hoặc bị trầy xước khiến camera của shipper không thể quét mã QR nhanh chóng.
  - *Gắn Success Metric:* Rút ngắn thời gian đối soát và trao túi đồ ăn tại cổng KTX xuống **dưới 20 giây**, loại bỏ cảnh shipper phải đứng gọi điện thoại tìm từng sinh viên giữa đám đông.
  - *Heuristic Nielsen #6 (Recognition rather than Recall) & #9 (Error Recovery):* Cung cấp phương thức dự phòng tức thì không cần mạng Internet phức tạp.
* **Phương án đã loại:** Chỉ dùng duy nhất một mã QR; nếu quét không được thì yêu cầu tài xế mở app bấm tìm tên sinh viên trong danh sách 20 đơn.  
  *Lý do loại:* Tìm kiếm thủ công giữa 20 đơn làm ùn tắc cổng KTX, thời gian đối soát kéo dài > 60 giây, vi phạm trực tiếp Success Metric đề ra.
* **Nơi thấy trên Figma:** File chính "Prototype", Page Student Screens: node `3:284` (`S7`).
* **Màn ảnh hưởng:** `S6_LiveOrderTracking`, `S7_PickupQRCode`.

---

### Quyết định 6: Biểu mẫu Khiếu nại `S8` hỗ trợ chọn nhiều sự cố, nhiều món bị ảnh hưởng, tự tính tiền hoàn và chọn 2 kênh hoàn tiền
* **Nội dung quyết định:** Thay vì form khiếu nại văn bản thuần túy, màn hình `S8` thiết kế tương tác chọn danh mục: tích chọn nhiều lý do (đổ vỡ, thiếu món, sai vị), tích chọn các món bị ảnh hưởng (có nút "Chọn tất cả"), hệ thống **tự động tính tổng số tiền bồi hoàn**, và cho chọn nhận hoàn về Ví KTX Food hoặc chuyển khoản Ngân hàng.
* **Lý do căn cứ:**
  - *Heuristic Nielsen #5 (Error Prevention) & #7 (Flexibility and Efficiency of Use):* Giảm thiểu nhập liệu thủ công; số tiền yêu cầu hoàn được tính toán tự động chính xác dựa trên đơn giá món bị thiếu/hỏng, tránh tranh cãi sai lệch số tiền.
  - *Ràng buộc tâm lý sinh viên:* Cung cấp tùy chọn hoàn về Ví KTX Food giúp tiền về ngay lập tức để đặt bữa tiếp theo, hoặc chọn nhận chuyển khoản về STK ngân hàng nếu muốn rút tiền mặt.
  - *(⚠ MÂU THUẪN NGUỒN (c): Khắc phục sự sơ sài của `user-flow.md` vốn chỉ ghi nhập STK, đồng bộ theo thiết kế hoàn chỉnh trên Figma).*
* **Phương án đã loại:** Sinh viên tự gõ số tiền muốn bồi hoàn vào ô input văn bản và chỉ ghi lý do chung chung vào ô ghi chú.  
  *Lý do loại:* Sinh viên dễ tính nhầm tiền, quán ăn mất thời gian đối soát lại hóa đơn, quy trình giải quyết kéo dài gây ức chế.
* **Nơi thấy trên Figma:** File chính "Prototype", Page Student Screens: node `8:6980`; File phụ "Lab 2 Food Ordering App": node `85:247` (tương tác) và `192:19` (gửi thành công).
* **Màn ảnh hưởng:** `S8_DisputeRefund`, `S10_OrderHistory`.

---

### Quyết định 7: Giới hạn phạm vi 3 Flows chỉ tập trung chuyên biệt vào vai trò Sinh viên (Student Role)
* **Nội dung quyết định:** Toàn bộ kịch bản thiết kế tương tác và chuyển giao Flutter của Lab 2 chỉ tập trung hiện thực hóa góc nhìn của Sinh viên nội trú (3 User Flows: Đặt món gom đơn ca trưa, Nhận hàng bằng QR tại cổng, Khiếu nại bồi hoàn), không ôm đồm giao diện của Shipper hay Chủ quán.
* **Lý do căn cứ:**
  - *Ràng buộc thực tế đề tài Lab 2 (Scope & Time Constraint):* Thời lượng làm việc nhóm có hạn; tập trung nguồn lực làm sâu sắc, chỉn chu trải nghiệm cốt lõi của người mua (Học sinh) giúp đạt chuẩn cao nhất về Accessibility, Design Tokens và Handoff.
  - *Bám sát Persona & Problem Statement:* Vấn đề cốt lõi cần giải quyết triệt để là nỗi đau của sinh viên KTX Khu A (giá ship cao, thất lạc đồ ăn tại cổng).
* **Phương án đã loại:** Dựng song song cả 3 vai trò (Sinh viên, Shipper, Quán ăn) cùng lúc trong 1 prototype.  
  *Lý do loại:* Giao diện sẽ bị phân mảnh, thiếu chiều sâu, không đủ thời gian hoàn thiện các variant và token theo quy chuẩn khắt khe của môn học.
* **Nơi thấy trên Figma:** File chính "Prototype", cấu trúc phân trang tập trung toàn bộ màn hình tương tác vào Page `Student Screens`.
* **Màn ảnh hưởng:** Toàn bộ 11 màn hình từ `S1` đến `S10`.

---

### Quyết định 8: Tách biệt biểu mẫu Đánh giá thành 2 đối tượng độc lập: Quán ăn và Shipper (`S9`)
* **Nội dung quyết định:** Tại màn hình `S9`, phân chia rõ ràng 2 khối chấm sao và nhận xét riêng biệt: Khối 1 dành cho Quán ăn (chất lượng hương vị, độ nóng, quy cách đóng gói); Khối 2 dành cho Người giao hàng (thái độ, đúng giờ tại cổng KTX, bảo quản đồ ăn).
* **Lý do căn cứ:**
  - *Heuristic Nielsen #2 (Match between System and the Real World):* Mô hình vận hành của KTX phân định rõ trách nhiệm giữa người nấu và người vận chuyển tập trung. Thức ăn bị nguội hoặc đổ tràn có thể do quán đóng gói kém hoặc do tài xế chạy ẩu; việc tách bạch đánh giá giúp truy đúng trách nhiệm.
  - *Bảo vệ quyền lợi công bằng cho các bên:* Tránh tình trạng shipper bị trừ sao oan do quán nấu dở, hoặc ngược lại quán ăn bị đánh giá 1 sao do tài xế giao trễ ca.
* **Phương án đã loại:** Chỉ có 1 thanh chấm sao chung cho toàn bộ đơn hàng như các app thương mại truyền thống.  
  *Lý do loại:* Không phản ánh đúng nguyên nhân sự cố, không cung cấp dữ liệu giá trị để cải thiện dịch vụ.
* **Nơi thấy trên Figma:** File chính "Prototype", Page Student Screens: node `8:6735` (`S9`).
* **Màn ảnh hưởng:** `S9_ReviewFeedback`.

---

### Quyết định 9: Tính năng "Đặt lại đơn này" (Re-order) một chạm trong Lịch sử đơn hàng (`S10`)
* **Nội dung quyết định:** Trên mỗi thẻ đơn hàng cũ ở màn hình `S10`, bố trí nút bấm nổi bật "Đặt lại đơn này" (`Secondary Button`) cho phép thêm lại toàn bộ món ăn và topping cũ vào giỏ hàng ngay lập tức.
* **Lý do căn cứ:**
  - *Gắn thói quen Persona Nguyễn Văn Tuấn:* Sinh viên KTX thường có xu hướng ăn lặp đi lặp lại một vài món quen thuộc (cơm sườn, bún bò) từ quán quen gần KTX vào các ngày trong tuần.
  - *Heuristic Nielsen #7 (Flexibility and Efficiency of Use):* Giảm thời gian tìm kiếm từ 30 giây xuống dưới 5 giây; sinh viên không phải duyệt menu và chọn lại từng loại topping từ đầu.
* **Phương án đã loại:** Bắt sinh viên phải bấm vào quán ăn, tìm lại từng món trong menu rồi tự cấu hình lại topping.  
  *Lý do loại:* Thao tác rườm rà, gây lãng phí thời gian và tăng nguy cơ trễ hạn Cut-off time ca trưa.
* **Nơi thấy trên Figma:** File chính "Prototype", Page Student Screens: node `26:2` (`S10`).
* **Màn ảnh hưởng:** `S10_OrderHistory`, `S4_GroupCartCheckout`.

---

### Quyết định 10: Thanh điều hướng đáy (Bottom Navigation Bar) cố định 4 tabs chuẩn M3
* **Nội dung quyết định:** Duy trì thanh điều hướng Bottom Navigation Bar xuyên suốt ở tất cả các màn hình cấp Root (`S1`, `S6`, `S10`, `S13`) với 4 tabs: Trang chủ (Home), Khám phá (Explore), Đơn hàng (Orders), Cá nhân (Profile).
* **Lý do căn cứ:**
  - *Heuristic Nielsen #4 (Consistency and Standards):* Tuân thủ quy chuẩn thiết kế Mobile Navigation chuẩn Android/Material 3; vị trí các tab cố định giúp người dùng hình thành phản xạ không gian (Spatial memory).
  - *Hỗ trợ chuyển đổi tác vụ nhanh:* Sinh viên đang ở Trang chủ có thể một chạm chuyển sang xem tiến trình đơn hàng đang giao (`S6`) hoặc kiểm tra lịch sử (`S10`).
  - *(⚠ MÂU THUẪN NGUỒN (b): Thiết kế trên Figma đang dùng 4 tab Home/Explore/Orders/Profile, trong khi IA của `user-flow.md` đề xuất Trang chủ/Đơn hàng/Lịch sử/Quán quen/Tài khoản. Quyết định giữ đúng 4 tabs theo Figma để đảm bảo 100% khớp với UI thực tế).*
* **Phương án đã loại:** Dùng Navigation Drawer (Menu ngăn kéo trượt bên hông) hoặc thanh Bottom Bar tự ẩn khi cuộn trang.  
  *Lý do loại:* Menu trượt làm ẩn giấu các chức năng quan trọng; thanh bottom bar tự ẩn làm sinh viên khó nhận biết trạng thái đơn hàng đang giao.
* **Nơi thấy trên Figma:** File chính "Prototype", Page Components: node `87:152` (`Crave/Bottom Navigation`); xuất hiện tại `4:1539`, `3:700`, `26:2`.
* **Màn ảnh hưởng:** `S1_FoodSearchHome`, `S6_LiveOrderTracking`, `S10_OrderHistory`.