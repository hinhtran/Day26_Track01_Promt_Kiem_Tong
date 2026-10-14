# BÁO CÁO ÁP DỤNG AI - AI ADOPTION CHANGE MANAGEMENT

**Dự án:** Trợ lý AI Tra cứu Quy trình & Chính sách Nội bộ
**Tên nhóm:** Promt Kiếm Tông
**Mã repo chuẩn:** `Day26_Track01_Promt_Kiem_Tong`
**Track:** Track 01 - AI Adoption & Workflow Transformation
**Ngày thực hiện:** 14/10/2026

---

## 1. Bảng thành viên & Phân công nhiệm vụ (Team Members)

| Họ và tên                                     | MSSV            | Phần phụ trách trong bài                                                                                                                                                                                                                                                                                    | Góp ý đã đưa cho nhóm bạn (Nhóm 05)                                                                                                                                                                                                                                                   |
| :----------------------------------------------- | :-------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Trần Đình Hinh** *(Nhóm trưởng)* | `2A202602399` | - Chẩn đoán tổ chức:**Gartner-Lite** (Đánh giá Direction, Readiness dữ liệu/governance, Absorption).- Phân chia ranh giới Người – AI: **Mollick Model** (Xác định vùng Human in charge, AI assist, AI automated).                                                                | Nhóm 05: Chỉ số*"Số lượng prompt/câu hỏi gửi lên AI"* là **Activity metric** ảo, chỉ đo tần suất gõ phím. Đề xuất đổi sang *"Tỷ lệ tra cứu thành công không cần hỏi lại đồng nghiệp"* để phản ánh đúng chất lượng và năng suất thật. |
| **Hoàng Quốc Dũng**                     | `2A202602523` | - Thiết kế lại quy trình: So sánh**AS-IS vs TO-BE**.- Xây dựng **Kiến trúc tin cậy khép kín** (Nguồn $\rightarrow$ Trích nguồn $\rightarrow$ QA $\rightarrow$ Chuyển người $\rightarrow$ Học lại).- Lập lộ trình **Gates 30–60–90 ngày** theo bằng chứng. | Nhóm 05: Quy trình TO-BE của nhóm bạn chưa có vai trò**Data Owner** chịu trách nhiệm thẩm định và cập nhật văn bản mới vào kho RAG, dẫn tới nguy cơ AI trích dẫn văn bản hết hiệu lực. Cần bổ sung Data Owner vào Gate 0–30 ngày.                    |
| **Đinh Xuân Quyền**                     | `2A202602358` | - Chẩn đoán tâm lý người dùng:**ADKAR Model** (Xác định điểm nghẽn Desire).- Xây dựng **Dashboard Hành Động v1 & v2** (5 tầng đo lường).- Soạn thảo **Memo Quyết định** (5 phần).                                                                                | Nhóm 05: Cột*"Hành động khi chỉ số xấu"* còn để chung chung (*'Họp xem xét'*). Nhóm cần quy định rõ SLA khẩn cấp (ví dụ: tạm dừng nạp dữ liệu và debug pipeline retrieval trong 48h khi lỗi trích nguồn).                                                   |

---

## 2. Phạm vi đã khóa (Scope Lock)

- **1 Sản phẩm AI cụ thể:** Trợ lý AI Tra cứu Tài liệu & Quy trình Nội bộ (Internal Knowledge AI Assistant / RAG).
- **1 Nhóm người dùng chính:** 25 chuyên viên thuộc Phòng Vận hành & Hỗ trợ Khách hàng (Operations & CS Support).
- **3 Bước quy trình liên quan:**
  1. *Tiếp nhận yêu cầu:* Nhân viên tiếp nhận tình huống/câu hỏi nghiệp vụ phức tạp từ khách hàng hoặc chi nhánh.
  2. *Tra cứu quy trình & kiểm chứng:* Đưa tình huống vào AI để tìm kiếm điều khoản, đọc trích dẫn nguồn, kiểm tra ngày cập nhật chính sách.
  3. *Xử lý nghiệp vụ & Báo lỗi:* Áp dụng chính sách để phản hồi khách hàng; trường hợp AI không chắc chắn hoặc phát hiện lỗi thì kích hoạt chuyển giao cho chuyên viên cấp cao / bấm nút báo lỗi.
- **1 Vấn đề đo được:** Mặc dù 100% nhân viên đã được cấp tài khoản, tỷ lệ quay lại sử dụng AI sau 2 tuần chỉ đạt **18%**. Nhân viên vẫn lục tìm file Word/PDF thủ công trong các thư mục dùng chung, thời gian tra cứu trung bình mất **8.5 phút/lượt**.

---

## 3. Nguyên nhân gốc & Bằng chứng

### 3.1. Hai nguyên nhân gốc (kèm Framework phân tích)

1. **Nguyên nhân gốc 1 (Độ tin cậy & Quản trị dữ liệu - Framework Gartner-Lite):**
   - *Phân tích Gartner-Lite:* Hướng đi (*Direction*) rõ ràng là giảm thời gian tìm kiếm; tuy nhiên Mức sẵn sàng (*Readiness*) bị **THIẾU NGHIÊM TRỌNG**. Dữ liệu văn bản nội bộ bị phân mảnh (nhiều phiên bản chồng chéo, văn bản cũ chưa lưu trữ), thiếu vai trò **Data Owner** chịu trách nhiệm phê duyệt nội dung nạp vào AI.
   - *Hệ quả:* AI đưa ra câu trả lời không kèm nguồn trích dẫn cụ thể (không có tên văn bản, số điều khoản, ngày hiệu lực), dẫn đến câu trả lời không có căn cứ pháp lý để sử dụng.
2. **Nguyên nhân gốc 2 (Tâm lý e ngại rủi ro - Framework ADKAR):**
   - *Phân tích ADKAR:* Nhân viên hiểu vì sao công ty mua AI (*Awareness* đạt), nhưng bị nghẽn nghiêm trọng ở **Desire (Động lực/Mong muốn áp dụng)**.
   - *Hệ quả:* Trong ngành vận hành, nếu tư vấn sai chính sách sẽ bị trừ KPI hoặc chịu trách nhiệm kỷ luật. Vì AI không có trích dẫn nguồn kiểm chứng, nhân viên chọn giải pháp an toàn nhất là quay lại mở file thủ công hoặc hỏi đồng nghiệp có thâm niên. Do đó, việc mở lớp đào tạo prompt (*Knowledge*) là sai điểm nghẽn và hoàn toàn vô tác dụng.

### 3.2. Bằng chứng thực tế

- **Bằng chứng định lượng nội bộ (Log hệ thống & Phỏng vấn):**
  - Trích xuất log AI 30 ngày gần nhất: 65% phiên tra cứu bị người dùng tắt ngang sau câu trả lời đầu tiên mà không có hành động sao chép hay đánh giá.
  - Phỏng vấn sâu 10 chuyên viên vận hành: 100% (10/10 người) trả lời *"Không dám dùng câu trả lời của AI gửi khách hàng vì không biết AI lấy từ quyết định ban hành năm nào, nếu khách khiếu nại thì ai chịu trách nhiệm?"*.
- **Bài học tham chiếu (Case study Morgan Stanley):**
  - Morgan Stanley khi triển khai GPT-4 cho 16.000 cố vấn tài chính đã chỉ ra: **Độ tin cậy và kiểm chứng nguồn (Verifiable Citations) phải đi trước việc mở rộng quy mô (Scale)**. Chỉ khi mỗi câu trả lời gắn chặt với tài liệu gốc và có con người chịu trách nhiệm cuối cùng thì tỷ lệ adoption mới đạt trên 90%.

---

## 4. Cách làm mới (Workflow TO-BE & Kiến trúc tin cậy)

### 4.1. So sánh AS-IS vs TO-BE

|   Bước   | Quy trình cũ (AS-IS)                                                                                           | Quy trình mới thiết kế lại (TO-BE)                                                                                                                                                                                                    | Điểm thay đổi cốt lõi                                                                 |
| :---------: | :--------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------ |
| **1** | Mở thư mục ổ đĩa mạng chung, tìm kiếm từ khóa trong hàng chục file Word/PDF.                        | Nhập câu hỏi nghiệp vụ vào Trợ lý AI theo cấu trúc chuẩn:*[Nghiệp vụ] + [Tình huống] + [Yêu cầu điều khoản]*.                                                                                                        | Tiết kiệm 80% thời gian tìm kiếm ban đầu.                                            |
| **2** | Tự đọc lướt các file, khó xác định văn bản nào là bản sửa đổi mới nhất.                      | AI trả lời kèm**Trích dẫn nguồn trực tiếp** (Tên văn bản, Số quyết định, Điều/Khoản, Ngày ban hành & Ngày hiệu lực).                                                                                          | **Kiểm chứng nguồn ngay lập tức**; loại bỏ rủi ro văn bản hết hạn.        |
| **3** | Nếu không tìm thấy, nhắn tin hỏi đồng nghiệp thâm niên (gây gián đoạn công việc người khác). | **Phân chia trách nhiệm (Mollick):** Chuyên viên kiểm tra nhanh trích dẫn nguồn, đối chiếu và chịu trách nhiệm duyệt nội dung trước khi gửi khách.                                                             | Con người giữ quyền phê duyệt cuối (*Human-in-the-loop*).                          |
| **4** | Không có cơ chế ghi nhận lỗi của tài liệu.                                                              | - Nếu AI đạt độ tin cậy: Sử dụng kết quả.- Nếu AI không chắc chắn (<85% confidence): Hệ thống tự động chuyển ticket sang Chuyên viên chính.- Nút **Báo lỗi 1-Click** để Data Owner cập nhật tri thức. | **Kiến trúc tin cậy khép kín** và cơ chế học lại từ lỗi (*Absorption*). |

### 4.2. Ba thay đổi bắt buộc theo chuẩn bài Lab

1. **Nguồn kiểm chứng:** Mọi câu trả lời của AI bắt buộc hiển thị trích dẫn có thể click xem tài liệu gốc (Document Link, Section, Effective Date).
2. **Người chịu trách nhiệm:** Quy chế quy định rõ AI là công cụ hỗ trợ tổng hợp (*Mollick - AI Assist*), Chuyên viên vận hành là người chịu trách nhiệm pháp lý cho quyết định áp dụng (*Mollick - Human in Charge*).
3. **Cách xử lý khi AI không chắc:** Nếu câu hỏi nằm ngoài phạm vi tài liệu đã nạp hoặc độ tin cậy dưới ngưỡng an toàn, AI phải thông báo: *"Dữ liệu chưa đủ căn cứ, đề xuất chuyển chuyên viên hỗ trợ"*, kèm link mở ticket nội bộ.

---

## 5. Hệ thống chỉ số ra quyết định (Dashboard v2)

| Chỉ số                                                                     |         Tầng đo lường         |       Phân loại       |           Mốc ban đầu (Baseline)           |     Mục tiêu (Target)     | Nguồn dữ liệu                                           | Người phụ trách (Owner)     | Hành động khi chỉ số xấu                                                                                                                   |
| :--------------------------------------------------------------------------- | :-------------------------------: | :----------------------: | :--------------------------------------------: | :--------------------------: | :--------------------------------------------------------- | :------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Tỷ lệ câu trả lời có trích dẫn nguồn chính xác**          | Tầng 4: Chất lượng & Tin cậy | **Product-level** |        0% (Bản cũ không trích dẫn)        |       **≥ 95%**       | Audit log của hệ thống RAG & QA kiểm tra ngẫu nhiên  | AI Tech Lead (Kỹ sư AI)       | Tạm dừng nạp tài liệu mới; tối ưu lại chunking/retrieval và prompt sinh trích dẫn; kiểm tra lại pipeline indexing trong 48h.       |
| **Thời gian hoàn thành một lượt tra cứu**                       |       Tầng 3: Năng suất       | **Workflow-level** | **8.5 phút** (Tra cứu file thủ công) |    **≤ 3.0 phút**    | Log thời gian đóng ticket trên hệ thống Helpdesk     | Trưởng nhóm Vận hành       | Mở phiên rà soát điểm nghẽn quy trình (phút thứ mấy nhân viên bị kẹt); cập nhật lại cẩm nang tra cứu và template câu hỏi. |
| **Tỷ lệ tra cứu thành công không cần hỏi lại đồng nghiệp** |         Tầng 2: Hành vi         | **Workflow-level** |                      22%                      |       **≥ 80%**       | Khảo sát micro-feedback 1 chạm sau mỗi lượt tra cứu | Quản lý Quy trình Vận hành | Phỏng vấn nhanh các ca phải hỏi lại người; nếu thiếu văn bản thì giao Data Owner cập nhật trong vòng 24h.                        |
| **Tổng số giờ làm việc tiết kiệm được của phòng**          |        Tầng 5: Giá trị        | **Business Value** |                 0 giờ/tháng                 | **≥ 120 giờ/tháng** | Báo cáo phân tích hiệu suất lao động hàng tháng  | Trưởng phòng Vận hành      | Đánh giá lại mức độ hấp thụ (*Absorption*); xem xét thu hẹp hoặc tái cấu trúc quy trình nếu không mang lại ROI.             |

---

## 6. Quyết định & Thay đổi so với bản v1

- **Quyết định cuối cùng:**  SỬA (PIVOT / FIX READINESS & GOVERNANCE)*Lý do:* Không tiếp tục mở rộng rollout toàn công ty khi mức sẵn sàng về dữ liệu và trích nguồn chưa đạt; nhưng không dừng dự án vì bài toán giảm từ 8.5 phút xuống 3.0 phút mang lại giá trị rất lớn (tiết kiệm hơn 120 giờ công/tháng). Dự án tập trung sửa triệt để tính minh bạch của dữ liệu trong 30 ngày tới.
- **Hai thay đổi cốt lõi so với bản v1 (sau phản biện chéo):**
  1. *Thay đổi 1 (Về chỉ số):* **Loại bỏ hoàn toàn chỉ số đo lường bề nổi/activity** *"Số lượng câu hỏi AI gửi lên hệ thống"* ở bản v1; thay thế bằng chỉ số chất lượng & độ tin cậy cốt lõi: *"Tỷ lệ câu trả lời có trích dẫn nguồn và số điều khoản chính xác ≥ 95%"*.
  2. *Thay đổi 2 (Về cơ chế kiểm soát & vận hành):* Bổ sung vai trò chính thức **Data Owner** phụ trách duyệt vòng đời tài liệu nội bộ và thiết lập **Quy tắc xử lý khi chỉ số xấu (SLA Escalation)** kèm cơ chế chuyển giao người khi AI không tự tin, giúp giải quyết triệt để điểm nghẽn *Desire* của nhân viên.
