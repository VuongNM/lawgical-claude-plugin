# Lawgical for Claude

Tra cứu pháp luật Việt Nam ngay trong Claude — có trích dẫn đến từng **Điều**,
**Khoản**, lấy từ hơn 150.000 văn bản pháp luật.

Vietnamese legal research inside Claude, with citations down to the exact
article and clause, drawn from 150,000+ legal documents.

## Cài đặt / Install

```
/plugin marketplace add VuongNM/lawgical-claude-plugin
/plugin install lawgical@lawgical
```

Lần đầu gọi công cụ, Claude sẽ mở trình duyệt để bạn đăng nhập Lawgical. Chưa có
tài khoản? Đăng ký miễn phí ngay ở bước đó, hoặc tại
[lawgical.vn/register](https://lawgical.vn/register).

## Có gì trong plugin / What's inside

**Kết nối MCP** tới `https://legal.lawgical.vn/mcp`, cung cấp sáu công cụ tra cứu:

| Công cụ | Việc nó làm |
| --- | --- |
| `search_legal_docs` | Tìm văn bản theo từ khóa |
| `get_document` | Đọc toàn văn một văn bản |
| `get_summary` | Xem mục lục Chương/Mục/Điều |
| `check_compliance` | Lấy trích đoạn liên quan tới một câu hỏi tuân thủ |
| `get_laws` | Duyệt danh mục Luật |
| `get_account_status` | Xem gói và hạn mức còn lại |

**Năm skill** hướng dẫn Claude dùng kho dữ liệu cho đúng:

- `tra-cuu-phap-luat` — quy trình kiểm chứng trước khi trích dẫn: đúng văn bản,
  đủ nội dung, còn hiệu lực. Đây là skill nền, các skill khác đều dựa vào.
- `soan-hop-dong` — soạn hợp đồng tiếng Việt, tra cứu nội dung bắt buộc và mức
  trần luật định trước khi viết.
- `phan-tich-hop-dong` — rà soát hợp đồng có sẵn, tìm điều khoản bất lợi hoặc
  trái luật.
- `doi-chieu-tuan-thu` — đối chiếu quy trình nội bộ với một văn bản pháp luật,
  tạo checklist tuân thủ theo mức rủi ro.
- `trinh-bay-va-dinh-dang` — định dạng báo cáo Word xuất ra từ kết quả tra cứu.

Cộng một skill `setup` để xử lý lỗi kết nối và hạn mức.

## Hạn mức / Quota

Miễn phí 20 lượt tra cứu mỗi ngày, đặt lại lúc 00:00 giờ Việt Nam. Gói trả phí
không giới hạn. Tra cứu không ra kết quả không bị tính lượt.

## Nguồn dữ liệu / Data source

Văn bản pháp luật lấy từ các cổng thông tin chính thức của nhà nước (Bộ Tư pháp).
Lawgical không sở hữu văn bản gốc.

## Miễn trừ trách nhiệm / Disclaimer

Lawgical là công cụ **hỗ trợ tra cứu**, không phải dịch vụ tư vấn pháp lý. Nội
dung do AI tạo ra có thể chứa sai sót hoặc chưa cập nhật kịp thời điểm hiệu lực
của văn bản. Luôn đối chiếu với văn bản gốc và tham vấn luật sư có chứng chỉ hành
nghề trước khi ra quyết định pháp lý.

## Liên kết / Links

- Trang chủ — <https://lawgical.vn>
- Hướng dẫn cài đặt mọi nền tảng — <https://lawgical.vn/cai-dat>
- Hỗ trợ — <https://lawgical.vn/support>
- Quyền riêng tư — <https://lawgical.vn/privacy>
- Điều khoản — <https://lawgical.vn/terms>

## Bản quyền / Licence

Copyright (c) 2026 Vương Minh Nguyễn. All rights reserved. Xem [LICENSE](LICENSE).
