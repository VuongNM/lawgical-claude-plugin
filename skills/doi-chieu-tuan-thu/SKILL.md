---
name: doi-chieu-tuan-thu
description: Đối chiếu quy trình/chính sách nội bộ công ty với một văn bản pháp luật cụ thể (ví dụ Luật Bảo vệ dữ liệu cá nhân, Bộ luật Lao động), tạo checklist tuân thủ có mức độ rủi ro và việc cần làm — dùng Lawgical để lấy đúng nội dung luật, kể cả tool check_compliance chuyên cho việc này. Dùng khi được hỏi "công ty tôi có tuân thủ luật X không", "làm checklist compliance".
---

# Đối chiếu tuân thủ

Dùng khi người dùng muốn kiểm tra công ty hoặc quy trình của họ có tuân thủ một luật/nghị định cụ thể không (ví dụ Luật Bảo vệ dữ liệu cá nhân, Bộ luật Lao động).

## Quy trình

1. **Xác định văn bản pháp luật cần đối chiếu và lấy đúng nội dung qua Lawgical:**
   - `check_compliance` — cách nhanh nhất khi câu hỏi đã ở dạng tình huống cụ thể (ví dụ "công ty tôi lưu dữ liệu khách hàng ở nước ngoài có vi phạm không") — tool trả về thẳng các văn bản/đoạn liên quan.
   - Nếu người dùng chỉ định rõ một luật/nghị định, dùng `get_laws` (liệt kê Luật hiện hành theo từ khóa) hoặc `get_summary` (mục lục Chương/Điều) trước, rồi `get_document` để đọc toàn văn Điều liên quan.

2. **Liệt kê từng nghĩa vụ/yêu cầu bắt buộc trong văn bản đó, kèm Điều — Khoản** — không suy đoán, chỉ liệt kê nghĩa vụ đã xác nhận có trong văn bản vừa tra cứu.

3. **Với mỗi nghĩa vụ, đánh giá dựa trên thông tin người dùng cung cấp (hỏi thêm nếu chưa đủ):**
   - Trạng thái: Đã tuân thủ / Chưa tuân thủ / Không áp dụng.
   - Mức độ ưu tiên: dựa trên chế tài nêu trong luật nếu có (ví dụ mức phạt hành chính, biện pháp khắc phục) — tra cứu qua Lawgical thay vì đoán mức phạt.
   - Bằng chứng cần có để chứng minh đã tuân thủ (ví dụ: hồ sơ đánh giá tác động, biên bản, chính sách nội bộ đã ban hành).

4. **Tổng hợp thành checklist:** Yêu cầu pháp luật | Điều — Khoản | Trạng thái | Mức ưu tiên | Bằng chứng/Việc cần làm | Hạn chót (nếu luật quy định lộ trình). Nếu người dùng yêu cầu, xuất ra Word, Google Docs, hoặc Google Sheets để theo dõi.

5. **Nếu người dùng cung cấp tài liệu chính sách/quy trình nội bộ**, đối chiếu trực tiếp từng điều khoản trong tài liệu đó với từng nghĩa vụ đã liệt kê ở Bước 2, thay vì chỉ hỏi miệng — cho kết quả chính xác hơn.

## Lưu ý

- Luôn lấy đúng nội dung từ Lawgical trước khi liệt kê nghĩa vụ — không suy đoán, kể cả với các luật quen thuộc.
- Ghi rõ ngày hiệu lực và tình trạng (`tinh_trang`) của văn bản đối chiếu — nghĩa vụ có thể đã thay đổi nếu văn bản được sửa đổi hoặc có lộ trình áp dụng riêng (ví dụ miễn trừ theo quy mô doanh nghiệp, theo thời gian).
