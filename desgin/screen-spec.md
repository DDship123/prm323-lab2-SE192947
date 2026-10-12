# Screen Spec – Food Ordering App KTX

> **Dự án:** Food Ordering App cho Sinh viên Ký túc xá ĐHQG-HCM (PRM323 – Lab 2)  
> **Người thực hiện:** Thành viên 4 – Trần Sanh Điền - Prototyping & Flutter Handoff Lead  
> **Tài liệu tham chiếu:** `ux/persona.md`, `ux/user-flow.md`, `design/DESIGN.md`, `food_ordering_app_srs.md` (Mục 3 & 4.A), và hệ thống thiết kế Figma (File chính key `84O0L9O6Z5TVkMjBvMRn33`, File phụ key `ALDYFWUZ72BaeyulpVi7uY`).  
> **Ghi chú về tiến độ & nguồn dữ liệu:**  
> - Các frame thiết kế hiện tại trên Figma Page Student Screens đang có kích thước rộng **390dp** (iPhone) và file phụ rộng **440dp**, chưa có Page 03 Final UI chuẩn **360×800dp**.  
> - Các mâu thuẫn giữa tài liệu và Figma được gắn cảnh báo `⚠ MÂU THUẪN NGUỒN` và ưu tiên hiển thị theo Figma UI kết hợp luồng logic của `user-flow.md`. Các vị trí thiếu dữ liệu được đánh dấu `⚠ CẦN BỔ SUNG`.

---

## 1. Tổng quan

Bảng tổng hợp 11 màn hình và dialog nằm trong phạm vi 3 User Flows cốt lõi của vai trò Sinh viên:

| Mã | Tên Màn hình (Chuẩn User Flow) | Loại Root / Nested | Thuộc Flow | Node Figma |
| :--- | :--- | :--- | :--- | :--- |
| **S1** | `S1_FoodSearchHome` (Tra cứu đặt đồ ăn) | Root Screen (Tab Trang chủ) | Flow 1 (Start), Flow 2 (End) | `4:1539` (File chính, Page Student Screens) |

| **S2** | `S2_StoreDetailMenu` (Chi tiết Quán ăn & Thực đơn) | Nested Screen | Flow 1 (Step) | `3:479` (File chính, Page Student Screens) |

| **S3** | `S3_FoodCustomization` (Tùy biến món ăn) | Nested Screen / Modal Bottom Sheet | Flow 1 (Step) | `8:7296` (File chính, Page Student Screens) |

| **S4** | `S4_GroupCartCheckout` (Giỏ hàng & Thanh toán gom đơn) | Nested Screen | Flow 1 (Step / Alt) | `3:2` (File chính, Page Student Screens) |

| **S5** | `S5_OnlinePayment` (Thanh toán online) | Nested Screen | Flow 1 (Step) | `8:7969` (File chính, Page Student Screens) |

| **S5_Success** | `S5_OrderSuccessDialog` (Dialog Xác nhận Đặt hàng thành công) | Dialog / Pop-up Overlay | Flow 1 (Step phản hồi) | `192:2` (File phụ `ALDYFWUZ...`, Page Prototype) |

| **S6** | `S6_LiveOrderTracking` (Theo dõi Đơn hàng thời gian thực) | Root Screen (Tab Đơn hàng) | Flow 1 (End), Flow 2 (Start), Flow 3 (Khởi phát & End) | `3:700` (File chính, Page Student Screens) |

| **S7** | `S7_PickupQRCode` (Mã QR Nhận hàng tại Cổng KTX) | Nested Screen / Modal Bottom Sheet | Flow 2 (Step / Alt) | `3:284` (File chính, Page Student Screens) |

| **S8** | `S8_DisputeRefund` (Khiếu nại và hoàn tiền) | Nested Screen | Flow 3 (Recovery) | `8:6980` (File chính); Tương tác `85:247`, Gửi xong `192:19` (File phụ) |

| **S9** | `S9_ReviewFeedback` (Đánh giá và phản hồi) | Nested Screen | Flow 2 (End) | `8:6735` (File chính, Page Student Screens) |

| **S10** | `S10_OrderHistory` (Lịch sử đơn hàng) | Root Screen (Tab Lịch sử) | Flow 3 (Khởi phát & End) | `26:2` (File chính, Page Student Screens) |

---

## 2. Đặc tả từng màn

### S1 – S1_FoodSearchHome (Tra cứu đặt đồ ăn)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Giúp sinh viên (Nguyễn Văn Tuấn) khám phá các quán ăn bình dân quanh khu vực KTX ĐHQG và đặt món kịp trước giờ đóng bếp ca trưa (Cut-off Time 10h45), giải quyết trực tiếp pain point hay quên/bỏ bữa do mải học/chơi game và metric hoàn tất đặt món < 30 giây.
* **Nội dung hiển thị:**
  - Header: Lời chào cá nhân hóa "Chào Tuấn 👋", bộ chọn địa điểm nhận hàng mặc định "Cổng KTX Khu A ▾", biểu tượng Thông báo (kèm badge) và Giỏ hàng.
  - Thanh tìm kiếm món ăn / quán ăn (`Text Field`).
  - Banner đếm ngược Cut-off time: Hiển thị đồng hồ đếm ngược cho ca trưa (11h30) và ca tối (18h00) kèm cảnh báo thời gian còn lại.
  - Bộ lọc nhanh theo khu vực: Chip lọc "Tất cả", "KTX Khu A", "KTX Khu B", "Làng Đại học".
  - Danh sách quán ăn & món ăn nổi bật: Hiển thị theo lưới thẻ món (`Food Item Card` dạng Vertical) gồm ảnh đại diện, tên món, tên quán, khoảng cách/cổng KTX, giá bán, số sao đánh giá và nút thêm nhanh.
  - Bottom Navigation Bar cố định chân trang (Active: Tab Home).
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):** 
  - Thuộc **Flow 1** với vai trò **Start Point** (Bắt đầu hành trình đặt món ca trưa).
  - Thuộc **Flow 2** với vai trò **End Point** (Điểm đích quay về sau khi hoàn thành đánh giá đơn ở S9).
* **Hành động chính:** Bấm vào thẻ món ăn / quán ăn mong muốn để chuyển sang màn hình Chi tiết Quán ăn & Thực đơn (`S2_StoreDetailMenu`).
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: Khởi động ứng dụng sau đăng nhập (`S0_StudentLogin`), hoặc quay về từ `S9_ReviewFeedback` sau khi đánh giá xong.
  - Đi tới: `S2_StoreDetailMenu` (khi chọn quán/món), `S4_GroupCartCheckout` (khi bấm icon Giỏ hàng trên header), hoặc chuyển tab qua Bottom Navigation (`S6`, `S10`).
* **Node Figma:** `4:1539` (File chính "Prototype", Page Student Screens, frame width 390).  
  *(⚠ GHI CHÚ TIẾN ĐỘ: Frame hiện rộng 390dp thay vì chuẩn 360×800dp. Chưa gắn instance Master Component C03/C04).*

---

### S2 – S2_StoreDetailMenu (Chi tiết Quán ăn & Thực đơn)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Cho phép sinh viên xem toàn bộ thực đơn của quán ăn bình dân gần KTX, cập nhật thông báo vận hành của quán (tránh tình trạng quán đóng cửa đột xuất), chọn món với mức giá sinh viên không bị độn phí chiết khấu cao.
* **Nội dung hiển thị:**
  - Top App Bar: Nút Back, nút Lưu quán yêu thích (Icon Tim), nút Chia sẻ.
  - Thông tin quán ăn: Ảnh bìa quán, tên quán ("Cơm Tấm Cô Ba - KTX Khu A"), điểm đánh giá (4.8 ⭐), cự ly di chuyển, giờ mở cửa.
  - Bảng tin quán: Thông báo nhanh từ chủ quán (ví dụ: "Hôm nay có sườn non nướng mật ong").
  - Thanh phân loại danh mục thực đơn: Cơm, Bún/Phở, Món thêm, Nước giải khát.
  - Danh sách món ăn: Thẻ món nằm ngang (`Food Item Card` dạng Horizontal) gồm ảnh thumbnail 80×80dp, tên món, mô tả topping, đơn giá, nút `+ Thêm` hoặc nút `Hết hàng` (Sold out).
  - Thanh xem trước giỏ hàng nổi (Floating Cart Bar) ở đáy màn hình hiển thị số lượng món đã chọn và tổng tạm tính.
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):** Thuộc **Flow 1** với vai trò **Step (Màn hình trung gian khám phá thực đơn)**.
* **Hành động chính:** Bấm nút `+ Thêm` trên món ăn để mở Modal Tùy biến món ăn (`S3_FoodCustomization`).
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: `S1_FoodSearchHome` (chọn quán từ trang chủ), hoặc `S11_FavoriteList`.
  - Đi tới: `S3_FoodCustomization` (khi bấm chọn món), hoặc `S4_GroupCartCheckout` (khi bấm thanh Giỏ hàng nổi dưới đáy). Bấm Back quay lại `S1`.
* **Node Figma:** `3:479` (File chính "Prototype", Page Student Screens, frame width 390).

---

### S3 – S3_FoodCustomization (Tùy biến món ăn)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Đáp ứng nhu cầu cá nhân hóa khẩu vị ăn uống của sinh viên (ít cay, không hành, thêm cơm/topping) mà không cần chat riêng với quán; giúp việc chốt món diễn ra tức thì dưới 10 giây.
* **Nội dung hiển thị:**
  - Modal Bottom Sheet trượt từ đáy màn hình lên, có thanh kéo Handle Bar.
  - Ảnh lớn món ăn, tên món ("Cơm Tấm Sườn Bì Chả"), đơn giá cơ sở.
  - Nhóm tùy chọn Kích cỡ (Size): Radio button chọn Size Vừa (Mặc định, +0đ) hoặc Size Lớn (+10.000đ).
  - Nhóm Mức độ cay / Ngọt: Radio button chọn Không cay / Cay vừa / Cay nhiều.
  - Nhóm Topping thêm: Checkbox chọn nhiều món phụ (Trứng ốp la +5.000đ, Chả thêm +7.000đ, Canh chua +5.000đ).
  - Trường nhập liệu ghi chú (`Text Field`): "Ghi chú cho quán (ví dụ: Nhiều cơm, không mỡ hành...)".
  - Bộ điều chỉnh số lượng món: Nút `[-]` Số lượng `[+]`.
  - Nút Sticky CTA chân trang: "Thêm vào giỏ - 35.000đ".
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):** Thuộc **Flow 1** với vai trò **Step (Modal tùy biến món)**.
* **Hành động chính:** Bấm nút "Thêm vào giỏ - [Giá tiền]" (`FilledButton`) để lưu cấu hình món và cập nhật giỏ hàng.
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: `S2_StoreDetailMenu` khi bấm nút thêm món.
  - Đi tới: Tự động đóng Modal và quay lại `S2_StoreDetailMenu` với thanh giỏ hàng nổi đã cập nhật giá trị.
* **Node Figma:** `8:7296` (File chính "Prototype", Page Student Screens, frame width 390).

---

### S4 – S4_GroupCartCheckout (Giỏ hàng & Thanh toán gom đơn)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Khắc phục triệt để pain point phí ship cao bằng cơ chế gom đơn tập trung tại KTX; sinh viên chọn chính xác Cổng KTX và ca nhận hàng cố định (Ca trưa 11h30), hỗ trợ nhập mã giảm giá sinh viên và chọn phương thức thanh toán linh hoạt.
* **Nội dung hiển thị:**
  - Top App Bar: Nút Back, Tiêu đề "Giỏ hàng & Thanh toán".
  - Địa điểm nhận hàng cố định: Dropdown/Radio chọn "Cổng KTX Khu A" hoặc "Cổng KTX Khu B".
  - Ca nhận hàng gom đơn: Chọn "Ca trưa (11:30 - 12:00)" hoặc "Ca tối (18:00 - 18:30)" kèm nhắc nhở Cut-off time.
  - Danh sách tóm tắt món trong giỏ: Tên món, topping đã chọn, số lượng `[-] [1] [+]`, nút xóa món.
  - Ô áp dụng mã giảm giá (`Text Field`): Nhập mã voucher kèm nút "Áp dụng".
  - Phương thức thanh toán: 2 tùy chọn Radio button:
    1. Chuyển khoản online (VietQR) – Khuyên dùng.
    2. Tiền mặt khi nhận hàng (COD).
  - Bảng tính tiền: Tạm tính, Phí dịch vụ gom đơn (0đ hoặc 3.000đ), Giảm giá voucher, Tổng thanh toán nổi bật (`type-headline-large`).
  - Nút thanh toán cố định đáy màn hình (`FilledButton` 48dp).
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):**
  - Thuộc **Flow 1**: Đóng vai trò **Step (Chốt đơn gom)** trong Happy Path.
  - Đóng vai trò **Alternative Path** khi từ S5 gặp lỗi thanh toán quay trở lại S4 để chuyển sang COD.
* **Hành động chính:** 
  - Nếu chọn VietQR: Bấm "Tiến hành thanh toán" để chuyển sang `S5_OnlinePayment`.
  - Nếu chọn COD: Bấm "Xác nhận đặt đơn" để trực tiếp kích hoạt Dialog `S5_Success`.
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: `S2_StoreDetailMenu` hoặc icon Giỏ hàng tại `S1_FoodSearchHome`; hoặc quay lại từ `S5_OnlinePayment` (nhánh đổi sang COD).
  - Đi tới: `S5_OnlinePayment` (nếu chọn VietQR) HOẶC `S5_Success` (nếu chọn COD). Bấm Back quay lại `S2`.
* **Node Figma:** `3:2` (File chính "Prototype", Page Student Screens, frame width 390).

---

### S5 – S5_OnlinePayment (Thanh toán online)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Phục vụ thói quen thanh toán không tiền mặt của sinh viên qua chuyển khoản ngân hàng bằng mã VietQR động chứa sẵn chính xác số tiền và cú pháp mã đơn, tránh nhầm lẫn nội dung chuyển khoản.
* **Nội dung hiển thị:**
  - Top App Bar: Nút Back, Tiêu đề "Thanh toán VietQR".
  - Thông tin đơn hàng: Mã đơn `#KTX-8492`, Tổng tiền cần thanh toán (ví dụ: `42.000đ`).
  - Khung mã VietQR động chính giữa màn hình (kèm nút "Tải mã QR" hoặc "Mở App Ngân hàng").
  - Thông tin tài khoản thụ hưởng: Tên chủ tài khoản, Ngân hàng, Số tài khoản kèm icon "Sao chép nhanh".
  - Nội dung chuyển khoản bắt buộc: Chuỗi mã định danh (ví dụ: `KTX8492 TUAN`).
  - Đồng hồ đếm ngược hiệu lực thanh toán (10:00 phút).
  - Nút liên kết chuyển đổi: "Gặp sự cố chuyển khoản? Đổi sang Tiền mặt (COD)".
  - Nút CTA chính chân trang: "Đã hoàn tất chuyển khoản" (`FilledButton`).
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):**
  - Thuộc **Flow 1** với vai trò **Step (Thực hiện thanh toán online)** trong Happy Path.
  - Điểm rẽ nhánh **Alternative Path**: Khi app ngân hàng lỗi/tài khoản hết tiền $\rightarrow$ bấm nút đổi sang COD để quay lại S4.
* **Hành động chính:** Bấm nút "Đã hoàn tất chuyển khoản" để hệ thống kiểm tra và mở Dialog `S5_Success`.
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: `S4_GroupCartCheckout` khi chọn hình thức Chuyển khoản online.
  - Đi tới: `S5_Success` (khi thanh toán hoàn tất); hoặc quay lại `S4_GroupCartCheckout` (khi bấm Đổi phương thức COD hoặc nút Back).
* **Node Figma:** `8:7969` (File chính "Prototype", Page Student Screens, frame width 390).

---

### S5_Success – S5_OrderSuccessDialog (Dialog Xác nhận Đặt hàng thành công)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Cung cấp phản hồi tức thì (Immediate Feedback theo Heuristic Nielsen #1) xác nhận đơn hàng đã được chuyển tới bếp quán ăn; thông báo rõ giờ có mặt tại cổng KTX nhận hàng để sinh viên yên tâm tiếp tục việc học/nghỉ ngơi.
* **Nội dung hiển thị:**
  - Dialog pop-up nổi trên nền tối phủ mờ (`rgba(0,0,0,0.5)`).
  - Minh họa Icon checkmark tròn thành công màu xanh lá/cam lấp lánh (64dp).
  - Tiêu đề: "Đặt đơn ca trưa thành công!" (`Headline Medium`).
  - Nội dung chi tiết: "Mã đơn: `#KTX-8492`. Đơn hàng đã gửi tới quán. Vui lòng có mặt tại **Cổng KTX Khu A** lúc **11:30** để nhận món."
  - Nút CTA chính: "Theo dõi đơn hàng ngay" (`FilledButton` 48dp).  
  *(⚠ MÂU THUẪN NGUỒN (d): Trong Figma Page Components chỉ có component `123:72` mang tên "Dialog / Xác nhận giao hàng KTX" (dùng cho đối soát giao nhận), còn Dialog Đặt hàng thành công này nằm ở node `192:2` file phụ, chưa được chuẩn hóa thành Master Component trong Page Components của file chính).*
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):** Thuộc **Flow 1** với vai trò **Step phản hồi thành công (Confirmation Overlay)** trước khi đóng flow đặt hàng.
* **Hành động chính:** Bấm nút "Theo dõi đơn hàng ngay" để chuyển sang `S6_LiveOrderTracking`.
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: `S5_OnlinePayment` (sau khi bấm hoàn tất chuyển khoản) HOẶC từ `S4_GroupCartCheckout` (sau khi bấm xác nhận đặt đơn COD).
  - Đi tới: `S6_LiveOrderTracking`.
* **Node Figma:** `192:2` (File phụ "Lab 2 Food Ordering App" key `ALDYFWUZ72BaeyulpVi7uY`, Page Prototype, frame width 440).

---

### S6 – S6_LiveOrderTracking (Theo dõi Đơn hàng thời gian thực)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Giải quyết tình trạng chen chúc và tài xế gọi điện liên tục tại cổng KTX bằng cách minh bạch tiến trình đơn hàng thời gian thực; giúp Tuấn biết chính xác thời điểm tài xế tới cổng KTX để xuống nhận hàng, đạt metric nhận đồ < 20 giây.
* **Nội dung hiển thị:**
  - Top App Bar: Nút Đóng/Về trang chủ, Tiêu đề mã đơn `#KTX-8492`, nút Hotline hỗ trợ.
  - Thanh tiến trình trạng thái trực tiếp (Stepper Progress):
    `1. Đã nhận đơn` $\rightarrow$ `2. Đang nấu` $\rightarrow$ `3. Đang gom chuyến` $\rightarrow$ `4. Đã tới Cổng KTX`.
  - Bộ đếm thời gian dự kiến shipper tới cổng (ví dụ: "Dự kiến tới cổng KTX trong: 12 phút").
  - Thẻ thông tin người giao hàng (Shipper Card): Ảnh đại diện, Tên tài xế, Biển số xe ("59-X1 123.45"), Vị trí đứng đón tại cổng KTX ("Cột cờ Cổng Khu A"), nút gọi điện nhanh.
  - Tóm tắt danh sách món ăn trong túi gom.
  - Nút phụ "Hủy đơn hàng" (chỉ kích hoạt khi quán chưa bấm nấu; vô hiệu hóa khi quán đã nấu).
  - Nút liên kết phụ: "Báo cáo sự cố đơn hàng" (khiếu nại nếu đồ ăn có vấn đề sau khi nhận).
  - Nút CTA chính nổi bật: "Mở Mã QR Nhận Hàng" (`FilledButton` 48dp, kích hoạt sáng khi shipper cập nhật đã đến cổng).
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):**
  - Thuộc **Flow 1**: Đóng vai trò **End Point** (Hoàn tất chu trình đặt món).
  - Thuộc **Flow 2**: Đóng vai trò **Start Point** (Bắt đầu chu trình nhận hàng tại cổng KTX).
  - Thuộc **Flow 3**: Đóng vai trò **Điểm khởi phát báo lỗi** (bấm Báo cáo sự cố) và **End Point** (cập nhật trạng thái "Đang chờ xử lý hoàn tiền").
* **Hành động chính:** Bấm nút "Mở Mã QR Nhận Hàng" để mở Modal `S7_PickupQRCode` khi shipper tới cổng.
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: `S5_Success` (sau khi đặt hàng thành công), hoặc từ Tab "Đơn hàng" trên Bottom Navigation Bar, hoặc từ `S10_OrderHistory`, hoặc từ thông báo Push.
  - Đi tới: `S7_PickupQRCode` (để nhận hàng), hoặc `S8_DisputeRefund` (khi cần khiếu nại), hoặc quay về `S1_FoodSearchHome`.
* **Node Figma:** `3:700` (File chính "Prototype", Page Student Screens, frame width 390).

---

### S7 – S7_PickupQRCode (Mã QR Nhận hàng tại Cổng KTX)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Giải quyết triệt để nỗi đau cổng KTX đông đúc dễ thất lạc/lấy nhầm đồ ăn và shipper gọi điện liên tục; hỗ trợ đối soát dưới ánh nắng gắt thông qua mã QR độ tương phản cao kèm 4 số cuối SĐT dự phòng, đạt tiêu chí nhận hàng < 20 giây.
* **Nội dung hiển thị:**
  - Modal / Card nhận hàng nổi bật trên nền tương phản cao.
  - Mã QR đơn hàng kích thước lớn (tối thiểu 180×180dp), hiển thị rõ ràng để camera shipper quét nhanh.
  - **Dòng thông tin dự phòng dưới mã QR:** Hiển thị nổi bật **4 số cuối Số điện thoại** của sinh viên (ví dụ: `Đuôi SĐT: •••• 2947`) dùng để đọc đối soát thủ công khi chói nắng.
  - Mã đơn hàng `#KTX-8492` và Địa điểm nhận ("Cổng KTX Khu A").
  - Danh sách tóm tắt các món trong bọc hàng (để sinh viên tự kiểm tra đối chiếu tại chỗ).
  - Hướng dẫn nhanh: "Đưa mã này cho tài xế quét hoặc đọc 4 số cuối SĐT để nhận đúng phần ăn của bạn."
  - Nút CTA chính: "Đã nhận được thức ăn" (`FilledButton` 48dp).
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):**
  - Thuộc **Flow 2** với vai trò **Step (Xác thực giao nhận)** trong Happy Path (quét QR).
  - Cung cấp **Alternative Path** tích hợp ngay trên màn hình: Khi camera shipper không quét được do nắng chói / màn hình trầy, sinh viên đọc 4 số cuối SĐT hiển thị ngay dưới QR để tài xế nhập tay.
* **Hành động chính:** Bấm nút "Đã nhận được thức ăn" (hoặc tự động chuyển khi shipper quét thành công) để chuyển sang `S9_ReviewFeedback`.
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: `S6_LiveOrderTracking` khi bấm nút "Mở Mã QR Nhận Hàng".
  - Đi tới: `S9_ReviewFeedback` (sau khi nhận xong đồ ăn); hoặc bấm icon Đóng `(X)` quay lại `S6_LiveOrderTracking`.
* **Node Figma:** `3:284` (File chính "Prototype", Page Student Screens, frame width 390).

---

### S8 – S8_DisputeRefund (Khiếu nại và hoàn tiền)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Bảo vệ quyền lợi tài chính của sinh viên nội trú khi món ăn gặp sự cố (đổ vỡ bao bì, giao thiếu món, sai ghi chú khẩu vị); quy trình khiếu nại minh bạch giúp sinh viên nhận lại tiền bồi hoàn nhanh chóng mà không phải tranh cãi.
* **Nội dung hiển thị:**
  *(⚠ MÂU THUẪN NGUỒN (c): Trong `user-flow.md` mô tả đơn giản là chọn nguyên nhân và nhập STK nhận tiền hoàn. Tuy nhiên trên Figma thiết kế chi tiết và chặt chẽ hơn nhiều: cho phép chọn nhiều sự cố, chọn nhiều món bị ảnh hưởng kèm nút 'Chọn tất cả', hệ thống tự động cộng dồn số tiền hoàn tương ứng, và cho phép chọn 1 trong 2 kênh nhận tiền hoàn: Ví KTX Food hoặc Chuyển khoản ngân hàng).*
  - Top App Bar: Nút Back, Tiêu đề "Khiếu nại & Hoàn tiền".
  - Khung thông tin đơn hàng gặp sự cố: Mã đơn `#KTX-8492`, Tên quán ăn.
  - Phần 1 - Chọn loại sự cố (Hỗ trợ Checkbox chọn nhiều):
    - [ ] Thức ăn bị đổ vỡ, nghiêng tràn bao bì
    - [ ] Giao thiếu món / thiếu topping
    - [ ] Giao sai món / không đúng ghi chú khẩu vị
    - [ ] Thức ăn không đảm bảo vệ sinh / chất lượng
  - Phần 2 - Danh sách món ăn bị ảnh hưởng:
    - Danh sách các món trong đơn kèm checkbox chọn từng món.
    - Nút chọn nhanh: "Chọn tất cả món".
    - Ô hiển thị tự động: **Số tiền yêu cầu hoàn lại** (tự động tính dựa trên tổng giá tiền các món được chọn).
  - Phần 3 - Bằng chứng thực tế:
    - Khu vực tải ảnh chụp thực tế: Nút chụp ảnh / tải ảnh từ thư viện (tối thiểu 1 ảnh bằng chứng).
    - Trường văn bản mô tả chi tiết sự cố (`Text Field`).
  - Phần 4 - Phương thức nhận tiền hoàn (Radio button chọn 1 trong 2):
    1. **Hoàn về Ví KTX Food** (Tiền về tức thì sau khi duyệt, dùng đặt đơn sau).
    2. **Chuyển khoản Ngân hàng** (Hiển thị các ô `Text Field` nhập Tên ngân hàng, Số tài khoản, Tên chủ tài khoản).
  - Nút CTA chính: "Gửi yêu cầu khiếu nại" (`FilledButton` 48dp).
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):** Thuộc **Flow 3** với vai trò **Recovery Path (Màn hình giải quyết sự cố và phục hồi quyền lợi)**.
* **Hành động chính:** Bấm nút "Gửi yêu cầu khiếu nại" (`FilledButton`) để gửi hồ sơ bồi hoàn lên hệ thống.
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: `S6_LiveOrderTracking` (sau khi nhận đồ ăn phát hiện lỗi) HOẶC từ `S10_OrderHistory` (chi tiết đơn hàng đã giao).
  - Đi tới: Màn hình gửi thành công (node `192:19` file phụ) $\rightarrow$ quay lại `S6_LiveOrderTracking` hoặc `S10_OrderHistory` với nhãn trạng thái đổi thành "Đang chờ xử lý hoàn tiền". Bấm Back quay lại màn hình trước.
* **Node Figma:** `8:6980` (File chính "Prototype"); File phụ "Lab 2 Food Ordering App": node `85:247` (tương tác chọn món/sự cố) và `192:19` (gửi khiếu nại thành công).

---

### S9 – S9_ReviewFeedback (Đánh giá và phản hồi)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Khép lại chu trình trải nghiệm ẩm thực, giúp sinh viên phản hồi chất lượng món của quán và thái độ giao hàng của shipper KTX, tạo dữ liệu đánh giá tin cậy cho cộng đồng sinh viên nội trú.
* **Nội dung hiển thị:**
  - Top App Bar: Nút Đóng `(X)` / Bỏ qua, Tiêu đề "Đánh giá đơn hàng".
  - Phần 1 - Đánh giá Quán ăn:
    - Tên quán và logo quán.
    - Thanh đánh giá 5 sao ⭐ (tương tác chạm để chọn từ 1 đến 5 sao).
    - Các chip nhận xét nhanh: "Món ăn ngon miệng", "Đóng gói cẩn thận", "Đúng khẩu vị", "Giao đúng giờ".
    - Khung nhập nhận xét chi tiết cho quán (`Text Field` nhiều dòng).
  - Phần 2 - Đánh giá Người giao hàng (Shipper):
    - Tên và avatar shipper KTX.
    - Thanh đánh giá 5 sao ⭐ cho tài xế.
    - Chip nhận xét nhanh: "Thân thiện, lịch sự", "Đúng giờ tại cổng KTX", "Bảo quản đồ cẩn thận".
    - Khung nhập góp ý riêng cho shipper.
  - Nút CTA chính chân trang: "Gửi đánh giá" (`FilledButton` 48dp).
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):** Thuộc **Flow 2** với vai trò **End Point (Kết thúc chu trình giao nhận & đánh giá)**.
* **Hành động chính:** Bấm nút "Gửi đánh giá" (`FilledButton`) để ghi nhận phản hồi và quay về màn hình chính.
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: `S7_PickupQRCode` (sau khi hoàn tất nhận món), hoặc từ nút "Đánh giá" trong `S10_OrderHistory`.
  - Đi tới: `S1_FoodSearchHome` (hoàn tất Flow 2); hoặc quay lại `S10_OrderHistory` nếu mở từ lịch sử.
* **Node Figma:** `8:6735` (File chính "Prototype", Page Student Screens, frame width 390).

---

### S10 – S10_OrderHistory (Lịch sử đơn hàng)
* **Mục đích (ý đồ thiết kế, gắn pain point persona):** Giúp sinh viên tra cứu lại các bữa ăn đã đặt trong tuần, nhanh chóng đặt lại các món quen miệng chỉ với một thao tác ("Đặt lại đơn này"), hoặc làm điểm xuất phát để gửi khiếu nại cho các đơn hàng cũ gặp lỗi.
* **Nội dung hiển thị:**
  - Top App Bar: Tiêu đề màn hình "Lịch sử đơn hàng".
  - Thanh phân loại trạng thái (Segmented Tabs): "Tất cả", "Đang xử lý", "Hoàn tất", "Đã hủy".
  - Danh sách thẻ đơn hàng cũ:
    - Mã đơn hàng `#KTX-...`, ngày giờ đặt, tên quán ăn.
    - Huy hiệu trạng thái đơn: "Đã giao thành công" (Xanh lá), "Đang xử lý hoàn tiền" (Cam/Đỏ), "Đã hủy" (Xám).
    - Tóm tắt danh sách món và tổng số tiền thanh toán.
    - Cặp nút hành động trên mỗi thẻ đơn:
      - Nút "Đặt lại đơn này" (`Secondary Button`): Thêm lại nguyên vẹn các món vào giỏ hàng.
      - Nút "Khiếu nại / Hoàn tiền" (`Outline/Danger Button`): Dành cho đơn vừa giao có sự cố.
      - Nút "Đánh giá" (nếu đơn chưa được chấm điểm).
  - Bottom Navigation Bar cố định chân trang (Active: Tab Lịch sử / Orders).
* **Thuộc flow nào & vai trò (Start/End/Alt/Error/Recovery):**
  - Thuộc **Flow 3**: Đóng vai trò **Điểm khởi phát báo lỗi (Start Point thay thế của Flow 3)** khi sinh viên về phòng kiểm tra lại lịch sử để khiếu nại.
  - Đồng thời là nơi hiển thị trạng thái hoàn tất phục hồi (End Point cập nhật trạng thái "Đang chờ xử lý hoàn tiền").
* **Hành động chính:** Bấm nút "Khiếu nại / Hoàn tiền" trên thẻ đơn hàng có sự cố để mở `S8_DisputeRefund` (trong Flow 3).
* **Vào từ đâu / đi tới đâu:**
  - Vào từ: Tab "Lịch sử" (Orders) trên Bottom Navigation Bar từ bất kỳ màn hình chính nào.
  - Đi tới: `S8_DisputeRefund` (khi cần khiếu nại), `S6_LiveOrderTracking` (nếu đơn đang trong tiến trình giao), `S2_StoreDetailMenu` hoặc `S4_GroupCartCheckout` (khi bấm Đặt lại đơn này).
* **Node Figma:** `26:2` (File chính "Prototype", Page Student Screens, frame width 390).

---

## 3. Bảng ánh xạ Màn hình ↔ Flow

*(Giữ nguyên vẹn 100% nội dung và phân loại đối chiếu từ Bảng Mục 3 của tài liệu `ux/user-flow.md`)*

| Mã Màn hình | Tên Màn hình (Khớp chính xác Figma) | Flow 1 (Đặt món & Thanh toán) | Flow 2 (Nhận hàng tại Cổng) | Flow 3 (Báo lỗi & Hoàn tiền) | Vai trò bổ trợ trong hệ thống |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **S0** | **Đăng nhập / Xác thực sinh viên** | | | | Xác thực định danh & phân luồng KTX |

| **S1** | **Tra cứu đặt đồ ăn** | **X** *(Bắt đầu)* | **X** *(Kết thúc)* | | Khám phá quán ăn & lọc ca nhận |

| **S2** | **Chi tiết Quán ăn & Thực đơn** | **X** | | | Xem menu & bảng tin thông báo quán |

| **S3** | **Tùy biến món ăn** | **X** | | | Tùy chọn kích cỡ, topping, ghi chú vị |

| **S4** | **Giỏ hàng & Thanh toán gom đơn** | **X** | | | Chọn điểm cổng KTX, ca nhận, mã giảm giá |

| **S5** | **Thanh toán online** | **X** | | | Quét VietQR động chính xác số tiền |

| **S5_Success** | **Dialog Xác nhận Đặt hàng thành công** | **X** | | | Phản hồi xác nhận đặt đơn tức thì |

| **S6** | **Theo dõi Đơn hàng thời gian thực** | **X** *(Kết thúc)* | **X** *(Bắt đầu)* | **X** | Theo dõi tiến trình & mở nhận hàng/khiếu nại |

| **S7** | **Mã QR Nhận hàng tại Cổng KTX** | | **X** | | Đối soát nhận hàng nhanh với shipper |

| **S8** | **Khiếu nại và hoàn tiền** | | | **X** *(Phục hồi)* | Biểu mẫu giải quyết sự cố đơn hàng |

| **S9** | **Đánh giá và phản hồi** | | **X** *(Kết thúc)* | | Chấm điểm sao cho Quán ăn và Shipper |

| **S10** | **Lịch sử đơn hàng** | | | **X** | Tra cứu đơn cũ, đặt lại hoặc khởi tạo khiếu nại |

| **S11** | **Danh sách yêu thích** | | | | Lưu quán quen để đặt lại nhanh |

| **S12** | **Bảng thông báo** | | | | Cập nhật thông báo hệ thống & Cut-off time |

| **S13** | **Hồ sơ cá nhân / Cài đặt tài khoản** | | | | Quản lý thông tin KTX, STK hoàn tiền mặc định |

---

## 4. Ngoài phạm vi flow (S0, S11, S12, S13)

Các màn hình dưới đây thuộc Kiến trúc thông tin (IA) của hệ thống nhưng **không nằm trong 3 User Flows chính** được đặc tả chi tiết của Lab 2. Các màn hình này chỉ được liệt kê tóm tắt theo quy định:

1. **S0 – `S0_StudentLogin` (Màn hình Đăng nhập / Xác thực sinh viên):**
   - **Vị trí trong IA:** Điểm vào ứng dụng (Entry / Authentication).
   - **Node Figma:** `6:4448` (File chính "Prototype", Page Common Screens).
   - **Mục đích tóm tắt:** Xác thực số điện thoại/mật khẩu hoặc OTP, xác thực email sinh viên `@vnuhcm.edu.vn` để nhận ưu đãi nội trú KTX.
   - **Lý do ngoài phạm vi flow:** Là màn hình tiền đề (Pre-requisite Screen) cho toàn bộ hệ thống, không thuộc chu trình thao tác nghiệp vụ đặt món, giao nhận hay khiếu nại của 3 flows.

2. **S11 – `S11_FavoriteList` (Danh sách quán yêu thích):**
   - **Vị trí trong IA:** Màn hình Root cấp cao (Tab Quán quen / Yêu thích trên Bottom Nav).
   - **Node Figma:** `8:7603` (File chính "Prototype", Page Student Screens).
   - **Mục đích tóm tắt:** Lưu trữ các quán ăn ruột của sinh viên để mở nhanh thực đơn mà không cần tìm kiếm lại.
   - **Lý do ngoài phạm vi flow:** Đóng vai trò lối tắt (Shortcut), Flow 1 đã chuẩn hóa điểm xuất phát trực tiếp từ Trang chủ `S1`.

3. **S12 – `S12_NotificationBoard` (Bảng thông báo trung tâm):**
   - **Vị trí trong IA:** Màn hình bổ trợ kích hoạt từ icon Chuông trên Header.
   - **Node Figma:** `8:6181` (File chính "Prototype", Page Student Screens).
   - **Mục đích tóm tắt:** Danh sách thông báo đẩy về biến động trạng thái đơn hàng, tin tức khuyến mãi và cảnh báo giờ Cut-off time.
   - **Lý do ngoài phạm vi flow:** Tương tác nhận hàng ở Flow 2 kích hoạt trực tiếp từ Màn hình theo dõi đơn `S6` hoặc Push Notification mở thẳng `S6`.

4. **S13 – `S13_ProfileSettings` (Hồ sơ cá nhân / Cài đặt tài khoản):**
   - **Vị trí trong IA:** Màn hình Root cấp cao (Tab Tài khoản trên Bottom Nav).
   - **Node Figma:** `6:4763` (File chính "Prototype", Page Common Screens).
   - **Mục đích tóm tắt:** Quản lý thông tin định danh sinh viên, phòng/tòa KTX đang lưu trú, liên kết số tài khoản ngân hàng mặc định, đổi mật khẩu và đăng xuất.
   - **Lý do ngoài phạm vi flow:** Phục vụ cấu hình tài khoản và phân quyền, không trực tiếp tham gia vào luồng giao dịch 3 flows.
