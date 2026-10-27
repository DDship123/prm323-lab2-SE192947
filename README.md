# Food Ordering App - KTX ĐHQG-HCM

> **Ứng dụng đặt đồ ăn kết nối giữa người bán và sinh viên trong các ký túc xá Khu đô thị Đại học Quốc gia TP.HCM (ĐHQG-HCM).**  
> Môn học: **PRM323 - Mobile Programming (Lab 2 - UI/UX Design & AI-assisted Prototyping)**  
> Lớp / Nhóm Zalo: `FA26-31-PRM323`

---

## 👥 Thông Tin Nhóm & Thành Viên

| STT | Họ và Tên | MSSV | Vai trò phụ trách chính trong Lab 2 |
| :---: | :--- | :---: | :--- |
| 1 | **Bùi Bảo Dương** | SE192947 | **Team Leader** – Khởi tạo ý tưởng UI/UX tổng quan, sinh 32 màn hình ban đầu bằng Stitch AI & Figma AI. |
| 2 | **Ngô Hoàng Trường Đạt** | SE192964 | **Design System Lead** – Xây dựng hệ thống Design Tokens & 9 bộ Master Components, phản biện Nielsen Heuristics. |
| 3 | **Trần Sanh Điền** | SE192850 | **Prototyping & Handoff Lead** – Thiết lập Design System, đặc tả Screen Spec và lập tài liệu Flutter Handoff. |
| 4 | **Quách Ngọc Vinh** | SE194159 | **UI/UX Refinement Lead** – Thực hiện 3 vòng lặp tinh chỉnh giao diện trên Stitch AI, tối ưu Touch Target & WCAG 2.1 AA. |

---

## 🎯 1. Chủ Đề Dự Án (Project Topic)

* **Tên dự án:** Food Ordering App – Ký túc xá ĐHQG-HCM (KTXFood).
* **Mô tả giải pháp:** Ứng dụng đặt đồ ăn kết nối trực tiếp các quán ăn bình dân lân cận với sinh viên nội trú KTX ĐHQG-HCM. Giải quyết bài toán ăn uống tiện lợi, tiết kiệm chi phí vận chuyển thông qua **cơ chế gom đơn giao tập trung theo ca cố định** (Ca trưa 11h30 và Ca tối 18h00) ngay trước cổng KTX (Cổng KTX Khu A, Cổng KTX Khu B), khắc phục tình trạng cấm xe vào KTX và chen chúc thất lạc đơn giờ cao điểm.

---

## 👤 2. Persona Một Dòng (One-line Persona)

> **Nguyễn Văn Tuấn (18 tuổi, sinh viên năm nhất nội trú KTX Khu A – ĐHQG-HCM):** Không có xe máy và ngân sách eo hẹp, cần ứng dụng đặt đồ ăn giá bình dân gom theo khung giờ cố định và đối soát nhận món siêu tốc (< 20s) bằng mã QR tại cổng KTX để kịp giờ ăn giữa các ca học dày đặc mà không lo bị đội phí ship hay chen chúc thất lạc đơn.

---

## 🎨 3. Liên Kết Thiết Kế Figma (Figma Prototype Link)

* 🔗 **Figma Design & Prototype chính thức:**  
  👉 [**Lab 2 - Food Ordering App on Figma**](https://www.figma.com/design/ALDYFWUZ72BaeyulpVi7uY/Lab-2-Food-Ordering-App?t=1J5Hgu4W5Wy0dUkh-1)  
  *(URL: `https://www.figma.com/design/ALDYFWUZ72BaeyulpVi7uY/Lab-2-Food-Ordering-App?t=1J5Hgu4W5Wy0dUkh-1`)*
* **File khóa tham chiếu:** File chính `84O0L9O6Z5TVkMjBvMRn33`, File phụ `ALDYFWUZ72BaeyulpVi7uY`.
* **Nội dung trên Figma:** Bao gồm các trang Cover, Sitemap & Information Architecture, Design System Tokens & Master Components, Student Screens (Flow 1, 2, 3), và Interactive Prototype.

---

## 🤖 4. Danh Sách Công Cụ AI Đã Dùng (AI Tools Declared)

| STT | Công cụ AI | Phiên bản / Môi trường | Mục đích sử dụng cụ thể trong dự án | Thành viên phụ trách |
| :---: | :--- | :--- | :--- | :--- |
| 1 | **Google Stitch (Stitch AI)** | Web UI Prompting & Stitch Canvas Agent | Khởi tạo khung layout ban đầu, phân bổ thông tin và sinh wireframe/mockup UI cho 32 màn hình nghiệp vụ từ prompt tiếng Việt. | Bùi Bảo Dương, Quách Ngọc Vinh |
| 2 | **Figma AI Agent / Figma Workspace** | Tích hợp trong Figma Design | Tạo các biến thể ban đầu cho 9 bộ Master Components, thiết lập Design Tokens, Auto Layout và liên kết các artboard màn hình. | Bùi Bảo Dương, Ngô Hoàng Trường Đạt |
| 3 | **Claude (Anthropic)** | Claude 3.5 Sonnet / Claude 3.7 Sonnet | Đóng vai trò Chuyên gia UX/UI: Tinh chỉnh cấu trúc prompt, phản biện thiết kế theo 10 Usability Heuristics của Jakob Nielsen, đối soát chuẩn tiếp cận WCAG 2.1 AA ngoài trời nắng gắt, và tính toán tỷ lệ tương phản. | Ngô Hoàng Trường Đạt, Trần Sanh Điền, Quách Ngọc Vinh |
| 4 | **ChatGPT (OpenAI)** | GPT-4o / Web Interface & Chat Agent | Hỗ trợ đối soát tính nhất quán của kịch bản người dùng (Critical Scenarios), kiểm tra logic nghiệp vụ gom đơn và rà soát tài liệu đặc tả. | Toàn nhóm |

---

## 🗺️ 5. Bản Đồ Nơi Tìm Từng Sản Phẩm (Deliverables Sitemap)

Toàn bộ các tài liệu đặc tả, thiết kế, phân tích UX và nhật ký AI được phân bổ rõ ràng theo cấu trúc thư mục chuẩn:

```text
PRM323_Lab2_Project/
├── README.md                      # Thông tin nhóm, chủ đề, persona một dòng, link Figma, AI tools, bản đồ sản phẩm
├── food_ordering_app_srs.md       # Đặc tả yêu cầu hệ thống (SRS), User Stories (Học sinh, Shipper, Quán ăn)
│
├── docs/                          # TÀI LIỆU SẢN PHẨM & QUY TẮC NGHIỆP VỤ (PRODUCT & BUSINESS RULES)
│   ├── PRD.md                     # Product Requirement Document: Bối cảnh, mục tiêu, scope, flows, NFRs, roadmap
│   └── business-rules.md          # Đặc tả chi tiết 16 Business Rules (BR-01 -> BR-16), phân quyền & ngoại lệ
│
├── ux/                            # PHÂN TÍCH TRẢI NGHIỆM NGƯỜI DÙNG (UX ANALYSIS)
│   ├── persona.md                 # Thẻ Proto-Persona P01 (Nguyễn Văn Tuấn), JTBD, Critical Scenario & Success Metrics
│   └── user-flow.md               # Kiến trúc thông tin (IA) & 3 User Flows chi tiết bằng sơ đồ Mermaid
│
├── design/                        # HỆ THỐNG THIẾT KẾ & ĐẶC TẢ GIAO DIỆN (UI DESIGN SYSTEM)
│   ├── DESIGN.md                  # Design System Specification: Color Tokens, Typography, 8-pt Grid, 9 Master Components
│   ├── screen-spec.md             # Đặc tả chi tiết từng màn hình UI (S1 -> S10), mục đích, node Figma, luồng tương tác
│   └── design-decisions.md        # 10 quyết định thiết kế cốt lõi gắn với Heuristics Nielsen & ràng buộc bối cảnh KTX
│
├── handoff/                       # TÀI LIỆU CHUYỂN GIAO KỸ THUẬT (DEVELOPMENT HANDOFF)
│   └── flutter-handoff.md         # Hướng dẫn handoff cho Flutter: ThemeData M3, Widget mapping, Responsive, Accessibility
│
├── ai/                            # NHẬT KÝ THIẾT KẾ BẰNG AI CỦA 4 THÀNH VIÊN (AI DESIGN LOGS)
│   ├── Dương/ai-design-log.md     # Thành viên 1: Khởi tạo 32 màn hình ban đầu của dự án bằng Stitch AI & Figma AI
│   ├── Dat/ai-design-log.md       # Thành viên 2: Tạo lập, phản biện và tối ưu 9 Master Components bằng Figma AI & Claude
│   ├── Điền/ai-design-log.md      # Thành viên 3: Thiết kế Master Components, Design System và đối soát chuẩn WCAG 2.1 AA
│   └── Vinh/ai-design-log.md      # Thành viên 4: 3 vòng lặp tinh chỉnh & phản biện UI/UX trên Stitch AI và Claude
│
└── assests/                       # THƯ MỤC MINH CHỨNG HÌNH ẢNH PROMPT & ARTBOARD
    ├── stitch/                    # Ảnh chụp prompt & kết quả giao diện sinh từ Stitch AI (Dương, Vinh)
    ├── figma/                     # Ảnh chụp artboard, Master Components & Prototype trên Figma (Đạt, Điền)
    └── claude/                    # Minh chứng các phiên phản biện tương tác với Claude
```

### Bảng tra cứu nhanh vị trí các tài liệu nộp bài:

| Hạng mục tài liệu | File tài liệu tương ứng trong repository | Nội dung then chốt |
| :--- | :--- | :--- |
| **0. Product Requirements (PRD)** | [`docs/PRD.md`](docs/PRD.md) | Tổng quan bài toán KTX, User Personas, Scope, NFRs, Metrics và Phasing Roadmap. |
| **0. Business Rules (BR)** | [`docs/business-rules.md`](docs/business-rules.md) | Đặc tả 16 Quy tắc nghiệp vụ (Cut-off time, Gom đơn, VietQR, Đối soát 2 lớp, Hoàn tiền). |
| **1. Persona & Problem Statement** | [`ux/persona.md`](ux/persona.md) | Thẻ Proto-Persona chuẩn, JTBD, bối cảnh KTX, tiêu chí hoàn tất đặt món < 30s và nhận đồ < 20s. |
| **2. User Flow & Screen Architecture** | [`ux/user-flow.md`](ux/user-flow.md) | Phân cấp điều hướng 2 tầng, danh mục màn hình Figma, 3 sơ đồ Flow chi tiết. |
| **3. Design System & Tokens** | [`design/DESIGN.md`](design/DESIGN.md) | Bộ Color Tokens chuẩn M3, Typography Scale, 8-pt Grid và 9 bộ Master Components. |
| **4. UI Screen Specification** | [`design/screen-spec.md`](design/screen-spec.md) | Chi tiết 11 màn hình/dialog gắn với mã node Figma và ý đồ thiết kế theo Persona. |
| **5. Design Decisions & Heuristics**| [`design/design-decisions.md`](design/design-decisions.md) | 10 quyết định thiết kế đối chiếu trực tiếp 10 Nielsen Heuristics và bối cảnh thực tế KTX. |
| **6. Flutter Handoff Guide** | [`handoff/flutter-handoff.md`](handoff/flutter-handoff.md) | Ánh xạ Flutter Widgets, ThemeData M3, xử lý độ sáng ngoài trời, touch target $\ge 48\text{dp}$. |
| **7. AI Design Logs & Minh chứng** | Thư mục [`ai/`](ai/) & [`assests/`](assests/) | Nhật ký 3 vòng lặp tinh chỉnh có ý nghĩa, nguyên văn prompts và ảnh chụp đối chứng của 4 thành viên. |
