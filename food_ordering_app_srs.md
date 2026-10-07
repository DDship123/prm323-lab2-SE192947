# Food Ordering App - Tài liệu Đặc tả Yêu cầu & Thiết kế Giao diện

---

## 1. Mô tả ngắn gọn

- Là ứng dụng kết nối giữa những người bán đồ ăn và học sinh/sinh viên trong các ký túc xá (KTX) thuộc Khu đô thị Đại học Quốc gia Thành phố Hồ Chí Minh (ĐHQG-HCM).
- Học sinh trong các khu ký túc xá sẽ đặt đồ ăn của các cửa hàng đăng ký trên ứng dụng. Đơn vị giao đồ ăn sẽ giao định kỳ theo ca tại các địa điểm cố định, thường là trước cổng của các ký túc xá.

---

## 2. Các vai trò trong ứng dụng (User Stories)

### 2.1. Học sinh (Student)
*Người sử dụng ứng dụng để tìm kiếm và đặt đồ ăn.*

#### Nhóm Khám phá & Chọn món ăn
- **As a** học sinh, **I want to** duyệt danh sách và chọn quán ăn theo từng khu vực hoặc danh mục món, **Because** tôi muốn dễ dàng tìm được món ăn mình yêu thích trong khuôn viên KTX và ĐHQG.
- **As a** học sinh, **I want to** thêm những quán ăn yêu thích vào danh sách riêng và nhận thông báo từ quán, **Because** tôi muốn nhanh chóng tìm lại các quán quen và cập nhật kịp thời các món mới hay ưu đãi.
- **As a** học sinh, **I want to** theo dõi đồng hồ đếm ngược thời gian chốt đơn (*cut-off time*) của từng ca giao, **Because** tôi cần biết chính xác hạn chót để kịp đặt đồ ăn trước khi bếp đóng đợt gom.

#### Nhóm Tùy biến món
- **As a** học sinh, **I want to** thêm các ghi chú chi tiết cho món ăn sau khi chốt món (ví dụ: ít cay, không hành, ít đường), **Because** tôi muốn quán ăn chế biến đúng theo khẩu vị và yêu cầu cá nhân.

#### Nhóm Địa điểm, Khung giờ & Thanh toán
- **As a** học sinh, **I want to** chọn địa điểm nhận hàng cố định (ví dụ: cổng KTX Khu A, cổng KTX Khu B) và khung giờ nhận mong muốn, **Because** tôi muốn người giao hàng mang đồ ăn đến đúng nơi và đúng vào giờ tôi rảnh hoặc vừa tan học.
- **As a** học sinh, **I want to** áp dụng mã giảm giá của quán ăn hoặc mã khuyến mãi của ứng dụng vào đơn hàng, **Because** tôi muốn tối ưu chi phí bữa ăn phù hợp với túi tiền sinh viên.
- **As a** học sinh, **I want to** lựa chọn thanh toán bằng hình thức chuyển khoản trước cho quán hoặc trả tiền mặt cho người giao hàng, **Because** tôi muốn linh hoạt phương thức chi trả tùy thuộc vào số dư tài khoản ngân hàng hoặc tiền mặt hiện có.

#### Nhóm Theo dõi & Nhận hàng tại Cổng KTX
- **As a** học sinh, **I want to** theo dõi trạng thái tiến trình đơn hàng theo thời gian thực (đang nấu, tài xế đã lấy món, tài xế đang di chuyển), **Because** tôi chủ động nắm được tiến độ và chuẩn bị xuống cổng ký túc xá kịp giờ.
- **As a** học sinh, **I want to** nhận thông báo tự động kèm thông tin nhận diện tài xế khi người giao hàng đã tới cổng KTX, **Because** tôi có thể nhanh chóng di chuyển ra cổng và tìm đúng tài xế mà không mất công đợi lâu.
- **As a** học sinh, **I want to** hiển thị mã nhận hàng (mã QR hoặc 4 số cuối số điện thoại) để người giao hàng quét/đối chiếu, **Because** tôi muốn đảm bảo nhận đúng đơn của mình và tránh bị người khác lấy nhầm trong lúc cổng KTX đông đúc.

#### Nhóm Đánh giá, Khiếu nại & Hậu mãi
- **As a** học sinh, **I want to** chấm điểm và viết đánh giá chi tiết cho quán ăn, **Because** tôi muốn giúp chủ quán biết được những điểm làm tốt cùng các điểm cần cải thiện, đồng thời làm nguồn tham khảo cho các bạn sinh viên khác.
- **As a** học sinh, **I want to** chấm điểm và nhận xét riêng cho người giao hàng, **Because** tôi muốn đánh giá thái độ phục vụ, mức độ đúng giờ và bảo quản món ăn của tài xế.
- **As a** học sinh, **I want to** hủy đơn hàng trước khi quán bắt đầu chế biến, **Because** tôi muốn chủ động xử lý khi có việc đột xuất mà không gây lãng phí đồ ăn của quán.
- **As a** học sinh, **I want to** gửi khiếu nại (báo thiếu món, đổ vỡ, sai đơn) và yêu cầu hoàn tiền nếu có sự cố, **Because** tôi cần được bảo vệ quyền lợi khi đơn hàng không đạt chất lượng cam kết.

---

### 2.2. Người giao hàng (Shipper)
*Người tiếp nhận và vận chuyển đơn hàng tập trung từ các quán đến cổng ký túc xá.*

#### Nhóm Quản lý Ca làm việc & Nhận chuyến gom
- **As a** người giao hàng, **I want to** đăng ký và chọn các khung giờ giao hàng cố định (ví dụ: ca trưa 11h30 – 12h30, ca tối 18h00 – 19h00), **Because** tôi muốn chủ động sắp xếp lịch trình cá nhân phù hợp với giờ tan học của sinh viên KTX.
- **As a** người giao hàng, **I want to** xem danh sách tổng hợp của chuyến gom đơn (bao gồm tổng số đơn, danh sách các quán cần lấy và cổng KTX đích đến), **Because** tôi cần nắm được quy mô đơn hàng để chuẩn bị thùng giữ nhiệt và không gian chở đồ ăn hợp lý.
- **As a** người giao hàng, **I want to** được hệ thống gợi ý thứ tự di chuyển lấy đồ ăn giữa các quán quanh khu ĐHQG, **Because** tôi muốn tiết kiệm thời gian gom hàng và tránh đi vòng vèo làm đồ ăn bị nguội.

#### Nhóm Lấy hàng & Đối soát tại quán ăn
- **As a** người giao hàng, **I want to** quét mã QR hoặc bấm xác nhận nhận đơn tại từng quán ăn, **Because** tôi cần ghi nhận trách nhiệm chuyển giao món ăn từ quán sang tài xế trên hệ thống.
- **As a** người giao hàng, **I want to** xem danh sách chi tiết các món/topping của từng đơn ngay trên ứng dụng khi lấy hàng, **Because** tôi cần đối chiếu nhanh với quán trước khi rời đi để tránh việc mang thiếu món đến KTX.
- **As a** người giao hàng, **I want to** báo cáo sự cố ngay tại quán (quán làm trễ, thiếu món hoặc đóng cửa), **Because** hệ thống và học sinh có thể cập nhật thông tin kịp thời mà không đổ lỗi làm trễ đơn cho tài xế.

#### Nhóm Giao nhận tại Cổng Ký túc xá
- **As a** người giao hàng, **I want to** bấm nút "Đã đến cổng KTX" để kích hoạt thông báo tự động đồng loạt gửi đến toàn bộ học sinh trong chuyến, **Because** tôi không muốn mất thời gian gọi điện thủ công cho 15–20 người cùng một lúc.
- **As a** người giao hàng, **I want to** quét mã QR nhận hàng hoặc đối chiếu 4 số cuối số điện thoại của học sinh khi phát đồ, **Because** tôi cần đảm bảo trao đúng món cho đúng người và tránh tình trạng lấy nhầm đơn khi đông người.
- **As a** người giao hàng, **I want to** có bộ đếm thời gian chờ kèm chức năng gọi trực tiếp cho học sinh chưa ra nhận, **Because** tôi cần hoàn tất ca giao đúng giờ và có căn cứ chuyển trạng thái "Giao không thành công" nếu quá hạn quy định.

#### Nhóm Thu tiền & Đối soát tài chính
- **As a** người giao hàng, **I want to** phân biệt rõ ràng đơn nào cần thu tiền mặt (COD) và đơn nào đã thanh toán online, **Because** tôi tránh được việc thu thừa hoặc bỏ sót tiền của khách hàng.
- **As a** người giao hàng, **I want to** hiển thị mã QR nhận tiền chuyển khoản ngay trên màn hình khi giao hàng, **Because** sinh viên không có tiền lẻ có thể thanh toán trực tiếp một cách nhanh chóng.
- **As a** người giao hàng, **I want to** xem bảng tổng kết tài chính sau mỗi chuyến gom (tổng tiền mặt đã thu, số tiền phải nộp lại cho quán hoặc hệ thống, tiền công được nhận), **Because** tôi muốn minh bạch dòng tiền và đối soát chuẩn xác với các quán ăn sau ca làm.

#### Nhóm Ví & Hiệu suất cá nhân
- **As a** người giao hàng, **I want to** theo dõi số dư thu nhập theo từng chuyến và theo tuần, **Because** tôi nắm rõ hiệu suất lao động và mức thu nhập thực tế của mình.
- **As a** người giao hàng, **I want to** gửi yêu cầu rút tiền công từ ví ứng dụng về tài khoản ngân hàng cá nhân, **Because** tôi muốn nhận tiền thù lao làm việc linh hoạt và thuận tiện.

---

### 2.3. Chủ quán ăn (Merchant)
*Chủ các gian hàng đăng ký kinh doanh món ăn trên hệ thống.*

#### Nhóm Quản lý Thực đơn & Trạng thái Món ăn
- **As a** chủ quán ăn, **I want to** thêm mới, chỉnh sửa, ẩn hoặc xóa các món ăn kèm giá cả, hình ảnh và danh mục, **Because** tôi muốn thực đơn trên ứng dụng luôn đồng bộ với các món thực tế đang phục vụ tại quán.
- **As a** chủ quán ăn, **I want to** thiết lập các tùy chọn đính kèm (size, mức cay, topping, ghi chú đặc biệt), **Because** tôi muốn khách hàng cá nhân hóa món ăn theo sở thích và quán chế biến chuẩn xác.
- **As a** chủ quán ăn, **I want to** bật công tắc chuyển trạng thái món sang "Tạm hết hàng" chỉ bằng một chạm, **Because** tôi muốn tránh tình trạng sinh viên tiếp tục đặt các món đã hết nguyên liệu trong ngày.

#### Nhóm Vận hành Đơn hàng & Gom đơn theo Ca
- **As a** chủ quán ăn, **I want to** nhận đơn và xem danh sách các đơn hàng được nhóm theo từng ca giao (ví dụ: ca trưa 11h30, ca tối 18h00), **Because** tôi muốn gom nguyên liệu và tối ưu quy trình nấu nướng hàng loạt trước giờ chốt đơn.
- **As a** chủ quán ăn, **I want to** xác nhận "Bắt đầu nấu" và "Món ăn đã sẵn sàng để lấy" theo từng đơn hoặc theo cả đợt gom, **Because** tôi muốn thông báo cho người giao hàng đến lấy đúng lúc, tránh việc tài xế phải đứng chờ đợi lâu hoặc đồ ăn bị nguội.
- **As a** chủ quán ăn, **I want to** quét mã QR nhận hàng của tài xế khi bàn giao các phần ăn, **Because** tôi cần đối soát chính xác số lượng món đã giao cho đúng người vận chuyển, tránh thất thoát hay nhầm lẫn đơn giữa các tài xế.

#### Nhóm Thiết lập Cửa hàng & Thông báo
- **As a** chủ quán ăn, **I want to** bật/tắt trạng thái hoạt động của quán hoặc chuyển sang chế độ "Tạm nghỉ / Quá tải", **Because** tôi muốn chủ động ngưng nhận đơn mới khi quán quá đông khách trực tiếp hoặc đột xuất có việc bận.
- **As a** chủ quán ăn, **I want to** đăng các bảng tin thông báo ngắn trên gian hàng (ví dụ: "Nghỉ lễ", "Hôm nay có món mới"), **Because** tôi muốn cập nhật nhanh các thông tin quan trọng đến tệp khách hàng quen thuộc ở KTX.
- **As a** chủ quán ăn, **I want to** cập nhật thông tin tài khoản ngân hàng và mã QR thanh toán của quán, **Because** tôi muốn sinh viên có thể chuyển khoản trực tiếp tiền món ăn về tài khoản của quán một cách chính xác.

#### Nhóm Khuyến mãi & Thu hút Khách hàng (Promotions & Marketing)
- **As a** chủ quán ăn, **I want to** tạo các mã giảm giá, voucher theo số tiền hoặc phần trăm với điều kiện áp dụng cụ thể, **Because** tôi muốn kích thích sức mua của sinh viên vào các ngày vắng khách hoặc khung giờ thấp điểm.

#### Nhóm Báo cáo Doanh thu & Đối soát Tài chính
- **As a** chủ quán ăn, **I want to** xem báo cáo tổng kết doanh thu và số lượng đơn hàng theo ngày, tuần, tháng, **Because** tôi muốn nắm rõ tình hình kinh doanh và đánh giá các món bán chạy nhất để chuẩn bị nguyên liệu hiệu quả.
- **As a** chủ quán ăn, **I want to** theo dõi bảng kê đối soát tiền mặt (COD do tài xế thu hộ) và tiền đã nhận qua chuyển khoản, **Because** tôi cần chốt số dư minh bạch và đối chiếu chuẩn xác với đội ngũ giao hàng sau mỗi ca làm việc.

#### Nhóm Phản hồi & Xử lý Khiếu nại
- **As a** chủ quán ăn, **I want to** xem và phản hồi công khai các đánh giá, chấm điểm từ sinh viên KTX, **Because** tôi muốn ghi nhận ý kiến để cải thiện chất lượng món ăn và duy trì uy tín cho gian hàng.
- **As a** chủ quán ăn, **I want to** nhận cảnh báo và xử lý các yêu cầu khiếu nại (như thiếu món, sai yêu cầu ghi chú), **Because** tôi muốn phối hợp hoàn tiền hoặc đền bù hợp lý nhằm giữ chân khách hàng.

---

## 3. Danh sách Chi tiết 32 Màn hình Ứng dụng Mobile

### Phân bổ tổng quan
| Phân loại | Số lượng màn hình |
| :--- | :---: |
| **Màn hình Chung (Cả 3 vai trò sử dụng)** | 6 |
| **Màn hình Riêng cho Học sinh** | 11 |
| **Màn hình Riêng cho Người giao hàng** | 7 |
| **Màn hình Riêng cho Chủ quán ăn** | 8 |
| **Tổng cộng** | **32** |

---

### I. Màn hình Chung (6 màn hình)

#### 1. Màn hình Chào & Đăng nhập (Splash & Login Screen)
- **Mô tả:** Giao diện khởi động đầu tiên, hiển thị logo ứng dụng và form đăng nhập nhanh bằng Số điện thoại/Mật khẩu hoặc mã OTP.
- **Chức năng:** Đăng nhập hệ thống, ghi nhớ phiên đăng nhập, điều hướng tự động theo vai trò (Role-based Navigation) sau khi xác thực thành công.
- **Vai trò dùng được:** Học sinh, Người giao hàng, Chủ quán ăn.
- **Màn hình truy cập trước:** Mở ứng dụng từ màn hình chính điện thoại.
- **Màn hình truy cập sau:** Màn hình Đăng ký tài khoản, Màn hình Quên mật khẩu, Màn hình Trang chủ tương ứng theo vai trò.

#### 2. Màn hình Đăng ký tài khoản (Register Screen)
- **Mô tả:** Biểu mẫu thu thập thông tin để tạo tài khoản mới và chọn phân quyền tham gia ứng dụng.
- **Chức năng:** Nhập Họ tên, Số điện thoại, Mật khẩu, chọn vai trò (Học sinh / Người giao hàng / Chủ quán), gửi yêu cầu mã xác thực OTP.
- **Vai trò dùng được:** Người dùng mới (Học sinh, Người giao hàng, Chủ quán ăn).
- **Màn hình truy cập trước:** Màn hình Chào & Đăng nhập.
- **Màn hình truy cập sau:** Màn hình Xác thực OTP.

#### 3. Màn hình Xác thực OTP (OTP Verification Screen)
- **Mô tả:** Giao diện nhập mã OTP gồm 6 chữ số được gửi qua SMS/Zalo để định danh số điện thoại.
- **Chức năng:** Nhập mã OTP, đếm ngược thời gian gửi lại mã, kích hoạt tài khoản hợp lệ.
- **Vai trò dùng được:** Học sinh, Người giao hàng, Chủ quán ăn.
- **Màn hình truy cập trước:** Màn hình Đăng ký tài khoản, Màn hình Quên mật khẩu.
- **Màn hình truy cập sau:** Màn hình Trang chủ của vai trò tương ứng (nếu đăng ký mới), Màn hình Đặt lại mật khẩu mới (nếu quên mật khẩu).

#### 4. Màn hình Quên / Đặt lại mật khẩu (Forgot / Reset Password Screen)
- **Mô tả:** Giao diện hỗ trợ khôi phục quyền truy cập khi người dùng không nhớ mật khẩu cũ.
- **Chức năng:** Nhập số điện thoại để nhận mã OTP khôi phục, thiết lập mật khẩu mới sau khi xác thực thành công.
- **Vai trò dùng được:** Học sinh, Người giao hàng, Chủ quán ăn.
- **Màn hình truy cập trước:** Màn hình Chào & Đăng nhập.
- **Màn hình truy cập sau:** Màn hình Xác thực OTP, Màn hình Chào & Đăng nhập.

#### 5. Màn hình Hồ sơ & Cài đặt cá nhân (Profile & Settings Screen)
- **Mô tả:** Khu vực quản lý thông tin định danh, tùy chỉnh ứng dụng và bảo mật tài khoản.
- **Chức năng:** Cập nhật ảnh đại diện, đổi mật khẩu, xem chính sách và điều khoản sử dụng KTX, Đăng xuất khỏi tài khoản.
- **Vai trò dùng được:** Học sinh, Người giao hàng, Chủ quán ăn.
- **Màn hình truy cập trước:** Thanh điều hướng (Bottom Bar / Header) của Trang chủ mỗi vai trò.
- **Màn hình truy cập sau:** Màn hình Chào & Đăng nhập (khi đăng xuất).

#### 6. Màn hình Trung tâm Thông báo (Notification Center Screen)
- **Mô tả:** Danh sách các thông báo đẩy của hệ thống theo thời gian thực.
- **Chức năng:** Phân loại thông báo (trạng thái đơn hàng, tin tức từ quán, biến động số dư ví), đánh dấu đã đọc, bấm trực tiếp để chuyển tới chi tiết đơn hàng hoặc bảng tin liên quan.
- **Vai trò dùng được:** Học sinh, Người giao hàng, Chủ quán ăn.
- **Màn hình truy cập trước:** Biểu tượng Chuông thông báo trên Header của tất cả màn hình chính.
- **Màn hình truy cập sau:** Màn hình Theo dõi đơn hàng thời gian thực, Màn hình Bảng giao nhận tại cổng KTX, Màn hình Ví thu nhập, Màn hình Vận hành đơn theo ca.

---

### II. Màn hình Riêng cho Học sinh (11 màn hình)

#### 7. Màn hình Trang chủ Học sinh (Student Home Screen)
- **Mô tả:** Giao diện khám phá món ăn, hiển thị danh mục món, quán ăn nổi bật quanh KTX và đồng hồ đếm ngược giờ chốt đơn của ca giao tiếp theo.
- **Chức năng:** Lọc quán theo khu vực (KTX Khu A, KTX Khu B, Làng ĐH), tìm kiếm món, xem đồng hồ đếm ngược hạn chót đặt món (Cut-off Time), truy cập giỏ hàng.
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Màn hình Chào & Đăng nhập.
- **Màn hình truy cập sau:** Màn hình Chi tiết quán ăn, Màn hình Danh sách quán yêu thích, Màn hình Lịch sử đơn hàng, Màn hình Hồ sơ cá nhân.

#### 8. Màn hình Danh sách Quán yêu thích (Favorite Stores Screen)
- **Mô tả:** Nơi lưu trữ toàn bộ các quán ăn mà học sinh đã đánh dấu yêu thích để tiện theo dõi.
- **Chức năng:** Xem danh sách quán quen, kiểm tra trạng thái quán đang mở hay nghỉ, xem thông báo mới nhất từ quán, bỏ lưu yêu thích.
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Màn hình Trang chủ Học sinh, Màn hình Hồ sơ cá nhân.
- **Màn hình truy cập sau:** Màn hình Chi tiết quán ăn.

#### 9. Màn hình Chi tiết Quán ăn & Thực đơn (Store Detail & Menu Screen)
- **Mô tả:** Trang hiển thị toàn bộ menu món, bảng tin thông báo và đánh giá của sinh viên về quán.
- **Chức năng:** Xem bảng tin thông báo từ chủ quán, duyệt danh mục món ăn, bấm chọn món để mở tùy biến, xem điểm đánh giá trung bình của quán, thả tim lưu quán.
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Màn hình Trang chủ Học sinh, Màn hình Danh sách quán yêu thích.
- **Màn hình truy cập sau:** Màn hình Tùy biến món ăn, Màn hình Giỏ hàng & Thanh toán.

#### 10. Màn hình Tùy biến Món ăn (Food Customization Screen / Modal)
- **Mô tả:** Giao diện chi tiết của từng món ăn để học sinh cấu hình theo sở thích cá nhân.
- **Chức năng:** Chọn kích cỡ (Size), chọn mức cay/ngọt, tích chọn topping thêm, nhập ô ghi chú tự do (ví dụ: ít cay, không hành, xin thêm tương ớt), bấm thêm vào giỏ hàng.
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Màn hình Chi tiết Quán ăn & Thực đơn.
- **Màn hình truy cập sau:** Màn hình Chi tiết Quán ăn & Thực đơn (đóng lại sau khi thêm thành công).

#### 11. Màn hình Giỏ hàng & Thanh toán (Cart & Checkout Screen)
- **Mô tả:** Màn hình chốt đơn hàng, chọn địa điểm tập trung, khung giờ giao và hình thức trả tiền.
- **Chức năng:**
  - Chọn địa điểm nhận cố định (Cổng KTX Khu A, Cổng KTX Khu B,...).
  - Chọn ca nhận hàng mong muốn (Ca trưa hoặc Ca tối).
  - Nhập/chọn mã giảm giá từ quán hoặc voucher nền tảng.
  - Lựa chọn phương thức thanh toán: Chuyển khoản trước cho quán hoặc Trả tiền mặt cho người giao hàng.
  - Bấm "Đặt đơn".
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Màn hình Chi tiết Quán ăn & Thực đơn.
- **Màn hình truy cập sau:** Màn hình Thanh toán Chuyển khoản VietQR (nếu chọn CK), Màn hình Theo dõi Đơn hàng thời gian thực.

#### 12. Màn hình Thanh toán Chuyển khoản VietQR (Bank Transfer Payment Screen)
- **Mô tả:** Giao diện cung cấp thông tin tài khoản ngân hàng và mã QR của quán để học sinh quét chuyển tiền trực tiếp.
- **Chức năng:** Tạo mã VietQR động chứa chính xác số tiền và cú pháp mã đơn hàng, sao chép số tài khoản/ngân hàng thụ hưởng, bấm "Đã hoàn tất chuyển khoản".
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Màn hình Giỏ hàng & Thanh toán.
- **Màn hình truy cập sau:** Màn hình Theo dõi Đơn hàng thời gian thực.

#### 13. Màn hình Theo dõi Đơn hàng thời gian thực (Live Order Tracking Screen)
- **Mô tả:** Màn hình trạng thái trực tiếp của đơn hàng từ lúc đặt đến khi nhận món.
- **Chức năng:**
  - Hiển thị tiến trình thời gian thực: `Đang nấu` $\rightarrow$ `Tài xế đã lấy món` $\rightarrow$ `Tài xế đang di chuyển` $\rightarrow$ `Đã tới cổng KTX`.
  - Hiển thị thẻ nhận diện tài xế (Ảnh, Tên, Biển số xe, vị trí đứng đón trước cổng).
  - Nút "Hủy đơn" (chỉ bấm được khi quán chưa bấm nấu).
  - Nút mở "Mã nhận hàng".
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Màn hình Giỏ hàng & Thanh toán, Màn hình Lịch sử đơn hàng, Màn hình Trung tâm Thông báo.
- **Màn hình truy cập sau:** Màn hình Mã QR Nhận hàng, Màn hình Đánh giá & Phản hồi, Màn hình Khiếu nại & Yêu cầu hoàn tiền.

#### 14. Màn hình Mã QR Nhận hàng (Pickup Verification Screen)
- **Mô tả:** Thẻ điện tử hiển thị mã xác thực nhận hàng để đưa cho shipper kiểm tra khi ra cổng KTX.
- **Chức năng:** Hiển thị mã QR đơn hàng, 4 số cuối số điện thoại của học sinh, tóm tắt các món trong túi để đối soát tránh nhận nhầm đồ ăn.
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Màn hình Theo dõi Đơn hàng thời gian thực.
- **Màn hình truy cập sau:** Trở lại Màn hình Theo dõi Đơn hàng thời gian thực.

#### 15. Màn hình Lịch sử Đơn hàng (Order History Screen)
- **Mô tả:** Danh sách các đơn hàng Đang phục vụ, Đã hoàn tất và Đã hủy của tài khoản học sinh.
- **Chức năng:** Tra cứu lại chi tiết các bữa ăn trước đó, trạng thái giao nhận, nút bấm "Đặt lại đơn này".
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Thanh điều hướng chính (Bottom Bar).
- **Màn hình truy cập sau:** Màn hình Theo dõi Đơn hàng thời gian thực, Màn hình Đánh giá & Phản hồi.

#### 16. Màn hình Đánh giá & Phản hồi (Rating & Review Screen)
- **Mô tả:** Biểu mẫu đánh giá chất lượng dịch vụ sau khi bữa ăn hoàn tất.
- **Chức năng:**
  - Chấm điểm 1–5 sao và viết nhận xét cho Quán ăn (hương vị, độ nóng, quy cách đóng gói).
  - Chấm điểm 1–5 sao và nhận xét riêng cho Người giao hàng (thái độ, đúng giờ, bảo quản món không nghiêng đổ).
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Màn hình Theo dõi Đơn hàng thời gian thực, Màn hình Lịch sử Đơn hàng.
- **Màn hình truy cập sau:** Màn hình Trang chủ Học sinh, Màn hình Lịch sử Đơn hàng.

#### 17. Màn hình Khiếu nại & Yêu cầu hoàn tiền (Dispute & Refund Screen)
- **Mô tả:** Giao diện hỗ trợ xử lý sự cố chất lượng hoặc lỗi giao nhận món ăn.
- **Chức năng:** Chọn lý do gặp phải (thiếu món, đổ vỡ thức ăn, sai ghi chú, tài xế không đến), đính kèm ảnh chụp bằng chứng, nhập số tài khoản ngân hàng để yêu cầu hoàn tiền.
- **Vai trò dùng được:** Học sinh.
- **Màn hình truy cập trước:** Màn hình Theo dõi Đơn hàng thời gian thực, Màn hình Lịch sử Đơn hàng.
- **Màn hình truy cập sau:** Màn hình Theo dõi Đơn hàng thời gian thực (ở trạng thái đang chờ xử lý khiếu nại).

---

### III. Màn hình Riêng cho Người giao hàng (7 màn hình)

#### 18. Màn hình Đăng ký Ca làm việc & Nhận chuyến gom (Shift & Batch Dispatch Screen)
- **Mô tả:** Bảng phân bổ công việc chính của tài xế, quản lý ca trực và các chuyến gom (Batch).
- **Chức năng:** Đăng ký các khung giờ cố định (ca trưa 11h30 – 12h30, ca tối 18h00 – 19h00), xem tổng quan chuyến gom (tổng số đơn, các quán cần lấy, cổng KTX đích đến), bấm "Bắt đầu chuyến gom".
- **Vai trò dùng được:** Người giao hàng.
- **Màn hình truy cập trước:** Màn hình Chào & Đăng nhập.
- **Màn hình truy cập sau:** Màn hình Lộ trình gom hàng tại quán, Màn hình Ví thu nhập & Rút tiền.

#### 19. Màn hình Lộ trình gom hàng tại quán (Pickup Route Screen)
- **Mô tả:** Bản đồ và danh sách thứ tự các quán ăn cần ghé lấy hàng đã được tối ưu hóa đường đi quanh KTX và khu ĐHQG.
- **Chức năng:** Hiển thị thứ tự di chuyển tối ưu giữa các quán ăn, hiển thị số lượng đơn cần lấy tại từng điểm, mở ứng dụng chỉ đường.
- **Vai trò dùng được:** Người giao hàng.
- **Màn hình truy cập trước:** Màn hình Đăng ký Ca làm việc & Nhận chuyến gom.
- **Màn hình truy cập sau:** Màn hình Chi tiết Lấy hàng tại Quán.

#### 20. Màn hình Chi tiết Lấy hàng tại Quán (Merchant Pickup Screen)
- **Mô tả:** Giao diện làm việc tại từng quán ăn để đối soát và tiếp nhận món ăn vào thùng giữ nhiệt.
- **Chức năng:** Xem checklist chi tiết món ăn/topping của từng đơn, quét mã QR hoặc bấm xác nhận nhận đơn tại quán, bấm nút "Báo cáo sự cố tại quán" (quán làm trễ, thiếu món, quán đóng cửa).
- **Vai trò dùng được:** Người giao hàng.
- **Màn hình truy cập trước:** Màn hình Lộ trình gom hàng tại quán.
- **Màn hình truy cập sau:** Màn hình Bảng giao nhận tại Cổng Ký túc xá (sau khi gom xong các quán).

#### 21. Màn hình Bảng giao nhận tại Cổng Ký túc xá (Drop-off Hub Screen)
- **Mô tả:** Màn hình tập trung phát hàng cho sinh viên tại cổng KTX Khu A hoặc Khu B.
- **Chức năng:**
  - Nút "Đã đến cổng KTX" để kích hoạt gửi thông báo tự động đồng loạt cho toàn bộ học sinh trong chuyến.
  - Bộ đếm thời gian chờ tại cổng.
  - Danh sách phân loại sinh viên: `Đã nhận` / `Chưa ra nhận`.
  - Nút gọi trực tiếp cho học sinh chưa ra nhận.
  - Nút mở camera quét mã QR nhận hàng của học sinh hoặc nhập 4 số cuối SĐT để đối chiếu.
- **Vai trò dùng được:** Người giao hàng.
- **Màn hình truy cập trước:** Màn hình Chi tiết Lấy hàng tại Quán.
- **Màn hình truy cập sau:** Màn hình Xác nhận Trao hàng & Thu tiền, Màn hình Tổng kết ca & Đối soát tài chính.

#### 22. Màn hình Xác nhận Trao hàng & Thu tiền (Handover & Payment Screen)
- **Mô tả:** Giao diện thao tác khi học sinh ra nhận đồ ăn, phục vụ thu tiền và chốt đơn.
- **Chức năng:**
  - Phân biệt rõ loại đơn: Đã trả online hay Cần thu tiền mặt (COD).
  - Hiển thị mã QR nhận tiền chuyển khoản ngay trên màn hình để sinh viên quét trả khi không có tiền lẻ.
  - Bấm "Xác nhận giao thành công" hoặc chuyển trạng thái "Giao không thành công" nếu quá hạn thời gian chờ.
- **Vai trò dùng được:** Người giao hàng.
- **Màn hình truy cập trước:** Màn hình Bảng giao nhận tại Cổng Ký túc xá.
- **Màn hình truy cập sau:** Trở lại Màn hình Bảng giao nhận tại Cổng Ký túc xá (để phát tiếp đơn khác).

#### 23. Màn hình Tổng kết ca & Đối soát Tài chính (Trip Settlement Screen)
- **Mô tả:** Bảng đối soát thu chi sau khi kết thúc đợt giao tại cổng KTX.
- **Chức năng:** Tổng kết số đơn giao thành công, tổng tiền mặt COD đã thu hộ, số tiền cần trả nộp lại cho từng quán hoặc hệ thống, tổng thù lao người giao hàng nhận được từ chuyến đi.
- **Vai trò dùng được:** Người giao hàng.
- **Màn hình truy cập trước:** Màn hình Bảng giao nhận tại Cổng Ký túc xá.
- **Màn hình truy cập sau:** Màn hình Đăng ký Ca làm việc & Nhận chuyến gom, Màn hình Ví thu nhập & Rút tiền.

#### 24. Màn hình Ví Thu nhập & Rút tiền (Shipper Earnings & Wallet Screen)
- **Mô tả:** Khu vực quản lý dòng tiền thù lao, theo dõi hạn mức công nợ và rút tiền ngân hàng.
- **Chức năng:** Theo dõi số dư thu nhập theo từng chuyến gom và theo tuần, kiểm tra mức tiền mặt đang giữ, tạo lệnh rút tiền thù lao về tài khoản ngân hàng cá nhân.
- **Vai trò dùng được:** Người giao hàng.
- **Màn hình truy cập trước:** Thanh điều hướng chính (Bottom Bar), Màn hình Tổng kết ca & Đối soát tài chính.
- **Màn hình truy cập sau:** Màn hình Đăng ký Ca làm việc & Nhận chuyến gom.

---

### IV. Màn hình Riêng cho Chủ quán ăn (8 màn hình)

#### 25. Màn hình Bảng điều khiển Quán (Merchant Dashboard Screen)
- **Mô tả:** Trang chủ dành riêng cho người bán, quản lý hoạt động tổng thể của gian hàng.
- **Chức năng:** Bật/tắt trạng thái hoạt động của quán ("Đang mở cửa", "Tạm nghỉ / Quá tải"), xem tóm tắt số đơn trong ca trưa/tối, xem nhanh doanh thu ngày, cảnh báo có đơn mới.
- **Vai trò dùng được:** Chủ quán ăn.
- **Màn hình truy cập trước:** Màn hình Chào & Đăng nhập.
- **Màn hình truy cập sau:** Màn hình Vận hành đơn theo ca, Màn hình Quản lý Thực đơn, Màn hình Thiết lập gian hàng & Bảng tin, Màn hình Quản lý Khuyến mãi, Màn hình Báo cáo Doanh thu, Màn hình Đánh giá & Xử lý khiếu nại.

#### 26. Màn hình Vận hành Đơn theo Ca (Batch Order Kitchen Screen)
- **Mô tả:** Giao diện điều phối bếp nấu, gom nhóm các đơn đặt theo từng khung giờ giao (ví dụ: ca trưa 11h30, ca tối 18h00).
- **Chức năng:**
  - Xem danh sách tổng hợp số lượng món cần chế biến theo ca (ví dụ: 15 Cơm tấm, 8 Bún chả).
  - Xem ghi chú chi tiết theo từng đơn của sinh viên.
  - Bấm nút chuyển trạng thái "Bắt đầu nấu" và "Món ăn đã sẵn sàng để lấy".
  - Mở camera quét mã QR nhận hàng của tài xế khi giao món ra ngoài.
- **Vai trò dùng được:** Chủ quán ăn.
- **Màn hình truy cập trước:** Màn hình Bảng điều khiển Quán.
- **Màn hình truy cập sau:** Trở lại Màn hình Bảng điều khiển Quán.

#### 27. Màn hình Quản lý Thực đơn (Menu Management Screen)
- **Mô tả:** Danh sách các món ăn của quán phân loại theo từng danh mục.
- **Chức năng:** Công tắc bật/tắt nhanh trạng thái "Tạm hết hàng" cho từng món, ẩn/hiện món, nút điều hướng tới tạo mới hoặc chỉnh sửa món ăn.
- **Vai trò dùng được:** Chủ quán ăn.
- **Màn hình truy cập trước:** Màn hình Bảng điều khiển Quán.
- **Màn hình truy cập sau:** Màn hình Thêm / Chỉnh sửa Món ăn.

#### 28. Màn hình Thêm / Chỉnh sửa Món ăn (Food Item Editor Screen)
- **Mô tả:** Biểu mẫu chi tiết để đăng bán hoặc cập nhật món ăn.
- **Chức năng:** Tải ảnh món, đặt Tên món, Giá bán, Danh mục, thiết lập danh sách Tùy chọn đi kèm (Size, mức cay, danh sách topping kèm phụ phí), Lưu hoặc Xóa món ăn.
- **Vai trò dùng được:** Chủ quán ăn.
- **Màn hình truy cập trước:** Màn hình Quản lý Thực đơn.
- **Màn hình truy cập sau:** Màn hình Quản lý Thực đơn (sau khi Lưu hoặc Hủy).

#### 29. Màn hình Thiết lập Gian hàng & Bảng tin (Store Profile & Bulletin Screen)
- **Mô tả:** Cài đặt thông tin nhận diện cửa hàng, tài khoản thanh toán và các thông cáo tới khách hàng.
- **Chức năng:** Cập nhật thông tin tài khoản ngân hàng và mã QR thanh toán của quán, đăng các mẩu tin thông báo ngắn (thông báo nghỉ lễ, đổi giờ phục vụ, thông báo món mới).
- **Vai trò dùng được:** Chủ quán ăn.
- **Màn hình truy cập trước:** Màn hình Bảng điều khiển Quán.
- **Màn hình truy cập sau:** Màn hình Bảng điều khiển Quán.

#### 30. Màn hình Quản lý Khuyến mãi (Voucher / Promotion Screen)
- **Mô tả:** Quản lý danh sách các chương trình khuyến mãi và mã ưu đãi của quán.
- **Chức năng:** Tạo mã giảm giá theo số tiền hoặc phần trăm, thiết lập điều kiện áp dụng (giá trị đơn tối thiểu, thời hạn sử dụng, số lượt dùng), bật/tắt kích hoạt voucher.
- **Vai trò dùng được:** Chủ quán ăn.
- **Màn hình truy cập trước:** Màn hình Bảng điều khiển Quán.
- **Màn hình truy cập sau:** Màn hình Bảng điều khiển Quán.

#### 31. Màn hình Báo cáo Doanh thu & Đối soát COD (Merchant Analytics & Reconciliation Screen)
- **Mô tả:** Trung tâm theo dõi tình hình tài chính, báo cáo bán hàng và đối chiếu tiền hàng.
- **Chức năng:**
  - Biểu đồ doanh thu và số lượng đơn hàng theo ngày, tuần, tháng; danh sách các món bán chạy nhất.
  - Bảng kê đối soát tài chính: Phân tách rõ ràng tiền đã vào tài khoản (học sinh chuyển khoản) và tiền mặt COD mà đội ngũ người giao hàng đã thu hộ cần thanh toán trả cho quán.
- **Vai trò dùng được:** Chủ quán ăn.
- **Màn hình truy cập trước:** Màn hình Bảng điều khiển Quán.
- **Màn hình truy cập sau:** Màn hình Bảng điều khiển Quán.

#### 32. Màn hình Đánh giá & Xử lý Khiếu nại (Merchant Reviews & Dispute Center Screen)
- **Mô tả:** Nơi tiếp nhận và xử lý tương tác phản hồi của sinh viên với quán.
- **Chức năng:** Xem điểm sao, trả lời bình luận đánh giá công khai từ sinh viên; tiếp nhận các yêu cầu khiếu nại (báo thiếu món, đổ vỡ, sai ghi chú) và xác nhận đồng ý hoàn tiền cho khách.
- **Vai trò dùng được:** Chủ quán ăn.
- **Màn hình truy cập trước:** Màn hình Bảng điều khiển Quán, Màn hình Trung tâm Thông báo.
- **Màn hình truy cập sau:** Màn hình Bảng điều khiển Quán.

---

## 4. Các Quy trình Luồng Người dùng Chính (User Flows)

### A. Luồng người dùng cho Học sinh (Student Flow)

```
[Trang chủ Học sinh]
         │ (Xem Cut-off time)
         ▼
[Chi tiết Quán & Thực đơn] ──► [Tùy biến Món (Size/Topping/Ghi chú)]
         │
         ▼
[Giỏ hàng & Thanh toán] (Chọn cổng KTX, ca nhận, mã giảm giá)
         │
         ├────────────────────────────────────────┬────────────────────────────────────────┐
         ▼ (Chọn Tiền mặt)                        ▼ (Chọn Chuyển khoản)                   │
         │                               [Thanh toán Chuyển khoản VietQR]                  │
         │                                        │ (Hoàn tất)                            │
         └────────────────────────────────────────┴────────────────────────────────────────┘
                                                  │
                                                  ▼
                               [Theo dõi Đơn hàng thời gian thực]
                                                  │
                                                  ▼ (Khi tài xế tới cổng)
                                       [Mã QR Nhận hàng]
                                                  │
                                                  ▼ (Nhận hàng thành công)
                         ┌────────────────────────┴────────────────────────┐
                         ▼                                                 ▼
             [Đánh giá & Phản hồi]                            [Khiếu nại & Yêu cầu hoàn tiền]
```

1. **Tìm kiếm & Chọn món:** Màn hình Trang chủ Học sinh $\rightarrow$ Xem đồng hồ đếm ngược chốt đơn (Cut-off Time) $\rightarrow$ Màn hình Chi tiết Quán ăn & Thực đơn $\rightarrow$ Màn hình Tùy biến Món ăn (chọn size, topping, ghi chú).
2. **Đặt hàng & Thanh toán:** Màn hình Giỏ hàng & Thanh toán $\rightarrow$ Chọn cổng KTX nhận hàng cố định & ca nhận $\rightarrow$ Áp dụng mã giảm giá $\rightarrow$ Chọn phương thức thanh toán (Tiền mặt / VietQR) $\rightarrow$ Màn hình Thanh toán VietQR (nếu chọn CK) $\rightarrow$ Xác nhận đặt đơn thành công.
3. **Theo dõi & Nhận hàng:** Màn hình Theo dõi Đơn hàng thời gian thực $\rightarrow$ Nhận thông báo "Tài xế đã đến cổng KTX" $\rightarrow$ Màn hình Mã QR Nhận hàng $\rightarrow$ Đưa tài xế quét/đối chiếu 4 số cuối SĐT $\rightarrow$ Nhận đồ ăn.
4. **Đánh giá & Sau bán hàng:** Màn hình Đánh giá & Phản hồi (chấm sao cho Quán ăn và Tài xế) **hoặc** Màn hình Khiếu nại & Yêu cầu hoàn tiền (nếu thiếu/hỏng món).

---

### B. Luồng người dùng cho Người giao hàng (Shipper Flow)

```
[Đăng ký Ca & Nhận chuyến gom]
         │
         ▼
[Lộ trình gom hàng tại quán] (Gợi ý đường đi tối ưu)
         │
         ▼
[Chi tiết Lấy hàng tại Quán] (Checklist món, quét mã QR nhận hàng, báo sự cố nếu có)
         │
         ▼ (Sau khi gom đủ đơn)
[Bảng giao nhận tại Cổng KTX] ──► Bấm "Đã đến cổng KTX" (Gửi thông báo hàng loạt)
         │
         ▼
[Xác nhận Trao hàng & Thu tiền] (Quét mã/check SĐT, thu COD hoặc show VietQR)
         │
         ▼ (Kết thúc ca phát hàng)
[Tổng kết ca & Đối soát Tài chính] ──► [Ví Thu nhập & Rút tiền]
```

1. **Nhận chuyến gom:** Màn hình Đăng ký Ca làm việc & Nhận chuyến gom $\rightarrow$ Chọn ca trực $\rightarrow$ Xác nhận nhận chuyến gom (Batch).
2. **Gom hàng tại quán:** Màn hình Lộ trình gom hàng tại quán $\rightarrow$ Di chuyển theo gợi ý $\rightarrow$ Màn hình Chi tiết Lấy hàng tại Quán $\rightarrow$ Quét mã QR/đối soát món $\rightarrow$ Báo hoàn tất lấy hàng.
3. **Phát hàng tại cổng KTX:** Di chuyển tới cổng KTX $\rightarrow$ Màn hình Bảng giao nhận tại Cổng KTX $\rightarrow$ Bấm "Đã đến cổng KTX" (gửi thông báo tự động) $\rightarrow$ Màn hình Xác nhận Trao hàng & Thu tiền (quét mã QR nhận hàng của sinh viên / thu tiền mặt COD) $\rightarrow$ Hoàn tất ca giao.
4. **Đối soát & Thu nhập:** Màn hình Tổng kết ca & Đối soát Tài chính $\rightarrow$ Màn hình Ví Thu nhập & Rút tiền (xem thù lao, rút tiền về tài khoản ngân hàng).

---

### C. Luồng người dùng cho Chủ quán ăn (Merchant Flow)

```
[Bảng điều khiển Quán] (Bật trạng thái mở cửa)
         │
         ├────────────────────────────────────────┬────────────────────────────────────────┐
         ▼                                        ▼                                        ▼
[Quản lý Thực đơn & Món ăn]             [Vận hành Đơn theo Ca]                  [Báo cáo Doanh thu & COD]
(Tạo mới, sửa, bật/tắt hết hàng)       (Gom đơn nấu hàng loạt,                  (Xem số liệu, đối soát tiền mặt/CK)
                                        quét mã bàn giao tài xế)                           │
                                                                                           ▼
                                                                                [Đánh giá & Khiếu nại]
                                                                                (Phản hồi review, duyệt hoàn tiền)
```

1. **Quản lý gian hàng & Thực đơn:** Màn hình Bảng điều khiển Quán $\rightarrow$ Bật trạng thái mở cửa $\rightarrow$ Màn hình Quản lý Thực đơn / Thêm & Chỉnh sửa Món ăn $\rightarrow$ Cập nhật món, topping, giá bán.
2. **Xử lý đơn hàng theo đợt:** Màn hình Vận hành Đơn theo Ca $\rightarrow$ Tiếp nhận danh sách tổng hợp đợt gom $\rightarrow$ Bấm "Bắt đầu nấu" $\rightarrow$ Đóng gói $\rightarrow$ Quét mã QR giao hàng cho Người giao hàng khi tới lấy.
3. **Tài chính & Chăm sóc khách hàng:** Màn hình Báo cáo Doanh thu & Đối soát COD $\rightarrow$ Màn hình Đánh giá & Xử lý Khiếu nại (phản hồi bình luận, duyệt hoàn tiền nếu có sự cố).