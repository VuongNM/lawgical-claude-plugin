---
name: soan-hop-dong
description: Soạn hợp đồng tiếng Việt đúng chuẩn pháp lý — lao động, mua bán, dịch vụ, thuê nhà, hợp tác kinh doanh. Tự tra cứu nội dung bắt buộc và mức trần luật định qua Lawgical trước khi viết, không đoán mò. Dùng khi được yêu cầu "soạn hợp đồng", "viết hợp đồng", "làm hợp đồng cho tôi".
---

# Soạn hợp đồng

Dùng khi người dùng yêu cầu soạn một hợp đồng mới (lao động, mua bán, dịch vụ, thuê nhà, hợp tác kinh doanh, v.v.).

## Quy trình

1. **Xác định loại hợp đồng, các bên, và luật điều chỉnh.** Một giao dịch dân sự chỉ có hiệu lực khi đủ 4 điều kiện của Bộ luật Dân sự 2015, Điều 117: (i) các bên có năng lực pháp luật/hành vi dân sự phù hợp, (ii) hoàn toàn tự nguyện, (iii) mục đích và nội dung không vi phạm điều cấm của luật, không trái đạo đức xã hội, (iv) đúng hình thức luật yêu cầu (nếu có). Hợp đồng thương mại (giữa các thương nhân, có mục đích sinh lợi) còn chịu thêm Luật Thương mại 2005 song song với BLDS — quan trọng vì mức trần phạt vi phạm khác nhau giữa hai loại (xem Bước 4).

2. **Tra cứu qua Lawgical trước khi khẳng định bất kỳ nội dung bắt buộc nào:**
   - `search_legal_docs` để tìm luật gốc áp dụng (ví dụ "hợp đồng lao động", "hợp đồng thuê nhà").
   - `get_summary` để xem mục lục Chương/Điều trước khi đọc toàn văn.
   - `get_document` hoặc hỏi thẳng một Điều cụ thể để lấy nguyên văn — không suy đoán số Điều/Khoản, kể cả với các Điều quen thuộc, vì luật có thể đã được sửa đổi.

3. **Checklist nội dung bắt buộc theo loại hợp đồng** (khung tham khảo — luôn xác nhận lại qua Lawgical vì đây chỉ là điểm khởi đầu, không phải danh sách đầy đủ):

   | Loại hợp đồng | Nội dung bắt buộc cần có | Luật gốc |
   |---|---|---|
   | Lao động | Thông tin hai bên (tên/địa chỉ/người đại diện NSDLĐ; họ tên/ngày sinh/CCCD của NLĐ); công việc & địa điểm; thời hạn; lương/hình thức/kỳ trả lương & phụ cấp; chế độ nâng bậc lương; thời giờ làm việc-nghỉ ngơi; trang bị bảo hộ; BHXH/BHYT/BHTN; đào tạo nâng cao trình độ | Bộ luật Lao động 2019, Điều 21 |
   | Mua bán | Đối tượng & chất lượng, giá & phương thức thanh toán, thời hạn/địa điểm/phương thức giao, trách nhiệm vi phạm | Bộ luật Dân sự 2015, từ Điều 430 |
   | Dịch vụ | Công việc, chất lượng, thời hạn hoàn thành, giá dịch vụ, phương thức thanh toán | Bộ luật Dân sự 2015, từ Điều 513 |
   | Thuê nhà/mặt bằng | Đối tượng thuê, giá thuê, thời hạn, quyền/nghĩa vụ sửa chữa, điều kiện đơn phương chấm dứt | BLDS 2015 từ Điều 472; Luật Nhà ở 2023 nếu là nhà ở |
   | Hợp tác kinh doanh | Mục đích hợp tác, phương thức góp vốn, phân chia lợi nhuận/lỗ, quyền quản lý, điều kiện rút vốn | BLDS 2015 từ Điều 504 |

4. **Rà soát các bẫy hiệu lực thường gặp trước khi soạn:**
   - **Thẩm quyền ký:** nếu một bên là pháp nhân, người ký phải là đại diện theo pháp luật (ghi trong ĐKKD) hoặc có giấy ủy quyền hợp lệ — thiếu điều này hợp đồng có thể vô hiệu hoặc không ràng buộc pháp nhân.
   - **Hình thức bắt buộc:** chuyển nhượng/tặng cho quyền sử dụng đất (Luật Đất đai 2024, Điều 27) và mua bán/tặng cho nhà ở (Luật Nhà ở 2023, Điều 164) chỉ có hiệu lực giữa các bên khi công chứng/chứng thực — với đất đai, còn cần đăng ký biến động tại cơ quan đất đai mới có hiệu lực với bên thứ ba/Nhà nước. Hợp đồng thuê (kể cả thuê nhà ở) thường KHÔNG bắt buộc công chứng. Luôn tra cứu Lawgical để xác nhận giao dịch cụ thể có thuộc diện bắt buộc công chứng không, vì có ngoại lệ (ví dụ tổ chức kinh doanh bất động sản, nhà ở xã hội).
   - **Mức phạt vi phạm:** hợp đồng thương mại bị giới hạn mức phạt tối đa 8% giá trị phần nghĩa vụ bị vi phạm, trừ dịch vụ giám định (Luật Thương mại 2005, Điều 301 và 266); hợp đồng dân sự thuần túy các bên được tự do thỏa thuận mức phạt, trừ khi luật chuyên ngành khác có quy định riêng (BLDS 2015, Điều 418). Đặt sai loại hoặc bỏ qua ngoại lệ có thể khiến điều khoản phạt bị vô hiệu một phần.

5. **Soạn hợp đồng đầy đủ:** các bên, đối tượng hợp đồng, quyền và nghĩa vụ, giá trị/thanh toán, thời hạn, chấm dứt/vi phạm, giải quyết tranh chấp, điều khoản chung — dựa trên checklist Bước 3 và bẫy Bước 4.

6. **Trích dẫn rõ nguồn:** với mỗi điều khoản lấy trực tiếp từ luật, ghi kèm Điều — Khoản để người dùng tự đối chiếu. Nếu người dùng yêu cầu, xuất thành file Word hoặc Google Docs.

## Lưu ý

- Không bịa điều khoản luật không có thật — checklist ở Bước 3-4 chỉ là khung tham khảo ban đầu, luôn tra cứu qua Lawgical để xác nhận số Điều/Khoản và tình trạng hiệu lực hiện hành trước khi khẳng định với người dùng.
- Ghi rõ đây là bản dự thảo tham khảo; khuyến nghị luật sư rà soát trước khi các bên ký kết, đặc biệt với hợp đồng giá trị lớn hoặc có yếu tố nước ngoài.
