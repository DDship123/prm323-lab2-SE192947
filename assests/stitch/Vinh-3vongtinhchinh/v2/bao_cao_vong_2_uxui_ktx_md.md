# BÁO CÁO MỤC 4.3: VÒNG LẶP 2 - BỔ SUNG TRẠNG THÁI TRỐNG (EMPTY STATE) VÀ THÔNG BÁO LỖI (ERROR STATE)

---

## 1. Nguyên văn Prompt đã nhập cho Stitch (Vòng 2)

```text
Tôi đính kèm ảnh giao diện ứng dụng nhận hàng/theo dõi đơn KTX của sinh viên hiện tại.
Nhiệm vụ:
Hãy giữ nguyên hệ thống thiết kế (Design System: tone màu chủ đạo, font chữ, độ bo góc, thanh Header và Bottom Navigation) của màn hình hiện tại và tạo ra 2 trạng thái giao diện mới (Vòng 2: Edge Cases) đặt cạnh nhau:

Trạng thái trống (Empty State):
- Ngữ cảnh: Sinh viên mở tab "Theo dõi đơn" hoặc "Lịch sử đơn" nhưng hiện tại không có đơn hàng nào cần nhận trong ngày.
- Yêu cầu UI:
  + Giữ nguyên thanh Header và thanh Bottom Navigation.
  + Khu vực nội dung trung tâm (Center body): Đặt một hình minh họa (Illustration/Icon 3D hoặc outline phẳng) thể hiện trạng thái trống (ví dụ: hộp rỗng, giỏ đồ ăn trống).
  + Tiêu đề (Headline, Bold 18–20sp): "Chưa có đơn hàng nào cần nhận".
  + Đoạn phụ (Body text, 14sp, màu xám #64748B): "Bạn không có đơn giao đến cổng KTX trong khung giờ này. Đặt món ngay để kịp chốt đơn nhé!".
  + Nút hành động chính (Primary Action CTA): Nút "Khám phá quán ngon / Đặt món ngay" (màu đỏ thương hiệu #B52603, chữ trắng, chiều cao >= 48dp, bo góc 8–12dp).

Trạng thái thông báo lỗi (Error State):
- Ngữ cảnh: Mất kết nối mạng (Network Timeout / Offline) hoặc lỗi server không thể tải dữ liệu đơn / không quét được mã nhận hàng.
- Yêu cầu UI:
  + Biểu tượng cảnh báo lỗi (Icon/Illustration về mất kết nối WiFi hoặc chấm than cảnh báo màu cam/đỏ).
  + Tiêu đề lỗi (Headline, Bold 18–20sp): "Mất kết nối máy chủ".
  + Mô tả chi tiết (Body text, 14sp, màu xám #64748B): "Không thể đồng bộ dữ liệu đơn hàng. Vui lòng kiểm tra lại kết nối WiFi/4G hoặc thử lại.".
  + Cụm nút hành động:
    * Nút chính (Primary CTA): Nút "Thử lại" (Retry), chiều cao tối thiểu 48dp, nền đỏ thương hiệu #B52603.
    * Nút phụ (Secondary CTA, dạng Outlined/Text button): "Xem hướng dẫn nhận hàng offline" hoặc "Liên hệ hỗ trợ KTX".

Đầu ra yêu cầu:
- Tạo hình ảnh trực quan rõ nét của 2 màn hình này (Side-by-side).
- Cung cấp bảng tóm tắt: [Trạng thái | Thành phần trực quan | Nội dung thông điệp | Nút hành động CTA | Lý do kỹ thuật / UX].
```

---

## 2. Lưu trữ hình ảnh đối chiếu Vòng 2

* **Bản gốc ban đầu (Trạng thái bình thường có đơn):** `assets/stitch/v2_before.png`
* **Bản hoàn thiện hậu quyết định (Empty State & Error State song song):** `assets/stitch/v2_after.png`

---

## 3. Chi tiết tối ưu hóa 2 màn hình biên (Edge-case States)

### Màn hình 11: Trạng Thái Trống - Chưa Có Đơn Hàng (Empty State)
* **Ngữ cảnh:** Sinh viên truy cập tab *Lịch sử* / *Theo dõi đơn* nhưng không có đơn hàng nào đang diễn ra hoặc cần nhận trong ca giao nhận hiện tại tại KTX.
* **Điểm nổi bật UI & Công thái học:**
  * **Bảo toàn khung ứng dụng:** Header nhận diện thương hiệu *KTX KHU B* và thanh Bottom Navigation 5 tab tiêu chuẩn (*Khám phá*, *Đặt món*, *Thanh toán*, *Lịch sử [Active]*, *Tài khoản*) được giữ nguyên vẹn.
  * **Minh họa trung tâm (Illustration):** Hình vẽ hộp cơm giữ nhiệt / túi thức ăn rỗng với tone màu cam ấm và đỏ thương hiệu, tạo cảm giác thân thiện thay vì màn hình trống trơn tiêu cực.
  * **Hệ thống nội dung:**
    * *Tiêu đề:* "Chưa có đơn hàng nào cần nhận" (`Bold 19px`, màu `#0F172A`).
    * *Mô tả phụ:* "Bạn không có đơn giao đến cổng KTX trong khung giờ này. Đặt món ngay để kịp chốt đơn nhé!" (`14px`, màu xám `#64748B`, giãn dòng thoáng đãng, không bị ngắt dòng cụt lủn).
  * **Nút CTA chính:** *"Khám phá quán ngon / Đặt món ngay"* màu đỏ sậm thương hiệu `#B52603`, chữ trắng in đậm, chiều cao `50dp` ($\ge 48\text{dp}$), bo góc `12px`, độ tương phản màu đạt $6.47:1$ (vượt chuẩn WCAG AA).
  * **Widget kích cầu (Conversion Trigger):** Thẻ card *"Gợi ý ca gom hôm nay"* hiển thị ca trưa đang mở nhận đơn (chốt lúc `10:45`), hỗ trợ sinh viên thao tác tiếp mà không gặp tình trạng "cụt đường" (dead-end).

### Màn hình 12: Trạng Thái Lỗi - Mất Kết Nối Máy Chủ (Error State)
* **Ngữ cảnh:** Mất kết nối mạng (Network Timeout / Offline) hoặc máy chủ gặp sự cố không thể đồng bộ dữ liệu đơn hoặc mã QR đối soát khi sinh viên đứng đợi tại bàn nhận cơm KTX.
* **Điểm nổi bật UI & Công thái học:**
  * **Banner cảnh báo đỉnh:** Dải thông báo màu cam đỏ nhạt *"Mất kết nối mạng • Dữ liệu chưa cập nhật"* với biểu tượng sóng mất kết nối.
  * **Minh họa lỗi trực quan:** Biểu tượng mất tín hiệu mạng tại điểm nhận hàng KTX Khu B kèm dấu chấm than cảnh báo màu đỏ trực diện.
  * **Hệ thống nội dung:**
    * *Tiêu đề lỗi:* "Mất kết nối máy chủ" (`Bold 19px`, màu `#0F172A`).
    * *Mô tả chi tiết:* "Không thể đồng bộ dữ liệu đơn hàng. Vui lòng kiểm tra lại kết nối WiFi/4G hoặc thử lại." (`14px`, màu xám `#64748B`).
  * **Cụm nút hành động kép (Action Cluster):**
    * *Nút chính (Primary CTA):* *"Thử lại kết nối"* nền đỏ `#B52603`, chữ trắng in đậm kèm icon làm mới (chiều cao `50dp` $\ge 48\text{dp}$).
    * *Nút phụ (Secondary CTA):* *"Xem cách nhận hàng offline"* viền bo mảnh, nền trắng chữ đậm.
  * **Phương án cứu sinh (Graceful Degradation):** Thẻ hướng dẫn giải pháp nhận cơm khẩn cấp: *"Đọc trực tiếp 4 số cuối SĐT cho Điều phối viên tại Bàn gom"* kèm hotline 1-chạm *"Gọi Trực Bàn Gom KTX (1900 6899)"*, đảm bảo sinh viên luôn lấy được suất ăn dù thiết bị mất kết nối.

---

## 4. Bảng tóm tắt so sánh kỹ thuật & UX (Edge Cases)

| Trạng thái | Thành phần trực quan | Nội dung thông điệp | Nút hành động CTA | Lý do kỹ thuật & Trợ năng (Accessibility) |
| :--- | :--- | :--- | :--- | :--- |
| **Trạng thái trống (Empty State)** | Hình minh họa hộp cơm giữ nhiệt rỗng tone ấm; thẻ card gợi ý ca trưa KTX gom đơn. | • Tiêu đề: *"Chưa có đơn hàng nào cần nhận"*<br>• Phụ: *"Bạn không có đơn giao đến cổng KTX trong khung giờ này. Đặt món ngay để kịp chốt đơn nhé!"* | • **Chính:** Khám phá quán ngon / Đặt món ngay (Nền đỏ `#B52603`, cao $50\text{dp} \ge 48\text{dp}$)<br>• **Phụ:** Card gợi ý ca gom đang mở chốt lúc 10:45 | **Nielsen #10 & Conversion UX:** Tránh hiện tượng màn hình trắng trơn gây hoang mang; chuyển đổi trạng thái trống thành cơ hội dẫn dắt sinh viên đặt món trước giờ đóng ca. |
| **Trạng thái lỗi (Error State)** | Icon cảnh báo ngắt kết nối WiFi/Server; banner cảnh báo đỉnh màu cam đỏ nhạt; icon chấm than trực quan. | • Tiêu đề: *"Mất kết nối máy chủ"*<br>• Phụ: *"Không thể đồng bộ dữ liệu đơn hàng. Vui lòng kiểm tra lại kết nối WiFi/4G hoặc thử lại."* | • **Chính:** Thử lại kết nối (Nền đỏ `#B52603`, cao $50\text{dp} \ge 48\text{dp}$)<br>• **Phụ:** Xem cách nhận hàng offline + Nút gọi trực tiếp hotline Bàn gom (1900 6899) | **Nielsen #9 & Graceful Degradation:** Giảm cảm giác hoang mang khi đứng đợi lấy cơm mà mất sóng; cung cấp lối thoát thực tế (đối soát 4 số cuối SĐT hoặc gọi điều phối viên). |

---

## 5. Đánh giá phản biện AI (AI Critique)

* **Phát hiện 1 (Heuristic #9 - Giúp người dùng nhận biết, chẩn đoán và phục hồi sau lỗi):**
  * *Chi tiết:* Màn hình Error State ban đầu nếu chỉ có một thông báo lỗi "Không thể kết nối" và một nút "Thử lại" đơn lẻ sẽ đẩy sinh viên vào thế bế tắc nếu khu vực cổng KTX bị mất sóng 4G kéo dài.
* **Phát hiện 2 (Heuristic #10 - Trợ giúp và tài liệu hướng dẫn / Anti-Dead-end):**
  * *Chi tiết:* Màn hình Empty State nếu để trống trơn hoàn toàn sẽ tạo ra trải nghiệm "đường cùng UX" (Dead-end), khiến sinh viên nghĩ rằng ứng dụng bị lỗi dữ liệu hoặc không biết phải làm gì tiếp theo.
* **Phát hiện 3 (WCAG 2.1 - Tiêu chí 2.5.5 Target Size & Công thái học):**
  * *Chi tiết:* Nút "Thử lại" và nút gọi hotline khẩn cấp cần được bảo đảm kích thước chạm tối thiểu $48\times 48\text{dp}$ với khoảng cách an toàn, vì người dùng trong trạng thái gặp lỗi mạng thường có tâm lý ức chế, dễ thao tác vội vàng dẫn đến chạm trượt.
* **Phát hiện 4 (Persona Sinh viên - Ngữ cảnh nhận cơm KTX):**
  * *Chi tiết:* Vào giờ cao điểm nhận cơm trưa, sinh viên đổ ra sảnh rất đông dẫn đến nghẽn mạng cục bộ. Nếu ứng dụng không có cơ chế lưu trữ đệm (Client-side Caching) để hiển thị thông tin đối soát ngoại tuyến, sinh viên sẽ không thể chứng minh đơn hàng với shipper.
* **Phát hiện 5 (WCAG 1.4.3 - Contrast Minimum & Hierarchy):**
  * *Chi tiết:* Các thông điệp cảnh báo trên banner đỉnh và đoạn mô tả giải thích lỗi cần sử dụng màu sắc có tỷ lệ tương phản đạt chuẩn AA ($> 4.5:1$), tránh dùng màu xám quá nhạt hoặc nền đỏ gắt gây khó chịu cho mắt.

---

## 6. Quyết định của sinh viên & Lý do kỹ thuật

* **Đối với Phát hiện 1 (Bế tắc khi lỗi mạng kéo dài):** `[Chấp nhận]`
  * *Lý do kỹ thuật:* Bổ sung cơ chế **Graceful Degradation** bằng thẻ cứu sinh: hướng dẫn đọc 4 số cuối SĐT cho điều phối viên tại bàn gom và tích hợp hotline 1-chạm `1900 6899`. Đảm bảo sinh viên luôn nhận được suất ăn mà không phụ thuộc hoàn toàn vào kết nối internet.
* **Đối với Phát hiện 2 (Dead-end ở Empty State):** `[Chấp nhận]`
  * *Lý do kỹ thuật:* Tích hợp widget kích cầu hiển thị ca gom trưa đang mở (chốt đơn lúc `10:45`) kèm nút Primary CTA *"Khám phá quán ngon / Đặt món ngay"*. Việc này mở lại luồng tương tác người dùng, biến trạng thái rỗng thành điểm bắt đầu của hành vi mua sắm.
* **Đối với Phát hiện 3 (Kích thước vùng chạm khi khẩn cấp):** `[Chấp nhận]`
  * *Lý do kỹ thuật:* Chuẩn hóa toàn bộ nút hành động (*Thử lại kết nối*, *Xem cách nhận hàng offline*, *Khám phá quán ngon*) đạt chiều cao $50\text{dp}$ ($\ge 48\text{dp}$), bo góc `12px` và khoảng cách giữa hai nút tối thiểu $12\text{dp}$ theo đúng chuẩn Material Design Target Size.
* **Đối với Phát hiện 4 (Nghẽn mạng giờ cao điểm tại KTX):** `[Tinh chỉnh]`
  * *Lý do kỹ thuật:* Đề xuất kiến trúc lưu trữ cục bộ (Local Storage / Cache) mã đơn `#8829B` và 4 số cuối SĐT ngay từ lúc đặt hàng thành công. Khi rơi vào Error State, hệ thống vẫn hiển thị được các trường thông tin cơ bản này để đối soát trực tiếp mà không cần tải lại toàn bộ trang.
* **Đối với Phát hiện 5 (Độ tương phản và phân cấp màu sắc):** `[Chấp nhận]`
  * *Lý do kỹ thuật:* Sử dụng màu nền cảnh báo `#FFDAD6` kết hợp icon chữ `#BA1A1A` cho banner lỗi (tương phản đạt $> 7:1$), văn bản mô tả quy chuẩn về mã màu Slate `#64748B`, chữ tiêu đề dùng `#0F172A` đảm bảo khả năng đọc lướt rõ ràng dưới mọi điều kiện ánh sáng ngoài trời.