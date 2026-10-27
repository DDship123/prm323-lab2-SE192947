# ĐẶC TẢ QUY TẮC NGHIỆP VỤ (BUSINESS RULES SPECIFICATION)
# HỆ THỐNG ĐẶT ĐỒ ĂN SINH VIÊN KÝ TÚC XÁ ĐHQG-HCM (KTXFOOD)

> **Môn học:** PRM323 – Mobile Programming  
> **Nhóm thực hiện:** `FA26-31-PRM323` (Bùi Bảo Dương, Ngô Hoàng Trường Đạt, Trần Sanh Điền, Quách Ngọc Vinh)  
> **Phiên bản:** 1.0 (Final)  
> **Tài liệu tham chiếu:** [`docs/PRD.md`](PRD.md), [`ux/user-flow.md`](../ux/user-flow.md), [`design/DESIGN.md`](../design/DESIGN.md), [`design/screen-spec.md`](../design/screen-spec.md).

---

## 1. MỤC ĐÍCH & QUY ƯỚC MÃ HÓA

### 1.1. Mục đích tài liệu
Tài liệu này định nghĩa chi tiết toàn bộ các **Quy tắc Nghiệp vụ (Business Rules - BR)** bắt buộc của hệ thống KTXFood. Đây là căn cứ kỹ thuật tối thượng để:
1. Đội ngũ thiết kế UI/UX xây dựng các trạng thái giao diện (Default, Active, Disabled, Error, Loading) trên Figma.
2. Đội ngũ phát triển (Flutter Mobile & Backend API) lập trình logic kiểm tra điều kiện (validation), tính toán tài chính và chuyển đổi trạng thái đơn hàng.
3. Đội ngũ kiểm thử (QA/QC) viết kịch bản kiểm thử (Test Cases).

### 1.2. Bảng phân loại mức độ ràng buộc (Enforcement Levels)
* **STRICT (Bắt buộc tuyệt đối):** Hệ thống chặn ngay lập tức, không cho phép tiếp tục thao tác nếu vi phạm; hiển thị Error state hoặc vô hiệu hóa nút bấm.
* **WARNING (Cảnh báo có điều kiện):** Hệ thống hiển thị hộp thoại xác nhận hoặc banner cảnh báo nhưng vẫn cho phép tiếp tục nếu người dùng chủ động chọn.
* **AUTOMATIC (Hệ thống tự động thực thi):** Hệ thống tự động kích hoạt logic dựa trên sự kiện thời gian thực (Cron Job, Webhook) mà không cần người dùng thao tác.

---

## 2. BẢNG TỔNG HỢP TOÀN BỘ CÁC QUY TẮC NGHIỆP VỤ (MASTER BR TABLE)

| Mã BR | Tên Quy Tắc Nghiệp Vụ | Nhóm Nghiệp Vụ | Màn hình liên quan | Mức độ |
| :---: | :--- | :--- | :---: | :---: |
| **BR-01** | Khung giờ phục vụ theo ca cố định | Gom đơn & Vận hành | S1, S4 | **STRICT** |
| **BR-02** | Giờ chốt đơn (Cut-off Time) & Chuyển ca tự động | Gom đơn & Vận hành | S1, S4 | **AUTOMATIC** |
| **BR-03** | Điều kiện Hủy đơn hàng của Sinh viên | Quản lý Đơn hàng | S6 | **STRICT** |
| **BR-04** | Giới hạn Địa điểm giao nhận cố định tại Cổng KTX | Giao nhận (Fulfillment) | S1, S4, S6 | **STRICT** |
| **BR-05** | Cơ chế Phí vận chuyển chia sẻ (Shared Delivery Fee) | Tài chính & Giá bán | S4 | **AUTOMATIC** |
| **BR-06** | Chính sách Áp dụng Mã giảm giá & Voucher | Khuyến mãi & Giá bán | S4 | **STRICT** |
| **BR-07** | Định dạng & Thời hạn hiệu lực của Mã VietQR | Thanh toán Online | S5 | **STRICT** |
| **BR-08** | Phương thức dự phòng Tiền mặt (COD Fallback) | Thanh toán | S4, S5 | **WARNING** |
| **BR-09** | Thông báo đẩy đồng loạt khi Shipper đến Cổng KTX | Giao nhận (Fulfillment) | S6 | **AUTOMATIC** |
| **BR-10** | Thời gian chờ tối đa tại Cổng & Xử lý vắng mặt | Giao nhận (Fulfillment) | S6, S7 | **STRICT** |
| **BR-11** | Đối soát nhận hàng 2 lớp (Mã QR & 4 số cuối SĐT) | Giao nhận & Bảo mật | S7 | **STRICT** |
| **BR-12** | Điều kiện Đính kèm Ảnh thực tế khi Khiếu nại | Hậu mãi & Hoàn tiền | S8 | **STRICT** |
| **BR-13** | Giới hạn Thời gian gửi Khiếu nại sau nhận hàng | Hậu mãi & Hoàn tiền | S6, S8, S10 | **STRICT** |
| **BR-14** | Thời hạn Xử lý Bồi hoàn Tài chính của Quán | Hậu mãi & Hoàn tiền | S8 | **AUTOMATIC** |
| **BR-15** | Đánh giá độc lập 2 chiều cho Quán & Shipper | Đánh giá & Chất lượng | S9 | **WARNING** |
| **BR-16** | Giới hạn Số lượng đơn tối đa mỗi mẻ gom (Batch Cap) | Vận hành Bếp quán | S1, S2, S4 | **AUTOMATIC** |

---

## 3. CHI TIẾT ĐẶC TẢ TỪNG QUY TẮC NGHIỆP VỤ

---

### NHÓM 1: QUY TẮC GOM ĐƠN THEO CA & THỜI GIAN VẬN HÀNH

#### 📌 BR-01: Khung giờ phục vụ theo ca cố định
* **Mô tả:** Hệ thống KTXFood chỉ vận hành giao hàng định kỳ theo 2 ca cố định mỗi ngày, không phục vụ giao đơn lẻ tẻ:
  - **Ca trưa:** Khung giờ giao nhận tại cổng là `11h30 – 12h30`.
  - **Ca tối:** Khung giờ giao nhận tại cổng là `18h00 – 19h00`.
* **Ràng buộc:**
  - Không cho phép sinh viên hẹn giờ giao lệch khỏi khung giờ chuẩn của ca (ví dụ: không cho phép chọn giao lúc 10h15 hay 14h00).
* **Hành vi UI:**
  - Tại màn hình Giỏ hàng `S4`, mục "Chọn ca nhận" chỉ hiển thị 2 Radio Buttons: `[•] Ca trưa (11:30 - 12:30)` và `[ ] Ca tối (18:00 - 19:00)`.

---

#### 📌 BR-02: Giờ chốt đơn (Cut-off Time) & Chuyển ca tự động
* **Mô tả:** Để đảm bảo chủ quán có đủ 45 phút chuẩn bị và nấu hàng loạt trước khi giao, hệ thống áp dụng hạn chót đặt đơn nghiêm ngặt:
  - Hạn chót ca trưa là **10h45**.
  - Hạn chót ca tối là **17h15**.
* **Logic xử lý:**
  - Nếu thời gian hiện tại $T \le \text{10h45}$: Đơn hàng được tính vào Ca trưa.
  - Nếu $\text{10h45} < T \le \text{17h15}$: Tùy chọn Ca trưa bị làm mờ (`Disabled`). Toàn bộ đơn hàng tự động chuyển sang phục vụ cho Ca tối (`18h00`).
  - Nếu $T > \text{17h15}$: Tự động chuyển đơn sang Ca trưa ngày hôm sau.
* **Hành vi UI:**
  - Trang chủ `S1` hiển thị đồng hồ đếm ngược: *"Chốt ca trưa sau 00:24:15"*.
  - Khi hết giờ chốt, hiển thị Inline Banner cảnh báo màu vàng cam `C09`: *"Bếp ca trưa đã đóng! Đơn của bạn sẽ được giao vào ca tối (18:00)"*.

---

#### 📌 BR-03: Điều kiện Hủy đơn hàng của Sinh viên
* **Mô tả:** Bảo vệ quyền lợi của chủ quán ăn tránh lãng phí nguyên liệu đã chế biến theo mẻ gom.
* **Logic xử lý:**
  - Sinh viên **CHỈ ĐƯỢC PHÉP HỦY ĐƠN** khi đơn hàng đang ở trạng thái `Chờ xác nhận` hoặc `Đã tiếp nhận`, và trước thời điểm quán bấm *"Bắt đầu nấu"*.
  - Một khi quán ăn đã kích hoạt trạng thái `Đang nấu` (thường diễn ra ngay sau giờ Cut-off Time), sinh viên **KHÔNG THỂ HỦY ĐƠN**.
* **Hành vi UI:**
  - Màn hình Theo dõi `S6`: Nút "Hủy đơn hàng" chuyển sang màu xám mờ (`Disabled Button C01`).
  - Nếu bấm hủy khi còn hợp lệ, hệ thống kích hoạt **Confirm Pop-up Dialog `C06`** yêu cầu xác nhận 2 bước: *"Quán chuẩn bị nấu mẻ gom, bạn có chắc chắn muốn hủy đơn #KTX...?"*

---

### NHÓM 2: QUY TẮC ĐỊA ĐIỂM NHẬN HÀNG & TÀI CHÍNH

#### 📌 BR-04: Giới hạn Địa điểm giao nhận cố định tại Cổng KTX
* **Mô tả:** Do nội quy Ban Quản lý KTX ĐHQG cấm xe máy vào nội khu, sinh viên bắt buộc phải chọn 1 trong 3 điểm nhận hàng cố định:
  1. `Cổng KTX Khu A (Cổng chính - Đường Tạ Quang Bửu)`
  2. `Cổng KTX Khu A (Cổng phụ - Trạm xe buýt)`
  3. `Cổng KTX Khu B (Cổng chính - Đối diện Tòa BA)`
* **Ràng buộc:**
  - Không cho phép nhập địa chỉ tự do dạng text (như "Phòng 302 Tòa B4").
  - Mọi đơn hàng trong cùng một chuyến gom phải có cùng điểm đến là một cổng KTX duy nhất.

---

#### 📌 BR-05: Cơ chế Phí vận chuyển chia sẻ (Shared Delivery Fee)
* **Mô tả:** Chi phí giao hàng được tối ưu hóa nhờ gom chuyến chở tập trung:
  - Phí giao hàng tiêu chuẩn đồng giá: **3.000đ / đơn hàng** (cho KTX Khu A) và **5.000đ / đơn hàng** (cho KTX Khu B do khoảng cách xa hơn).
  - **Chính sách Gom nhóm cùng phòng (Group Order):** Nếu giỏ hàng có từ 3 phần ăn trở lên từ cùng một quán ăn về cùng một điểm nhận, hệ thống tự động áp dụng **Miễn phí vận chuyển (Freeship 100%)**.
* **Công thức tính tổng tiền đơn hàng:**
  $$\text{Tổng thanh toán} = \sum (\text{Đơn giá món} \times \text{Số lượng} + \text{Topping}) + \text{Phí ship gom} - \text{Mã giảm giá}$$

---

#### 📌 BR-06: Chính sách Áp dụng Mã giảm giá & Voucher
* **Mô tả:**
  - Mỗi đơn hàng chỉ được áp dụng tối đa **01 Mã giảm giá của Quán** và **01 Mã ưu đãi vận chuyển của KTXFood**.
  - Không áp dụng giảm giá nếu tổng tiền món ăn nhỏ hơn giá trị đơn hàng tối thiểu quy định của voucher (thường là 30.000đ).

---

### NHÓM 3: QUY TẮC THANH TOÁN

#### 📌 BR-07: Định dạng & Thời hạn hiệu lực của Mã VietQR
* **Mô tả:**
  - Mã VietQR sinh ra tại màn hình `S5` là **VietQR động (Dynamic QR)** theo chuẩn NAPAS 247.
  - Mã QR phải được nhúng cứng chính xác: (1) Số tài khoản quán/hệ thống, (2) Mã ngân hàng, (3) Số tiền chính xác từng đồng, (4) Nội dung chuyển khoản chuẩn cú pháp: `KTXFOOD [Mã_Đơn_Hàng]`.
* **Thời hạn thanh toán:**
  - Mã VietQR có hiệu lực đếm ngược trong vòng **10 phút**.
  - Nếu sau 10 phút hệ thống chưa nhận được Webhook thanh toán thành công, đơn hàng tự động chuyển sang trạng thái `Thanh toán thất bại / Hết hạn`.

---

#### 📌 BR-08: Phương thức dự phòng Tiền mặt (COD Fallback)
* **Mô tả:**
  - Nếu trong quá trình quét VietQR tại `S5`, tài khoản ngân hàng của sinh viên không đủ số dư hoặc app ngân hàng bảo trì kết nối, sinh viên được bấm nút *"Đổi sang Tiền mặt khi nhận (COD)"*.
  - Khi chuyển sang COD, đơn hàng được xác nhận ngay lập tức, và hệ thống ghi chú lên thẻ Shipper: *"Đơn cần thu tiền mặt: [Số_Tiền]đ"*.

---

### NHÓM 4: QUY TẮC GIAO NHẬN & ĐỐI SOÁT TẠI CỔNG KTX

#### 📌 BR-09: Thông báo đẩy đồng loạt khi Shipper đến Cổng KTX
* **Mô tả:**
  - Khi shipper di chuyển đến cổng KTX, shipper bấm nút *"Đã đến cổng KTX"* trên app tài xế.
  - Hệ thống tự động kích hoạt **Push Notification đồng loạt** đến toàn bộ sinh viên có đơn trong chuyến gom đó kèm thông tin:
    > *"Shipper [Tên_Tài_Xế] (Xe: [Biển_Số]) đã có mặt tại Cổng KTX Khu A. Vui lòng xuống nhận món trong 15 phút!"*
  - Ứng dụng sinh viên tự động chuyển thẻ trạng thái sang màu xanh lá và hiển thị nút *"Mở Mã QR Nhận hàng"*.

---

#### 📌 BR-10: Thời gian chờ tối đa tại Cổng & Xử lý vắng mặt
* **Mô tả:**
  - Tổng thời gian shipper dừng đỗ phát hàng tại cổng là **15 phút** kể từ thời điểm gửi thông báo.
  - Đồng hồ đếm ngược hiển thị trực tiếp trên màn hình `S6`.
* **Xử lý vi phạm:**
  - Nếu quá 15 phút sinh viên không ra nhận đồ và shipper đã gọi điện ít nhất 3 cuộc không nghe máy:
    - Trạng thái đơn đổi thành `Học sinh vắng mặt / Hủy do quá hạn`.
    - Đối với đơn đã trả qua VietQR: **Không được hoàn lại tiền** nhằm bảo vệ chi phí của quán và công shipper.
    - Suất ăn bị hủy sẽ được thanh lý theo quy chế nội bộ KTX.

---

#### 📌 BR-11: Đối soát nhận hàng 2 lớp (Mã QR & 4 số cuối SĐT)
* **Mô tả:** Đảm bảo trao đúng món ăn cho đúng người trong thời gian **dưới 20 giây**:
  - **Lớp 1 (Ưu tiên):** Sinh viên mở màn hình `S7`, đưa mã QR cho camera shipper quét. Khi quét thành công, hệ thống phát âm thanh *"Tít"* và cập nhật trạng thái đơn thành `Giao hàng thành công`.
  - **Lớp 2 (Dự phòng ngoài trời):** Trường hợp màn hình sinh viên bị nứt vỡ hoặc chói lóa ánh nắng khiến camera không quét được QR, sinh viên đọc to **4 số cuối số điện thoại** (được in to 24sp ngay dưới mã QR). Shipper nhập 4 số này vào app tài xế để mở khóa bàn giao đơn.

---

### NHÓM 5: QUY TẮC HẬU MÃI, KHIẾU NẠI & ĐÁNH GIÁ

#### 📌 BR-12: Điều kiện Đính kèm Ảnh thực tế khi Khiếu nại
* **Mô tả:** Ngăn chặn việc khiếu nại ảo hoặc lạm dụng hoàn tiền.
* **Ràng buộc:**
  - Tại màn hình Khiếu nại `S8`, sinh viên **BẮT BUỘC TẢI LÊN ÍT NHẤT 01 ẢNH CHỤP THỰC TẾ** phần ăn gặp sự cố (ảnh chụp rõ hộp bị vỡ, thức ăn tràn, hoặc túi thiếu món kèm hóa đơn).
* **Hành vi UI:**
  - Nếu chưa tải ảnh: Nút "Gửi yêu cầu khiếu nại" ở trạng thái `Disabled` (`C01`), đồng thời hiển thị thông báo lỗi `C09`: *"Vui lòng chụp ảnh món ăn thực tế để được hỗ trợ bồi hoàn."*

---

#### 📌 BR-13: Giới hạn Thời gian gửi Khiếu nại sau nhận hàng
* **Mô tả:**
  - Yêu cầu khiếu nại chỉ được chấp nhận trong vòng **60 phút** kể từ thời điểm shipper quét giao hàng thành công.
  - Quá 60 phút, nút "Khiếu nại & Yêu cầu hoàn tiền" tại màn hình `S6` và `S10` sẽ tự động biến mất/bị khóa.

---

#### 📌 BR-14: Thời hạn Xử lý Bồi hoàn Tài chính của Quán
* **Mô tả:**
  - Sau khi sinh viên gửi khiếu nại thành công, Chủ quán và Ban quản trị hệ thống có trách nhiệm thẩm định và hoàn trả tiền về Số tài khoản ngân hàng của sinh viên trong vòng tối đa **24 giờ**.
  - Nếu lỗi thuộc về quán (thiếu món, làm sai), quán hoàn tiền 100% giá trị món thiếu.
  - Nếu lỗi do shipper làm rơi vỡ dọc đường, bảo hiểm chuyến gom của hệ thống sẽ chi trả tiền hoàn cho sinh viên.

---

#### 📌 BR-15: Đánh giá độc lập 2 chiều cho Quán & Shipper
* **Mô tả:**
  - Màn hình Đánh giá `S9` phân tách minh bạch thành 2 phần chấm điểm sao (1 đến 5 sao) và nhận xét riêng biệt:
    1. `Chất lượng Món ăn & Quán:` Đánh giá hương vị, độ nóng sốt, quy cách đóng gói và độ sạch sẽ.
    2. `Dịch vụ Shipper:` Đánh giá thái độ giao nhận, đúng giờ và độ cẩn thận khi vận chuyển.
  - Điểm số của Quán không làm ảnh hưởng đến điểm uy tín của Shipper và ngược lại.

---

#### 📌 BR-16: Giới hạn Số lượng đơn tối đa mỗi mẻ gom (Batch Cap)
* **Mô tả:** Bảo đảm chất lượng nấu nướng của quán và sức chứa thùng giữ nhiệt của shipper.
* **Logic xử lý:**
  - Mỗi quán ăn đối tác được thiết lập một ngưỡng nhận đơn tối đa cho mỗi ca gom (mặc định là **30 suất ăn / ca**).
  - Khi số lượng đơn đã đặt cho ca trưa đạt ngưỡng 30, toàn bộ thực đơn của quán đó trên app sẽ hiển thị huy hiệu *"Đã đủ số lượng ca trưa"*, và mọi lượt đặt thêm sẽ tự động chuyển sang ca tối.

---

## 4. MA TRẬN PHÂN QUYỀN TRUY CẬP (ROLE-BASED PERMISSION MATRIX)

| Nghiệp vụ hệ thống | Sinh viên (Student) | Shipper KTX | Chủ Quán (Merchant) | Quản trị viên (Admin) |
| :--- | :---: | :---: | :---: | :---: |
| Tìm kiếm món & Đặt hàng gom ca | **Toàn quyền** | Không | Không | Xem & Giám sát |
| Hủy đơn trước giờ Cut-off | **Cho phép** | Không | Không | Can thiệp cưỡng chế |
| Xác nhận "Bắt đầu nấu" | Không | Không | **Toàn quyền** | Xem |
| Bấm "Đã đến cổng KTX" | Không | **Toàn quyền** | Không | Giám sát GPS |
| Quét mã QR nhận hàng | Xuất trình mã | **Quét camera** | Không | Xem log đối soát |
| Gửi khiếu nại & ảnh bằng chứng | **Toàn quyền** | Xem báo cáo | Nhận thông báo | Xem & Duyệt hoàn tiền |
| Chấm điểm & Viết review | **Toàn quyền** | Xem điểm | Phản hồi bình luận | Quản duyệt từ ngữ |

---
*Tài liệu Đặc tả Quy tắc Nghiệp vụ KTXFood được phê duyệt làm tiêu chuẩn vận hành và ràng buộc kỹ thuật cho toàn bộ dự án PRM323 Lab 2.*
