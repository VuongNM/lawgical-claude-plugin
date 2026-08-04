---
name: setup
description: Hướng dẫn kết nối và khắc phục sự cố plugin Lawgical — dùng khi người dùng vừa cài plugin, khi kết nối MCP thất bại, khi bị lỗi xác thực (unauthorized/401), hoặc khi hết hạn mức tra cứu trong ngày. Guides connecting the Lawgical MCP server and troubleshoots authorization and quota errors.
---

# Kết nối Lawgical

Plugin này kết nối tới máy chủ MCP của Lawgical tại `https://legal.lawgical.vn/mcp`
để tra cứu hơn 150.000 văn bản pháp luật Việt Nam. Máy chủ yêu cầu đăng nhập —
mọi lượt tra cứu đều gắn với một tài khoản Lawgical.

## Kết nối lần đầu

Khi người dùng gọi một công cụ Lawgical lần đầu, Claude sẽ mở trình duyệt để xác
thực. Các bước người dùng sẽ thấy:

1. Trình duyệt chuyển sang trang đăng nhập Lawgical.
2. Đăng nhập bằng email đã đăng ký — hoặc **đăng ký ngay tại đó** nếu chưa có
   tài khoản (miễn phí, không cần thẻ).
3. Bấm **Authorize** để cấp quyền.
4. Trình duyệt tự quay lại; công cụ chạy tiếp.

Nếu người dùng chưa có tài khoản, hướng họ tới <https://lawgical.vn/register>.
Hướng dẫn đầy đủ cho mọi nền tảng: <https://lawgical.vn/cai-dat>.

## Hạn mức

- **Miễn phí** — 20 lượt tra cứu mỗi ngày, đặt lại lúc 00:00 giờ Việt Nam.
- **Trả phí** — không giới hạn.

Tra cứu không ra kết quả **không bị tính lượt**. Chỉ những lần thực sự trả về nội
dung mới tính, nên cứ thử tra khi chưa chắc.

Gọi công cụ `get_account_status` để xem gói hiện tại và số lượt còn lại. Nâng cấp
tại <https://lawgical.vn/dashboard>.

## Khắc phục sự cố

**Lỗi xác thực / 401 / "unauthorized"**
Phiên đăng nhập đã hết hạn hoặc chưa từng hoàn tất. Bảo người dùng ngắt kết nối
rồi kết nối lại plugin để chạy lại luồng đăng nhập ở trên. Nếu vẫn lỗi, kiểm tra
xem họ có đăng nhập đúng tài khoản đã đăng ký không.

**"Incompatible auth server" khi kết nối**
Cấu hình trong `.mcp.json` đã khai báo sẵn `oauth.clientId` cho trường hợp này.
Nếu vẫn gặp lỗi, khả năng cao là bản plugin đã cũ — cập nhật plugin rồi thử lại.

**Đã hết hạn mức trong ngày**
`get_account_status` sẽ cho biết chính xác còn bao nhiêu lượt và khi nào đặt lại.
Hạn mức đặt lại lúc nửa đêm giờ Việt Nam, hoặc nâng cấp để dùng không giới hạn.

**Không thấy công cụ Lawgical nào**
Kiểm tra plugin đã được bật, và máy chủ MCP đã kết nối. Máy chủ cung cấp sáu công
cụ tra cứu: `search_legal_docs`, `get_document`, `get_summary`, `check_compliance`,
`get_laws`, `get_account_status`.

Cần hỗ trợ thêm: <https://lawgical.vn/support>
