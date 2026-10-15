# Lawgical for Claude

Tra cứu pháp luật Việt Nam ngay trong Claude, có trích dẫn đến từng **Điều**,
**Khoản**, lấy từ hơn 150.000 văn bản pháp luật.

Vietnamese legal research inside Claude, with citations down to the exact
article and clause, drawn from 150,000+ legal documents.

## Dùng Claude.ai, Claude Desktop hoặc app điện thoại

Bạn không cần cài plugin. Lawgical có sẵn trong thư mục connector của Claude:

1. Mở [Lawgical trong thư mục Claude](https://claude.ai/directory/lawgical) rồi
   bấm **Add** (chưa đăng nhập Claude thì nút là **Sign in to add**).
2. Đăng nhập Lawgical và bấm **Authorize**. Chưa có tài khoản thì đăng ký miễn
   phí ngay ở bước này, không cần thẻ.
3. Hỏi Claude một câu, ví dụ: *"Công ty nợ lương 2 tháng, tôi nghỉ ngay được
   không?"*

Cài một lần trên web là dùng được cả trên app điện thoại. Hướng dẫn có video:
[lawgical.vn/cai-dat](https://lawgical.vn/cai-dat).

**Using Claude.ai, Claude Desktop or the mobile app?** No plugin needed. Open
[Lawgical in the Claude directory](https://claude.ai/directory/lawgical), click
**Add** (or **Sign in to add**), then sign in to Lawgical and click **Authorize**.

## Dùng Claude Code / Claude Code

Plugin này dành cho Claude Code. Ngoài connector, nó có thêm các skill soạn hợp
đồng, rà soát hợp đồng và đối chiếu tuân thủ (xem bên dưới).

```
/plugin marketplace add VuongNM/lawgical-claude-plugin
/plugin install lawgical@lawgical
```

Lần đầu gọi công cụ, Claude sẽ mở trình duyệt để bạn đăng nhập Lawgical. Chưa có
tài khoản? Đăng ký miễn phí ngay ở bước đó, hoặc tại
[lawgical.vn/register](https://lawgical.vn/register).

## Thử ngay, không cần cài / Try it without installing

- [Tính thuế thu nhập cá nhân 2026](https://lawgical.vn/tinh/thue-thu-nhap-ca-nhan)
- [Tính bảo hiểm xã hội một lần](https://lawgical.vn/tinh/bao-hiem-xa-hoi-mot-lan)
- [Hộ kinh doanh hay công ty? So sánh thuế theo doanh thu](https://lawgical.vn/tinh/thue-ho-kinh-doanh-hay-cong-ty)
- [Tra cứu mã số thuế](https://lawgical.vn/tra-cuu/ma-so-thue)
- [Tra cứu văn bản pháp luật](https://lawgical.vn/tra-cuu/van-ban)

Câu hỏi thật, trả lời có trích dẫn ([xem hơn 260 ví dụ](https://lawgical.vn/vi-du)):

- [Xây nhà không phép, sai phép bị phạt bao nhiêu, có bị tháo dỡ không?](https://lawgical.vn/vi-du/xay-nha-khong-phep-sai-phep-bi-phat-bao-nhieu-co-bi-thao-do-khong-luat-xay-dung-2025)
- [Ly hôn rồi, người trực tiếp nuôi con có được tự ý đưa con ra nước ngoài không?](https://lawgical.vn/vi-du/ly-hon-roi-nguoi-truc-tiep-nuoi-con-co-duoc-tu-y-dua-con-ra-nuoc-ngoai-khong)
- [Thuế thu nhập doanh nghiệp cho SME hiện nay áp dụng mức nào?](https://lawgical.vn/vi-du/thue-thu-nhap-doanh-nghiep-sme-hien-nay-ap-dung-muc-nao-nguong-doanh-thu-bao-nhieu)
- [Ở nhà ông bà 60 năm, giờ muốn đứng tên một mình](https://lawgical.vn/vi-du/thua-ke-het-thoi-hieu-30-nam)
- [Doanh nghiệp nhỏ được miễn đánh giá tác động dữ liệu](https://lawgical.vn/vi-du/luat-bao-ve-du-lieu-ca-nhan-2025)

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
