---
name: trinh-bay-va-dinh-dang
description: Khi xuất báo cáo dạng file Word (.docx) từ kết quả Lawgical — thêm một dải banner gradient thương hiệu ở đầu tài liệu; nếu tài liệu có bảng, tô gradient đó CHỈ ở hàng tiêu đề bảng, không tô phần thân bảng. Dùng khi được yêu cầu xuất file Word hoặc báo cáo có bảng từ nội dung pháp luật đã tra cứu qua Lawgical.
---

# Trình bày & định dạng — dải gradient tiêu đề

## Quy tắc

1. **File Word (.docx)**: thêm một dải banner ở đầu tài liệu dùng gradient thương hiệu (xem hex bên dưới).
2. **Bảng**: nếu tài liệu có bảng, chỉ **hàng tiêu đề (header row)** dùng gradient — thân bảng (các hàng dữ liệu) giữ nguyên nền trắng/plain, không tô gradient.

## Gradient thương hiệu

3 điểm dừng, lấy từ gradient hero của lawgical.vn (`from-[#1a2fd8] via-[#7b2bd4] to-[#e8309a]`):

| Vị trí | Hex |
|---|---|
| 0% | `#1A2FD8` (chàm) |
| 50% | `#7B2BD4` (tím) |
| 100% | `#E8309A` (hồng cánh sen) |

## Cách dựng

OOXML (`.docx`) không hỗ trợ gradient nhiều điểm dừng trong tô nền (`<w:shd>` chỉ nhận một màu đặc), nên cả hai chỗ trên đều cần xấp xỉ:

- **Dải banner đầu trang**: dựng một ảnh PNG gradient ngang nội suy tuyến tính qua 3 điểm dừng trên, chèn bằng `ImageRun` (docx-js) hoặc tương đương — không tô nền đoạn văn bằng shading.
- **Hàng tiêu đề bảng**: với N cột, màu ô thứ *i* (0-based, i từ 0 đến N-1) = màu gradient nội suy tại vị trí `i / (N-1)`, tạo hiệu ứng chuyển màu trái sang phải qua các ô. Tô bằng `ShadingType.CLEAR` (không dùng `SOLID`, sẽ ra nền đen). Chữ trong hàng tiêu đề dùng màu trắng để đủ tương phản trên cả 3 điểm dừng màu.
