# BÁO CÁO MỤC 4.3: VÒNG LẶP 1 - TINH CHỈNH PHÂN CẤP THỊ GIÁC & NÚT HÀNH ĐỘNG CHÍNH

---

## 1. Nguyên văn Prompt đã nhập cho Stitch (Vòng 1)

```text
Please duplicate the selected screen, place the new refined version right next to the original one (side-by-side), and apply the following refinements on the new copy:

Establish clear visual hierarchy: Increase font size/weight for headers, enhance contrast for key content, and mute auxiliary info with neutral tones.

Emphasize Primary Action: Design a prominent Primary Button (e.g., 'Xác nhận nhận hàng') using the brand accent color, white high-contrast text, rounded corners, and place it conveniently in the bottom thumb zone.

De-emphasize secondary actions: Style secondary buttons as outlined or ghost buttons.

Finally, provide a Markdown summary table of all applied changes in this format: [Element | Before | After | Technical Reason].
```

---

## 2. Lưu trữ hình ảnh đối chiếu Vòng 1

*   **Bản gốc ban đầu:** `assets/stitch/v1_before.png`
*   **Bản hoàn thiện hậu quyết định (Final Resolved):** `assets/stitch/v1_after.png`

---

## 3. Chi tiết tối ưu hóa 10 màn hình (Bản Chốt Chuẩn)

### Màn hình 1: Trang Chủ Đặt Món & Ca Gom KTX
*   **Đúc kết từ:** Cặp màn hình Group 7.
*   **Tối ưu nổi bật:**
    *   **Thanh điều hướng & Giỏ hàng nổi:** Giữ trọn vẹn thanh Bottom Navigation 5 tab tiêu chuẩn (Khám phá, Đặt món, Thanh toán, Lịch sử, Tài khoản) kết hợp thanh giỏ hàng nổi *"Đơn gom KTX Khu B • 1 món • 35.000đ"* với nút *"Xem giỏ hàng"* màu đỏ sậm `#B52603`.
    *   **Banner đếm ngược ca trưa:** Đồng hồ đếm ngược chốt đơn lớn, trực quan (`00:28:45`), nhãn *"CA TRƯA ĐANG MỞ"* có độ tương phản cao, tạo cảm giác khẩn cấp hợp lý.
    *   **Xử lý Text Wrapping:** Tiêu đề quán, khoảng cách (`150m`), tag freeship và khoảng giá (`28.000đ - 45.000đ`) được bọc trong container co giãn tự nhiên (`auto-width`), loại bỏ hiện tượng rớt chữ mồ côi (typographic orphans).

### Màn hình 2: Chi Tiết Quán & Thực Đơn Cơm Tấm
*   **Đúc kết từ:** Cặp màn hình Group 8.
*   **Tối ưu nổi bật:**
    *   **Header quán Cơm Tấm Cô Ba:** Đầy đủ metadata định danh: tích xanh xác thực, khoảng cách `600m`, đánh giá `4.9` sao, banner *"Bảng tin Cô Ba hôm nay"* và đồng hồ đếm ngược chốt đơn `24:59`.
    *   **Phân loại Tab súc tích:** Cấu trúc 3 tab rõ ràng: *Món Bán Chạy 🔥*, *Cơm Tấm*, *Món Thêm / Topping*.
    *   **Thanh ghim đáy (Sticky Bar):** Hiển thị cố định *"Giỏ hàng (2 phần) • 70.000đ"* kèm nút *"Chốt đơn >"* với chiều cao và diện tích bấm đạt chuẩn $\ge 48\text{dp}$.

### Màn hình 3: Tùy Biến Món Ăn (Customization Modal)
*   **Đúc kết từ:** Cặp màn hình Group 9.
*   **Tối ưu nổi bật:**
    *   **Compact Vertical Layout:** Loại bỏ hoàn toàn padding thừa; tổ chức 5 khối tùy chọn mạch lạc: *Kích cỡ / Phần ăn*, *Khẩu vị & Mỡ hành*, *Topping thêm*, *Độ cay & Nước mắm*, *Ghi chú*.
    *   **Cụm CTA ghim đáy:** Kết hợp bộ đếm số lượng `(- 1 +)` cùng nút bấm to bản *"Thêm vào giỏ • 46.000đ"* màu đỏ `#B52603`, chữ trắng in đậm nằm trọn trên 1 dòng duy nhất.

### Màn hình 4: Thanh Toán Gom Đơn & Điểm Nhận KTX
*   **Đúc kết từ:** Cặp màn hình Group 10.
*   **Tối ưu nổi bật:**
    *   **Cấu trúc 6 bước rõ ràng:** *Điểm nhận cố định tại Cổng Khu B* (hiển thị huy hiệu 28 bạn cùng tòa), *Khung giờ ca trưa*, *Tóm tắt món*, *Mã giảm giá SINHVIENKTX*, *Phương thức VietQR*, và *Bảng chi tiết thanh toán*.
    *   **Nút CTA chính Thumb Zone:** Nút *"Đặt đơn nhận tại Cổng KTX Khu B (45.000đ)"* cao `52dp`, tương phản chữ chuẩn WCAG AA (> 4.5:1).

### Màn hình 5: Chuyển Khoản VietQR Khớp Lệnh Tự Động
*   **Đúc kết từ:** Cặp màn hình Group 11.
*   **Tối ưu nổi bật:**
    *   **Khối VietQR Napas247:** Khung QR lớn, viền đệm trắng chuẩn; tích hợp 2 nút tiện ích *"Lưu ảnh QR"* và *"Mở App Bank"* đạt chuẩn $\ge 48\times 48\text{dp}$, cách nhau $\ge 16\text{dp}$.
    *   **Sao chép 1 chạm độc lập:** 3 nút riêng biệt cho *STK*, *Số tiền chính xác 45.000 đ*, và *Nội dung bắt buộc KTX8829B LE THUY LINH*.
    *   **Nút xác nhận đáy:** Nút ghim đáy *"Tôi đã hoàn tất chuyển khoản"* màu đỏ thương hiệu `#B52603` nổi bật.

### Màn hình 6: Theo Dõi Giao Hàng & Tài Xế KTX
*   **Đúc kết từ:** Cặp màn hình Group 8 (Flow theo dõi đơn).
*   **Tối ưu nổi bật:**
    *   **Tiến trình giao hàng 4 bước:** Toàn bộ tiến trình (*Đã chốt & Bếp nấu xong $\rightarrow$ Tài xế đã lấy món $\rightarrow$ Đang tới KTX Khu B $\rightarrow$ Sẵn sàng phát hàng*) và thông tin tài xế Nguyễn Văn Minh (*Honda Wave Đỏ • 59-X1 839.24*) hiển thị thẳng hàng, không gãy dòng.
    *   **Nút CTA chính:** Nút *"Mở Mã Nhận Hàng (QR Code)"* màu đỏ `#B52603`, chữ trắng in đậm cao `50dp` ($\ge 48\text{dp}$), nằm trọn vẹn 1 dòng.
    *   **Duy trì Bottom Navigation:** Bảo toàn thanh 5 tab với chỉ báo chấm active tại tab *Lịch sử*.
    *   **Live Mini-map:** Bản đồ live *"Đang đi: Đường Tạ Quang Bửu - Cách cổng 450m"* kèm nhãn *"Đơn xếp số 04/12 đợt trưa"*.

### Màn hình 7: Mã Nhận Hàng & QR Đối Soát Cổng KTX
*   **Đúc kết từ:** Cặp màn hình Group 9 (Flow nhận hàng).
*   **Tối ưu nổi bật:**
    *   **Khung QR & Quick Action Sáng max:** Khung QR sắc nét, nút *"Sáng max"* chuyển thành Quick Action icon mặt trời ở góc trên bên phải khung QR ($\ge 48\times 48\text{dp}$), kích hoạt 1 chạm dưới trời nắng gắt.
    *   **Mã PIN 4 số đối soát to đậm:** Số `4 8 2 9` đặt trong ô cam nhạt to rõ, hỗ trợ đọc to từ khoảng cách xa.
    *   **Dải dán nhãn chống thu nhầm tiền:** Dải huy hiệu xanh lá đậm *"ĐÃ THANH TOÁN (VIETQR) • KHÔNG THU TIỀN"* in hoa trực diện dưới mã QR.
    *   **Hệ thống nút hành động kép:** Nút phụ Outlined *"Theo dõi đơn"* / *"Khiếu nại"* đặt song song phía trên nút chính *"Xác nhận nhận hàng"* màu đỏ sậm.

### Màn hình 8: Khiếu Nại & Hoàn Tiền Nhanh KTX
*   **Đúc kết từ:** Cặp màn hình Group 10 (Flow báo sự cố).
*   **Tối ưu nổi bật:**
    *   **Compact Vertical Layout:** Gom 5 nhóm sự cố thành các thẻ radio gọn gàng; chọn sẵn món bị ảnh hưởng *"Trà Đào Cam Sả Tươi (500ml) - 10.000đ"* kèm tỷ lệ hoàn 100%.
    *   **Gom cụm bằng chứng:** Khối tải ảnh tem nhiệt (*Tem #8829B_KTX.jpg*) và ô chụp thêm ảnh dàn hàng ngang dạng lưới thumbnail, giảm 30% chiều dài cuộn trang.
    *   **Phương thức hoàn tiền tối ưu:** Đưa tùy chọn hoàn tiền tức thì về *Ví KTX Food / Xu Sinh Viên* (tặng voucher 5.000đ bù đắp) lên vị trí ưu tiên số 1.
    *   **Nút CTA chính ghim đáy:** *"Gửi Yêu Cầu Khiếu Nại & Hoàn Tiền"* màu đỏ `#B52603` vững chãi ở vùng ngón tay cái.

### Màn hình 9: Lịch Sử Đơn Hàng KTX
*   **Đúc kết từ:** Cặp màn hình Group 13.
*   **Tối ưu nổi bật:**
    *   **Sửa lỗi ngắt dòng:** Tên món (*Cơm Tấm Sườn Bì Chả Đặc Biệt*, *Trà Đào Cam Sả Tươi*, *Bún Đậu Mắm Tôm A-B ĐHQG*) và mã đơn (*#KTX-8829B*, *#KTX-8512A*) nằm trọn trên container tự co giãn.
    *   **Thẻ đơn đang giao nổi bật:** Đặt trên cùng với banner *"Shipper đang tới cổng KTX ~3 phút"*, phân tách 2 nút phụ *"Theo dõi trực tiếp"* và *"Mã QR Nhận Hàng"* chuẩn touch target $\ge 48\text{dp}$.
    *   **Nút CTA chính ghim đáy:** Nút to bản *"Mã QR Nhận Hàng"* màu đỏ sậm `#B52603` mở nhanh bằng một tay khi đang đi bộ.
    *   **Duy trì Bottom Navigation:** Tích hợp thanh 5 tab chuẩn ngay dưới CTA chính, chống đứt gãy luồng chuyển trang.

### Màn hình 10: Khiếu Nại & Hoàn Tiền Sau Giao Nhận
*   **Đúc kết từ:** Cặp màn hình Group 14.
*   **Tối ưu nổi bật:**
    *   **Rút ngắn hành trình cuộn:** Gom nhóm sự cố và tự động tính hoàn tiền 100% giúp hoàn tất khiếu nại trong 1.5 chiều dài màn hình.
    *   **Lưới Thumbnail bằng chứng:** Tải ảnh tem niêm phong và chụp ảnh bổ sung dàn hàng ngang không chiếm diện tích dọc.
    *   **CTA chính:** *"Gửi Yêu Cầu Khiếu Nại & Hoàn Tiền"* màu đỏ sậm `#B52603`, cao `52dp`, chữ trọn vẹn 1 dòng.

---

## 4. Bảng tổng hợp so sánh kỹ thuật & trợ năng (Before vs. AI Draft vs. Final Resolved)

| Thành phần UI | Bản Cũ (Before) | Bản Mới (AI Draft) | Bản Chốt Chuẩn (Final Resolved) | Lý do Kỹ thuật & Trợ năng (Accessibility) |
| :--- | :--- | :--- | :--- | :--- |
| **Ngắt dòng tiếng Việt (Text Wrapping)** | Rớt 1–2 chữ cụt lủn ở tên món, mã đơn `#8829B` và nhãn nút bấm. | Container bị co ép chiều ngang ở một số khu vực. | 100% text container dùng `auto-width` & `white-space` linh hoạt. Toàn bộ nhãn nút bấm nằm trọn 1 dòng. | Loại bỏ lỗi typographic orphans; tối ưu khả năng quét lướt (scannability) khi sinh viên đang di chuyển lấy cơm. |
| **Nút CTA Chính & Vùng ngón tay cái** | Nằm inline cuộn theo trang, khó chạm khi cầm máy 1 tay. | Ghim đáy nhưng chiếm trọn đáy, che mất navigation. | Ghim đáy (Sticky Bar) cao $\ge 50\text{dp}$, đỏ `#B52603`, chữ trắng in đậm. | Đạt chuẩn Touch Target Material Design ($\ge 48\times 48\text{dp}$); tương phản màu WCAG 2.1 AA (> 4.5:1). |
| **Thanh Bottom Navigation** | Đầy đủ 5 tab điều hướng chuẩn. | Bị loại bỏ hoàn toàn làm đứt gãy luồng chuyển trang. | Khôi phục hoàn toàn Bottom Navigation 5 tab chuẩn ở đáy màn hình. | Giữ vững kiến trúc thông tin (IA), cho phép sinh viên chuyển tab sang Lịch sử, Tài khoản hoặc Trang chủ tức thì. |
| **Khoảng cách cuộn trang (Compact Layout)** | Rời rạc, thiếu nhịp đệm thị giác. | Bị kéo giãn padding quá mức (> 2400px), cuộn mỏi tay. | Tối ưu Vertical Rhythm: Gom nhóm tùy chọn, bằng chứng và thông tin đối soát súc tích. | Giảm scroll fatigue, đưa các thông tin quan trọng nhất vào màn hình đầu tiên (Above the fold). |
| **Khối Mã QR & Phím Sáng màn hình** | Phím sáng chiếm 1 thanh ngang cồng kềnh. | Dàn nút viền mỏng chiếm diện tích phía dưới QR. | Chuyển thành nút Quick Action icon mặt trời góc QR code ($\ge 48\times 48\text{dp}$). | Thao tác 1 chạm bật sáng nhanh dưới trời nắng gắt, tiết kiệm không gian thẳng đứng. |
| **Vùng chạm nút phụ (Secondary Action)** | Các nút nhỏ đặt sát nhau dễ bấm nhầm ($< 36\text{dp}$). | Dàn nút viền mỏng dàn trải chiếm diện tích. | Nút phụ phân cách tối thiểu 12–16dp, touch target $\ge 48\times 48\text{dp}$. | Ngăn chặn việc bấm trượt hoặc bấm nhầm giữa hai hành động trái ngược khi sinh viên đang đi bộ. |

---

## 5. Đánh giá phản biện AI (AI Critique)

*   **Phát hiện 1 (Heuristic #8 - Thẩm mỹ & Thiết kế tối giản):** AI Draft tự động chèn padding và margin quá mức khiến màn hình bị kéo dài bất thường (> 2400px), buộc sinh viên phải vuốt cuộn nhiều lần để tìm thông tin đơn hàng.
*   **Phát hiện 2 (Heuristic #4 - Nhất quán & Tiêu chuẩn):** AI Draft tự ý xóa bỏ thanh Bottom Navigation 5 tab chuẩn ở đáy màn hình để nhường chỗ cho nút CTA to bản, phá vỡ luồng điều hướng tổng thể của ứng dụng.
*   **Phát hiện 3 (WCAG 2.5.5 - Target Size & Text Wrapping):** Container chữ trên các nút bấm bị gán thuộc tính fixed-width cứng nhắc dẫn đến việc chữ tiếng Việt bị rớt 1–2 từ cụt lủn xuống dòng thứ hai; đồng thời các nút phụ (Theo dõi, Khiếu nại) có chiều cao chỉ 36dp, chưa đạt chuẩn tối thiểu 48dp.
*   **Phát hiện 4 (Persona Sinh viên - Bối cảnh giao nhận KTX):** Nút "Tăng độ sáng màn hình" ở bản AI Draft bị hạ cấp thành nút viền mỏng (outlined) đặt dưới chân trang khiến sinh viên thao tác chậm chạp khi shipper yêu cầu bật sáng màn hình dưới trời nắng gắt.
*   **Phát hiện 5 (Heuristic #5 - Ngăn ngừa lỗi & Tranh chấp dữ liệu):** Trên màn hình lịch sử nhiều đơn hàng, nút CTA dưới chân trang chỉ ghi "Mã QR Nhận hàng" chung chung mà không gắn kèm mã đơn cụ thể `#8829B`, dễ gây nhầm lẫn dữ liệu giữa các đơn đang giao đồng thời.

---

## 6. Quyết định của sinh viên & Lý do kỹ thuật

*   **Đối với Phát hiện 1 (Over-scrolling Layout):** `[Từ chối]`
    *   *Lý do kỹ thuật:* Không chấp nhận bố cục giãn dài của AI. Tái cấu trúc lại nhịp điệu không gian (Vertical Rhythm), gom gọn các cụm bằng chứng thành lưới thumbnail ngang và thu nhỏ padding để đưa thông tin trọng tâm vào màn hình đầu tiên (Above the fold).
*   **Đối với Phát hiện 2 (Mất Bottom Navigation):** `[Từ chối]`
    *   *Lý do kỹ thuật:* Khôi phục lại hoàn toàn thanh Bottom Navigation 5 tab tiêu chuẩn phía dưới nút hành động chính. Việc giữ vững thanh điều hướng đảm bảo tính liên tục của Kiến trúc thông tin (Information Architecture), cho phép sinh viên chuyển đổi tức thì giữa các phân hệ.
*   **Đối với Phát hiện 3 (Lỗi Text Wrapping & Vùng chạm nhỏ):** `[Chấp nhận]`
    *   *Lý do kỹ thuật:* Chuyển đổi toàn bộ text container sang chế độ `auto-width` và `white-space: nowrap` trên các nút bấm để nhãn hiển thị trọn vẹn trên 1 dòng. Nâng chiều cao tương tác của tất cả các nút phụ lên tối thiểu $48\text{dp}$ và nút chính lên $50-52\text{dp}$ theo chuẩn Android Material Design / WCAG 2.5.5.
*   **Đối với Phát hiện 4 (Vị trí nút Tăng độ sáng):** `[Tinh chỉnh]`
    *   *Lý do kỹ thuật:* Không giữ nút dạng viền mỏng ở chân trang của AI, cũng không dùng thanh ngang cồng kềnh của bản cũ. Tinh chỉnh thành Quick-action Icon Button hình mặt trời ($\ge 48\times 48\text{dp}$) đính ngay góc trên bên phải khung QR để sinh viên bật nhanh chỉ với 1 chạm ngón cái.
*   **Đối với Phát hiện 5 (Nhầm lẫn mã đơn hàng):** `[Tinh chỉnh]`
    *   *Lý do kỹ thuật:* Chỉ hiển thị nút Sticky Footer ở đáy màn hình Lịch sử khi có duy nhất 1 đơn đang giao kèm mã định danh cụ thể (*"Mã QR - Đơn #8829B"*). Nếu có từ 2 đơn trở lên, duy trì nút mở mã trực tiếp trên từng card đơn hàng để tránh lỗi xung đột dữ liệu logic (data mismatch).