# UX Personas & Problem Statements (Food Ordering App - KTX ĐHQG-HCM)

---

### `P01 · PRIMARY PERSONA` <span style="float: right; color: #1a73e8; font-weight: bold;">Ưu tiên cao</span>

## Lê Thùy Linh · Sinh viên nội trú KTX ĐHQG-HCM (Khu B, Tòa B3, Phòng 408)
*19 tuổi (minh họa) · SĐT: +84 912 *** 829 (Đuôi SĐT: 4829) · Smartphone (Android / iOS) · 4–6 bữa/tuần (giả định)*

> “Tôi cần đặt đồ ăn giá sinh viên giao đúng giờ tan học, không muốn vừa tan học vừa chen chúc tìm shipper giữa trời nắng cổng KTX.”  
> *Câu nói giả lập để minh họa nhu cầu; không phải phát biểu của người tham gia nghiên cứu.*

| **Goals** | **Pain points** |
| :--- | :--- |
| • Chuẩn bị và bắt đầu bữa ăn đúng giờ sau ca học, không bị gián đoạn hay lỡ bữa.<br>• Tối ưu chi phí ăn uống với mức giá bình dân và phí ship gom hợp lý túi tiền sinh viên.<br>• Nhận đúng đồ ăn nhanh chóng tại cổng KTX mà không bị nhầm lẫn hay thất lạc. | • Phí ship trên các ứng dụng giao đồ ăn thông thường quá cao; quán cơm bình dân quanh KTX không chịu được chiết khấu app.<br>• Giờ tan học cổng KTX cực kỳ đông đúc; shipper gọi điện liên tục, khó tìm nhau và dễ lấy nhầm đơn.<br>• Lịch học kín và không có phương tiện cá nhân (xe máy) để tự chạy đi mua cơm ở xa. |

| **Behaviors & Context** | **Constraints & Motivations** |
| :--- | :--- |
| Thường xuyên dùng smartphone để học tập và giải trí; thành thạo mua sắm trực tuyến và quét mã VietQR ngân hàng. Tranh thủ đặt món tại phòng KTX (Tòa B3) hoặc giữa giờ giải lao; đứng đón nhận hàng ngoài trời tại cổng KTX Khu B (Trụ A1-A2) dưới thời tiết nắng gắt. | Ngân sách sinh viên có hạn, rất nhạy cảm về giá và phí ship; không có xe máy cá nhân. Cần thao tác đặt món siêu tốc trước giờ chốt đơn (*Cut-off Time* 10:45 ca trưa). Ưu tiên tốc độ, sự đúng giờ và độ chính xác khi giao nhận hơn các tính năng trang trí phức tạp. |

---

**Job to Be Done**  
*Khi kết thúc ca học hoặc chuẩn bị đến bữa ăn tại KTX, tôi muốn đặt đồ ăn giá sinh viên từ các quán quen và nhận hàng tập trung theo khung giờ cố định tại cổng KTX, để có bữa ăn đầy đủ, đúng giờ với chi phí tiết kiệm nhất mà không tốn công đi lại.*

**Critical scenario**  
Trong giờ giải lao lúc 10h40 tại giảng đường, Linh mở app tranh thủ chốt nhanh phần cơm trưa trước hạn chốt bếp (*Cut-off Time* 10h45) của ca giao 11h30 – 12:00, sau đó tan học thong thả về KTX Khu B và dùng mã QR (mã đơn #8829B, đuôi SĐT 4829) nhận đúng phần cơm của mình từ shipper Nguyễn Văn Minh tại Cổng KTX Khu B (Trụ A1-A2) trong vòng dưới 20 giây mà không cần chen lấn hay gọi điện thoại tìm nhau giữa trời nắng.

**Success criteria**  
Hoàn thành chuỗi tác vụ “mở app → chọn quán quen → chọn món & ghi chú khẩu vị → thanh toán gom đơn trước Cut-off Time” trong **dưới 30 giây**; và chuỗi “đến cổng KTX → xuất trình mã QR → shipper quét đối soát → nhận đúng đơn hàng” trong **dưới 20 giây** mà không có lỗi nhận nhầm đơn; đo bằng thời gian thao tác, tỷ lệ lỗi và nhận xét khi thử nghiệm người dùng.

**Giả thuyết thiết kế cần thử nghiệm**  
Tổ chức luồng đặt món theo các ca giao cố định kèm đồng hồ đếm ngược *Cut-off Time* nổi bật ngay trang chủ; tích hợp mã QR nhận hàng độc bản kèm 4 số cuối SĐT (4829) và tối ưu giao diện có độ tương phản cao, phông chữ lớn, touch target tối thiểu 48dp cho môi trường ánh sáng mạnh ngoài trời tại cổng KTX. **Đây mới là giải pháp đề xuất, không phải user need đã được xác thực.**

*Evidence status: Proto-Persona · Chưa có bằng chứng thực tế quy mô lớn. Cần phỏng vấn/quan sát sinh viên nội trú KTX ĐHQG (Khu A & Khu B) để xác minh tần suất đặt món, ngân sách bữa ăn, thiết bị sử dụng, trở ngại tại cổng KTX và cách xử lý hiện tại.*

---

## Problem Statement & Measurable Success Metrics

### A. Câu phát biểu vấn đề (Problem Statement)
> "Sinh viên nội trú ký túc xá ĐHQG gặp khó khăn trong việc đặt đồ ăn giá hợp lý từ các quán quen quanh ký túc xá do mức phí dịch vụ của các ứng dụng phổ biến quá cao và tình trạng chen chúc, thất lạc đơn tại cổng ký túc xá vào giờ cao điểm."

### B. Tiêu chí thành công đo lường được (Measurable Success Metrics)
1. **Thời gian đặt đơn:** Sinh viên hoàn tất chọn món và đặt đơn trước Cut-off time trong **dưới 30 giây**.
2. **Thời gian nhận hàng:** Thời gian đối soát và nhận đúng đồ ăn tại cổng ký túc xá từ shipper bằng quét mã QR diễn ra trong **dưới 20 giây**.
3. **Độ chính xác giao nhận:** Tỷ lệ thất lạc hoặc lấy nhầm đơn hàng tại cổng KTX đạt mức **0%**.
