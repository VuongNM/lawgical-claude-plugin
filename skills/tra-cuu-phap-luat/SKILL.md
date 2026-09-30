---
name: tra-cuu-phap-luat
description: >-
  Tra cứu và kiểm chứng văn bản pháp luật Việt Nam qua Lawgical trước khi trích
  dẫn — xác minh đúng văn bản, đủ nội dung, còn hiệu lực, và không nhầm văn bản
  dẫn chiếu. Dùng cho MỌI câu hỏi về pháp luật Việt Nam: "tra cứu luật", một
  Điều/Khoản cụ thể, "còn hiệu lực không", so sánh hai văn bản, hoặc "Lawgical
  có văn bản X không". Đây là skill nền — các skill soạn/phân tích hợp đồng và
  đối chiếu tuân thủ đều dựa vào quy trình kiểm chứng ở đây.
---

# Tra cứu & kiểm chứng văn bản pháp luật

Lawgical lập chỉ mục hơn 150.000 văn bản pháp luật Việt Nam từ các nguồn chính thức của
nhà nước. Skill này nói về cách dùng **cho đúng**: kho dữ liệu có thể trả về kết quả
nghe rất thuyết phục nhưng sai văn bản, thiếu nội dung, hoặc đã hết hiệu lực. Quy trình
kiểm chứng ở dưới là thứ ngăn điều đó.

## Nạp công cụ

Công cụ Lawgical có thể đang ở dạng deferred (chỉ hiện tên, chưa có schema). Phải nạp
trước khi gọi. **Không sao chép server id từ bất kỳ tài liệu nào** — mỗi người dùng có
một id riêng. Hãy khớp theo **phần đuôi** của tên công cụ:

1. Tìm trong danh sách deferred những tên kết thúc bằng `__search_legal_docs`,
   `__get_document`, `__get_laws`, …
2. Nạp bằng đúng tên đầy đủ như đang được liệt kê:
   `ToolSearch({query: "select:<tên_đầy_đủ_1>,<tên_đầy_đủ_2>,…", max_results: 5})`

Nếu không thấy công cụ nào, connector Lawgical chưa được kết nối — xem phần Xử lý sự cố.

## Các công cụ và chi phí hạn mức

Hạn mức tính **1 lượt cho mỗi lần gọi thành công**. Gói Miễn phí: **20 lượt/ngày**. Gói
Trả phí: **không giới hạn**. Hạn mức đặt lại vào **00:00 giờ Việt Nam (ICT)**.

| Công cụ | Tính lượt? | Dùng để |
|---|---|---|
| `get_account_status()` | **Không — luôn miễn phí** | Xem gói, số lượt đã dùng/còn lại hôm nay, giờ đặt lại hạn mức, ngày gia hạn/hết hạn; với thành viên văn phòng: admin có cần cấp account hay gia hạn gói không |
| `search_legal_docs(keywords)` | 1 lượt | **Bước đầu tiên.** Tìm theo từ khóa trên toàn kho |
| `check_compliance(question)` | 1 lượt | Cùng cơ chế tìm, nhưng nhận đầu vào dạng câu hỏi. Trả về trích đoạn thô để **bạn** tự phân tích — không trả về kết luận |
| `get_laws(tinh_trang, keyword, limit, offset)` | 1 lượt | Duyệt riêng **Luật** (do Quốc hội ban hành), không gồm Nghị định/Thông tư hướng dẫn |
| `get_summary(query)` | 1 lượt | Mục lục (Chương/Mục/Điều). **Dùng trước `get_document` với luật dài** để tìm đúng Điều mà không phải tải 60.000 ký tự |
| `get_document(query)` | 1 lượt | Toàn văn theo tên, doc id, hoặc số ký hiệu (ví dụ `"20/2023/QH15"`). **Tự tải lại từ nguồn gốc** khi bản trong kho bị thiếu hoặc chỉ có metadata — xem phần cuối |

**Tìm không ra thì không bị tính lượt.** Chỉ những lần thực sự trả về nội dung (HIT hoặc
PARTIAL) mới tính; lần gọi bị lỗi cũng miễn phí. Vì vậy **cứ thử tra cứu khi chưa chắc** —
điều nên tránh là tiêu lượt để đọc lại văn bản đã có sẵn trong ngữ cảnh.

Vài thói quen tiết kiệm:
- Gọi `get_account_status()` trước nếu người dùng ở gói Miễn phí và việc cần nhiều bước —
  không tốn lượt mà biết được còn bao nhiêu.
- `get_summary` rồi đọc đúng chỗ, thay vì `get_document` cả một luật 60.000 ký tự.
- Nếu kết quả đã được lưu ra file (do quá dài), **đọc file đó**, đừng gọi lại công cụ.

## Quy trình

1. **`search_legal_docs`** với từ khóa tiếng Việt bao quát khái niệm, không chỉ một từ
   trơ. Nên kèm cách diễn đạt của Điều/Chương, ví dụ
   `"quyền hạn chế xử lý dữ liệu cá nhân Điều 10"`. Tiếng Anh vẫn chạy, nhưng từ khóa
   tiếng Việt khớp kho dữ liệu tốt hơn nhiều.
2. **Đọc tiêu đề các kết quả trước khi chọn.** Một kết quả khớp số ký hiệu thường **không
   phải** văn bản đó, mà là văn bản *dẫn chiếu* tới nó (xem bước kiểm chứng 4).
3. **`get_summary`** nếu là luật dài, để định vị đúng Điều.
4. **`get_document`** lấy toàn văn. Nếu kết quả vượt giới hạn, nó được lưu ra file — đọc
   hoặc grep file đó thay vì gọi lại.
5. **Chạy quy trình kiểm chứng bên dưới** — trước khi đọc nội dung, không phải sau.
6. Đọc đúng Điều/Khoản và trả lời từ chính văn bản.
7. **Trích dẫn chính xác**: Điều / Khoản / Điểm, kèm số ký hiệu và Tình trạng hiệu lực.
   Không bao giờ diễn giải một nghĩa vụ pháp lý mà không chỉ ra điều luật.

## Quy trình kiểm chứng — bắt buộc trước khi trích dẫn

Kho dữ liệu này sai theo bốn kiểu khác nhau. Mỗi bước dưới đây chỉ mất vài giây và không
tốn thêm lượt nào (chỉ đọc lại thứ đã có). **Làm cả bốn. Đừng bỏ bước nào vì văn bản
"trông đúng rồi" — trông đúng chính là kiểu lỗi ở đây.**

**1. Đúng văn bản — có phải văn bản tôi yêu cầu?**
`get_document` đôi khi trả về một văn bản **không liên quan** thay vì báo không tìm thấy.
Hãy đọc dòng `Số ký hiệu` trong bảng thông tin và xác nhận nó khớp với thứ đã yêu cầu.
Chỉ riêng bước này là khác biệt giữa một câu trả lời đúng và một câu trả lời sai nhưng
được trích dẫn đầy tự tin.

**2. Đủ nội dung — đã có toàn văn chưa?**
Hai kiểu lỗi: chỉ có metadata (đúng bảng thông tin, vài trăm ký tự, không có điều nào), và
bị cắt giữa văn bản. Hãy kiểm tra số hiệu Điều có liên tục, và văn bản có kết thúc đúng
chỗ — phần ký của Quốc hội (`Luật này được Quốc hội … thông qua ngày …` rồi tới dòng
CHỦ TỊCH QUỐC HỘI). Nếu dãy Điều bị nhảy số, hoặc kết thúc giữa câu, **đừng trích dẫn**.

Lưu ý về khả năng tự chữa: nếu bản trong kho **rỗng hoặc chỉ có metadata**, gọi
`get_document` **theo số ký hiệu** sẽ khiến server tự tải lại bản đầy đủ từ nguồn gốc rồi mới
trả lời — nên trường hợp này thường tự khỏi ở lần gọi tiếp theo. Nhưng nếu văn bản **có nội
dung đáng kể mà vẫn thiếu điều ở giữa**, cơ chế tự tải lại **không** kích hoạt: hãy nói rõ
với người dùng là bản trong kho không đầy đủ, trích dẫn phần đã kiểm chứng được và đừng suy
diễn phần thiếu.

Nếu bạn chạy được code (Claude Code, Cursor, VS Code…) và văn bản đã được lưu ra file vì
quá dài, kiểm tra bằng máy thay vì đọc bằng mắt:

```bash
python3 -c "
import json, re
d = json.load(open('ĐƯỜNG_DẪN_FILE'))['result']
arts = sorted({int(m) for m in re.findall(r'Điều (\d+)\.', d)})
print('số Điều:', len(arts), '| từ', arts[0], 'đến', arts[-1])
print('thiếu:', [n for n in range(arts[0], arts[-1]+1) if n not in arts] or 'không')
print('kết thúc:', repr(d[-160:]))"
```

Danh sách `thiếu` phải rỗng, và phần `kết thúc` phải là khối ký của Quốc hội. Trên
Claude.ai hoặc ChatGPT (không chạy được code) thì kiểm tra bằng mắt: đọc số hiệu Điều
cuối cùng và cuộn xuống cuối văn bản.

**3. Còn hiệu lực — đây có còn là luật hiện hành?**
Đọc `Tình trạng hiệu lực` trên chính văn bản. Sau đó kiểm tra xem có bản hợp nhất mới hơn
không. **Văn bản hợp nhất (số ký hiệu dạng `…/VBHN-VPQH`) đã gộp mọi sửa đổi, bổ sung
sau này và là bản thể hiện luật hiện hành.** Loại này có trường tình trạng **để trống**,
nên bộ lọc mặc định của `get_laws` che nó đi hoàn toàn:

```
get_laws(keyword="giao dịch điện tử")                 → 1 kết quả  (20/2023/QH15)
get_laws(keyword="giao dịch điện tử", tinh_trang="")  → 4 kết quả, có cả
                                                         42/VBHN-VPQH (27/02/2025)
```

Trích dẫn luật gốc 2023 khi đã có bản hợp nhất 2025 là **sai về luật hiện hành**. Hãy ưu
tiên bản hợp nhất nếu có, và nói rõ đang dùng bản nào.

**Suy ra: đừng bao giờ kết luận Lawgical không có một văn bản mà chưa kiểm tra lại với
`tinh_trang=""`.** Bộ lọc mặc định là nguyên nhân phổ biến nhất của kết luận sai "không có".

**4. Nguồn dẫn — đây là văn bản đó, hay văn bản trích nó?**
Tìm theo số ký hiệu phần lớn trả về những văn bản dẫn chiếu nó ở phần `Căn cứ`. Ví dụ
thật: tìm `20/2023/QH15` trả về 8 kết quả và **không kết quả nào là Luật Giao dịch điện
tử** — toàn bộ là Quyết định của các tỉnh và quy chuẩn kỹ thuật QCVN trích dẫn luật này.
Nếu tiêu đề là văn bản địa phương hoặc quy chuẩn kỹ thuật trong khi bạn đang hỏi về một
Luật, thì bạn đang đọc phần dẫn chiếu, không phải luật.

### Dấu hiệu phải dừng lại và kiểm chứng lại

| Ý nghĩ | Thực tế |
|---|---|
| "Tìm thấy rồi — trả về một văn bản rất dài" | Độ dài không chứng minh gì. Kiểm tra `Số ký hiệu`. |
| "8 kết quả, kho dữ liệu tốt đấy" | Có thể **tất cả** chỉ là văn bản dẫn chiếu, không cái nào là văn bản cần tìm. |
| "`get_laws` không trả về gì, vậy là không có" | Bộ lọc mặc định che văn bản có tình trạng trống. Chạy lại với `tinh_trang=""`. |
| "Tình trạng ghi Còn hiệu lực, vậy đây là bản hiện hành" | Có thể đã có bản hợp nhất thay thế. Tìm `VBHN`. |
| "Nội dung trông đủ mà, dài thế còn gì" | Kiểm tra tính liên tục của Điều và phần ký cuối văn bản. |
| "Tôi tóm tắt nghĩa vụ này theo hiểu biết chung" | Phải trích nguyên văn Điều. Luật Việt Nam thay đổi nhanh, kho dữ liệu là nguồn đúng. |

## Khi văn bản thiếu hoặc chỉ có metadata

**Dấu hiệu:** `get_document` chỉ trả về bảng thông tin (Số ký hiệu / Loại văn bản / Ngày
ban hành …) mà không có điều nào, hoặc không tìm thấy gì.

1. **Gọi `get_document` với đúng số ký hiệu** (không phải tên). Đây là bước quan trọng
   nhất: khi truy vấn có dạng số ký hiệu và bản trong kho bị thiếu hoặc rỗng, server **tự
   tải lại văn bản từ nguồn gốc rồi lập chỉ mục trước khi trả lời**. Thường mất vài
   giây, nhưng có thể lâu hơn nếu nguồn phản hồi chậm.
   Cơ chế này **chỉ chạy khi truy vấn trông giống số ký hiệu** — tra bằng từ khóa chung
   chung sẽ không kích hoạt nó, vì một kết quả tìm kiếm mờ không đủ tin cậy để nhận là
   đúng văn bản.
2. Kiểm tra lại chính định danh. Số ký hiệu có nhiều dạng — thực tế có cả `40 /2026/TT-BCT`
   với một dấu cách lạc trước dấu gạch chéo. Sai một ký tự là không kích hoạt được bước 1.
3. Chạy lại các bước `get_laws` với `tinh_trang=""` để loại khả năng bị bộ lọc che.
4. Chạy lại `search_legal_docs` với một cụm từ riêng biệt trong nội dung để xác nhận đã lập
   chỉ mục, rồi kiểm chứng lại theo quy trình trên.
5. Nếu vẫn không có, **hãy nói thẳng là không có**, đừng trả lời bằng kiến thức chung. Một
   câu trả lời pháp lý sai tốn kém hơn nhiều so với việc thừa nhận thiếu dữ liệu. Kho dữ
   liệu phủ tốt văn bản trung ương; văn bản địa phương và văn bản mới ban hành là chỗ dễ
   thiếu nhất.

## Trả lời cho tốt

- **Không đưa ra ý kiến pháp lý như thể của chính mình.** Hãy thuật lại văn bản nói gì,
  trích điều luật, và nêu rõ khi nào cần luật sư có chứng chỉ.
- **Trích nguyên văn, không diễn giải, với nghĩa vụ / thời hạn / mức phạt.** Cách soạn
  luật Việt Nam rất chặt về số ngày, mức phạt và ngưỡng áp dụng; một câu diễn giải làm
  rơi chữ "làm việc" khỏi "15 ngày làm việc" là đã đổi câu trả lời.
- **Nêu ngày có hiệu lực.** Một luật có hiệu lực từ 01/07/2024 trả lời khác cho câu hỏi
  về năm 2023.
- **Luôn dẫn tên văn bản kèm số ký hiệu.**
- Nếu kho dữ liệu và giả định của người dùng khác nhau, hãy cho họ xem chính văn bản.

## Xử lý sự cố

**"Your session has expired. You can reconnect to re-authorize."**
Kết nối lại connector Lawgical. Nếu lặp lại chỉ sau vài giờ, hãy báo lại — đó là một lỗi
phía máy chủ đã được sửa ngày 29/07/2026 và giờ hiếm khi xảy ra.

**"Authorization with Lawgical failed", hoặc kết nối được nhưng không có công cụ nào.**
Nếu connector được tạo với một URL Lawgical cũ, hãy **xóa đi và thêm lại** — kết nối lại
cái cũ sẽ không bao giờ chạy được. Client MCP gắn token của nó với đúng URL đã cấu hình
ban đầu, nên một connector cũ sẽ gửi yêu cầu mà không kèm thông tin xác thực và lặp vô
hạn. Xóa rồi thêm lại là hết.

**"Không thể tra cứu: đã dùng hết 20/20 lượt tra cứu hôm nay."**
Đã hết hạn mức ngày của gói Miễn phí, đặt lại vào 00:00 giờ Việt Nam.
`get_account_status()` miễn phí và cho biết con số chính xác; gói Trả phí bỏ giới hạn này.
Lưu ý các lần tra cứu không ra kết quả **không** bị tính, nên con số này chỉ gồm những
lần thành công.

**Không thấy công cụ nào.**
Connector chưa được kết nối. Lawgical được thêm dưới dạng remote MCP server tại
`https://legal.lawgical.vn/mcp`.
