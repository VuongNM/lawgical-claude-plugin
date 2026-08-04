---
name: phan-tich-hop-dong
description: Phân tích hợp đồng có sẵn để phát hiện điều khoản bất lợi, trái luật, hoặc thuộc nhóm "red flag" thường gặp trong thực tiễn hợp đồng Việt Nam — đối chiếu qua Lawgical trước khi kết luận. Dùng khi người dùng dán/tải một hợp đồng và hỏi "rà soát", "phân tích", "có rủi ro gì không".
---

# Phân tích hợp đồng

Dùng khi người dùng đưa vào một hợp đồng có sẵn (dán văn bản hoặc tải file) và muốn rà soát rủi ro.

## Quy trình

1. **Đọc toàn bộ hợp đồng, liệt kê từng điều khoản chính** — đặc biệt các nhóm điều khoản nhạy cảm: chấm dứt hợp đồng, phạt vi phạm/bồi thường, bảo mật/không cạnh tranh, miễn trừ trách nhiệm, giải quyết tranh chấp, gia hạn.

2. **Quét qua thư viện "red flag" thường gặp trong thực tiễn hợp đồng Việt Nam** (khung tham khảo dựa trên kinh nghiệm thực tiễn — vẫn cần đối chiếu luật cụ thể ở Bước 3 trước khi kết luận trái luật):

   | Dấu hiệu | Vì sao đáng chú ý |
   |---|---|
   | Quyền đơn phương chấm dứt bất cân xứng (chỉ một bên có quyền, hoặc thời hạn báo trước chênh lệch lớn) | Bất lợi rõ cho bên yếu thế hơn, dù không nhất thiết trái luật |
   | Mức phạt vi phạm vượt 8% giá trị nghĩa vụ bị vi phạm, trong hợp đồng có tính chất thương mại | Vượt trần Luật Thương mại 2005, Điều 301 (trừ dịch vụ giám định theo Điều 266) — phần vượt có thể bị tuyên vô hiệu. Với hợp đồng dân sự thuần túy, mức phạt được tự do thỏa thuận theo BLDS Điều 418, trừ khi luật chuyên ngành khác giới hạn — cần xác định đúng loại hợp đồng trước khi kết luận |
   | Miễn trừ trách nhiệm cho cả lỗi cố ý / vi phạm nghiêm trọng | Đi ngược nguyên tắc thiện chí, trung thực (BLDS 2015, Điều 3 khoản 3) và thường bị tòa/trọng tài xem xét không công nhận hiệu lực — nhưng cơ sở vô hiệu hóa cụ thể (điều luật viện dẫn) cần tra cứu theo từng trường hợp qua Lawgical, không suy diễn sẵn từ một điều luật duy nhất |
   | Tự động gia hạn không có cơ chế thông báo trước hợp lý | Dễ khiến một bên bị ràng buộc ngoài ý muốn |
   | Không cạnh tranh (non-compete) sau khi nghỉ việc, phạm vi/thời hạn quá rộng | Bộ luật Lao động 2019 không có điều khoản riêng quy định hiệu lực của thỏa thuận này — đây là vùng pháp lý còn tranh cãi ở Việt Nam, cần khuyến nghị thận trọng thay vì kết luận chắc chắn hợp lệ hay vô hiệu |
   | Chọn tòa án/trọng tài ở nơi bất tiện, hoặc luật áp dụng không phù hợp bản chất giao dịch trong nước | Có thể gây bất lợi thực tế khi tranh chấp xảy ra dù về hình thức vẫn hợp pháp |
   | Người ký không đúng thẩm quyền / thiếu con dấu pháp nhân theo điều lệ | Rủi ro hợp đồng không ràng buộc bên đó |

3. **Với mỗi điều khoản nghi ngờ, đối chiếu qua Lawgical trước khi kết luận:**
   - `check_compliance` — hỏi thẳng tình huống (ví dụ "hợp đồng thương mại phạt vi phạm 15% có hợp lệ không") để lấy nhanh văn bản liên quan.
   - `search_legal_docs` / `get_summary` / `get_document` khi cần đọc đúng nguyên văn Điều — Khoản để trích dẫn chính xác.

4. **Đánh dấu từng điều khoản:**
   - 🔴 Vi phạm hoặc trái luật hiện hành (kèm trích dẫn Điều — Khoản)
   - 🟡 Bất lợi cho bên yêu cầu phân tích nhưng không trái luật
   - 🟢 Phù hợp, không có rủi ro rõ ràng

5. **Tổng hợp thành bảng:** Điều khoản | Rủi ro | Trích dẫn luật | Đề xuất chỉnh sửa. Nếu người dùng yêu cầu, xuất ra Word, Google Docs, hoặc Google Slides để trình bày.

## Lưu ý

- Thư viện "red flag" ở Bước 2 là kinh nghiệm thực tiễn phổ biến, không phải trích dẫn luật đầy đủ — không tự suy đoán điều luật bị vi phạm, luôn tra cứu qua Lawgical trước khi gắn nhãn 🔴.
- Đây là công cụ hỗ trợ rà soát nhanh, không thay thế tư vấn pháp lý chính thức cho các hợp đồng giá trị lớn, phức tạp, hoặc có yếu tố nước ngoài.
