# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 09
- **Họ tên:**NGÔ THU THÚY
- **Lớp:**CNTT3
- **Link repository Pha2:**https://github.com/ngothuthuy87208-eng/HN-K26-CNTT3_PromptAI_H02
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):**Gemini

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt chỗ workshop ra JSON

**KET QUA AI**

```text
[
  {
    "ma_lop": "NANTAY",
    "ngay_hoc": "2026-12-13",
    "nguoi_lon": 2,
    "tre_em": 1,
    "ca_hoc": "chieu",
    "ghi_chu": null
  },
  {
    "ma_lop": "BANXOAY",
    "ngay_hoc": "2027-01-10",
    "nguoi_lon": 3,
    "tre_em": 0,
    "ca_hoc": null,
    "ghi_chu": "1 người bị đau cổ tay"
  },
  {
    "ma_lop": "VEGOM",
    "ngay_hoc": null,
    "nguoi_lon": 4,
    "tre_em": 0,
    "ca_hoc": "sang",
    "ghi_chu": "1 bạn đi xe lăn" 
  }
]
```

**Link trò chuyện:**https://share.gemini.google/jrLhlXOB8VuE

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
### PHÂN TÍCH YÊU CẦU & TÍNH TOÁN BÁO GIÁ

**Thông tin nhóm khách:**
* **Lớp học đăng ký:** BANXOAY – Làm gốm bàn xoay, 3 giờ (Đơn giá người lớn: 550.000 đồng/người).
* **Số lượng thành viên:** 5 người lớn, 2 trẻ em trong độ tuổi 6–12 (8 tuổi và 12 tuổi), 1 trẻ dưới 6 tuổi đi kèm (4 tuổi).
* **Dịch vụ đi kèm:** Nung và giao tận nhà 4 sản phẩm.

---

**Chi tiết các bước tính toán:**

* **Bước 1: Tính tiền người lớn**
  * Phép tính: $5 \times 550.000 = 2.750.000\text{ đồng}$

* **Bước 2: Tính tiền trẻ em**
  * Trẻ em 8 tuổi và 12 tuổi (nằm trong độ tuổi từ 6 đến 12 tuổi, tính 70% giá người lớn): $2 \times (550.000 \times 70\%) = 2 \times 385.000 = 770.000\text{ đồng}$
  * Trẻ em 4 tuổi (dưới 6 tuổi đi kèm, miễn phí): $1 \times 0 = 0\text{ đồng}$
  * Tổng tiền trẻ em: $770.000 + 0 = 770.000\text{ đồng}$

* **Bước 3: Tính tiền vé (tiền người lớn + tiền trẻ em)**
  * Phép tính: $2.750.000 + 770.000 = 3.520.000\text{ đồng}$

* **Bước 4: Tính giảm giá nhóm (nếu có)**
  * Vì nhóm có đủ 5 người lớn nên được giảm 5% trên tổng tiền học (tiền người lớn + tiền trẻ em): $3.520.000 \times 5\% = 176.000\text{ đồng}$
  * Tiền học sau giảm: $3.520.000 - 176.000 = 3.344.000\text{ đồng}$

* **Bước 5: Tính phụ thu (phí nung và giao sản phẩm)**
  * Phí nung và giao 4 sản phẩm tận nhà (không áp dụng giảm giá): $4 \times 80.000 = 320.000\text{ đồng}$

* **Bước 6: Tính tổng tiền**
  * Phép tính: $3.344.000 + 320.000 = 3.664.000\text{ đồng}$

[RESULT: 3.664.000 đồng]
```

**Link trò chuyện:**https://share.gemini.google/vmpxewlJlBxe

### b) Kiểm tra kết quả AI

AI đúng
## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

a) Nhận xét & Sửa lỗi Prompt Trạm 1
1. Điểm tốt:

Áp dụng tốt kỹ thuật phân tách dữ liệu bằng thẻ XML (<phan_hoi>, <vi_du>, <chinh_sach>).

Có đưa ra cấu trúc mẫu (One-shot/Schema) và ràng buộc không chào hỏi, chỉ trả về JSON.

2. Lỗi cần khắc phục:

Lỗi chính tả & ký tự thừa: Các từ như "du liệu", "đứng 4 trường", "I", "so khach" (thiếu dấu gạch dưới _), "[Explantion]", "nhắc tôi" (nhắc tới), "Ket quả", "duy nhat". Việc viết sai tên trường (so khach thay vì so_khach) sẽ làm sai lệch cấu trúc JSON đầu ra.

Thiếu ngữ cảnh & quy tắc phòng ngừa ảo giác: Nếu khách hàng không nhắc đến số người tham gia, AI có thể tự đoán. Cần bổ sung quy tắc null cho cả "so_khach" hoặc quy định rõ cách xử lý khi thiếu thông tin, đồng thời yêu cầu không bọc trong markdown ````json` (nếu hệ thống parser yêu cầu chuỗi JSON thuần).

3. Bản chỉnh sửa hoàn thiện (Gợi ý):

Plaintext
Bạn là một chuyên gia phân tích phản hồi khiếu nại của khách hàng thành định dạng dữ liệu JSON. Hãy đọc nội dung phản hồi của khách hàng trong thẻ <phan_hoi>, đối chiếu với quy định trong thẻ <chinh_sach> và trích xuất thông tin thành đối tượng JSON gồm đúng 4 trường: "loai_su_co", "so_khach", "so_san_pham_bi_hong", "tom_tat".

[Quy tắc dữ liệu]
- "loai_su_co": Bắt buộc là một trong 4 giá trị: "hong_san_pham", "giao_tre", "huong_dan", hoặc "khac".
- "so_khach": Số nguyên (hoặc null nếu không đề cập).
- "so_san_pham_bi_hong": Số nguyên (hoặc null nếu không đề cập).
- "tom_tat": Chuỗi văn bản tóm tắt nội dung khiếu nại, tối đa 20 từ.

[Định dạng đầu ra]
- Tuân thủ đúng cấu trúc trong thẻ <vi_du>.
- Chỉ trả về duy nhất chuỗi JSON hợp lệ. Tuyệt đối không chào hỏi, không giải thích và không dùng dấu ngoặc markdown (```json).

<phan_hoi>
Gia đình tôi 3 người học lớp nặn gốm ngày 01/11/2026, mỗi người làm 2 sản phẩm và đã trả phí nung, giao sản phẩm. Khi nhận hàng, có 5 sản phẩm bị nứt vỡ. Cô hướng dẫn rất nhiệt tình, tôi không có gì phàn nàn về người hướng dẫn. Tôi đề nghị xưởng giải quyết thỏa đáng.
</phan_hoi>

<vi_du>
{"loai_su_co": "hong_san_pham", "so_khach": 3, "so_san_pham_bi_hong": 5, "tom_tat": "5 sản phẩm gốm bị nứt vỡ khi nhận hàng."}
</vi_du>

<chinh_sach>
======================================================
CHÍNH SÁCH ĐỀN BÙ CỦA ĐẤT VIỆT WORKSHOP
======================================================
- hong_san_pham: sản phẩm bị nứt, vỡ khi nung hoặc khi giao: hoàn 150.000 đồng cho mỗi sản phẩm bị hỏng.
- giao_tre: giao sản phẩm trễ quá 7 ngày so với hẹn: tặng voucher 50.000 đồng/khách.
- huong_dan: khiếu nại về thái độ người hướng dẫn: tặng voucher 100.000 đồng/khách.
- khac: chuyển bộ phận Chăm sóc khách hàng xem xét, chưa đề xuất mức đền bù.
- Tổng mức đền bù trên 600.000 đồng phải được Quản lý xưởng duyệt trước khi gửi khách.
</chinh_sach>
b) Nhận xét phần kiểm tra đầu ra Trạm 1
Ý trả lời của bạn đúng hướng nhưng diễn đạt hơi chung chung ở ý 2 (nói "điều kiện có trong chính sách" dễ nhầm sang việc tính tiền đền bù ở Trạm 2, trong khi Trạm 1 chỉ làm nhiệm vụ phân loại và trích xuất). Bạn nên viết cụ thể, rõ ràng theo đúng tiêu chuẩn kỹ thuật:

Tính hợp lệ của cú pháp JSON (Valid JSON): Kết quả trả về phải là một chuỗi JSON chuẩn xác (parse được ngay bằng code, không dính văn bản thừa hay ký tự lỗi) và có đủ, đúng tên 4 trường quy định (loai_su_co, so_khach, so_san_pham_bi_hong, tom_tat).

Tính chính xác của kiểu dữ liệu và giá trị ràng buộc:

loai_su_co phải khớp chính xác với 1 trong 4 mã danh mục quy định (ở ví dụ này phải là "hong_san_pham").

so_khach và so_san_pham_bi_hong phải đúng kiểu số nguyên (3 và 5, không phải dạng chuỗi "3" hay "5 sản phẩm"), hoặc null nếu thiếu dữ liệu.

tom_tat đảm bảo đúng nội dung phản hồi và không vượt quá giới hạn 20 từ.

c) Nhận xét Câu lệnh viết tiếp (Continuation Prompt)
1. Vấn đề trong câu lệnh của bạn:

Nếu bạn chỉ đưa một mẩu câu bị cắt cụ thể ("... Đất Việt Workshop xin hoàn lại Quý khách khoản") mà không kèm lại ngữ cảnh gốc (tên khách/số lượng sản phẩm hỏng/mức đền bù đã tính ở Trạm 2) và phần văn bản đã sinh trước đó, AI sẽ không biết phải hoàn bao nhiêu tiền (750.000 đồng) và không biết phải chuyển cho Quản lý duyệt hay gửi thẳng.

Ngoài ra, câu lệnh này đang hard-code (gắn cứng) nội dung của một trường hợp cụ thể, không dùng được như một prompt mẫu tổng quát cho các tình huống ngắt quãng khác.

2. Cách viết chuẩn (Dùng biến động hoặc đính kèm ngữ cảnh):

Plaintext
Hệ thống bị ngắt kết nối giữa chừng khi đang soạn email phản hồi khách hàng. Dựa vào thông tin sự cố và kết quả tính toán đền bù bên dưới, hãy viết tiếp nội dung email ngay tại điểm bị ngắt.

[Quy tắc bắt buộc]
- Bắt đầu viết nối tiếp ngay sau chữ cuối cùng của đoạn bị ngắt, không lặp lại từ ngữ đã có.
- Giữ nguyên giọng văn lịch sự, chuyên nghiệp của phần mở đầu.
- Tuân thủ đúng mức đền bù và quy trình duyệt theo chính sách.

[Thông tin đầu vào & Chính sách]
{Dữ_liệu_Trạm_1_và_Chính_sách}

[Đoạn email đã viết trước khi bị ngắt]
{Toàn_bộ_đoạn_văn_bản_đã_sinh_ra_đến_chỗ_bị_ngắt}
```

**Link trò chuyện:**https://share.gemini.google/4aykKwG4MGdf

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
| Tiêu chí | Điểm | Minh chứng | Đề xuất sửa |
| --- | --- | --- | --- |
| **Đúng thông tin (50%)**<br>

<br>*(Tối đa: 5.0 điểm)* | 5.0 / 5.0 | - *"Lớp vẽ gốm bên em 200k thôi nè"* (Đề cập mức giá 200.000đ).<br>

<br>- *"Chị đổi trước 1 ngày thì free nha chị"* (Đề cập chính sách đổi lịch trước 1 ngày miễn phí). | Không có lỗi về thông tin được nêu, tuy nhiên cần điều chỉnh cách diễn đạt ở phần Giọng điệu. |
| **Đầy đủ (30%)**<br>

<br>*(Tối đa: 3.0 điểm)* | 1.5 / 3.0 | - **Câu bị lỗi:** *"Có gì chị nhắn em nha!"*<br>

<br>- **Lý do sai:** Đã trả lời đủ 2 thông tin (giá và chính sách đổi lịch), nhưng thiếu lời mời khách hàng cung cấp các thông tin bắt buộc để đặt chỗ (ngày học, ca học, số lượng người tham gia). | - **Câu sửa đề xuất:** *"Để em hỗ trợ giữ chỗ cho mình, chị vui lòng cho em xin thông tin về ngày học, ca học và số lượng người tham gia nhé ạ."* |
| **Giọng điệu (20%)**<br>

<br>*(Tối đa: 2.0 điểm)* | 0.5 / 2.0 | - **Câu bị lỗi:** *"Hi chị ơi! Lớp vẽ gốm bên em 200k thôi nè, vui lắm luôn. Chị đổi trước 1 ngày thì free nha chị. Có gì chị nhắn em nha!"*<br>

<br>- **Lý do sai:** Sử dụng ngôn ngữ quá suồng sã, thiếu tính chuyên nghiệp trong giao tiếp dịch vụ khách hàng (dùng từ tiếng Anh bồi không cần thiết như *"Hi"*, *"free"*; dùng từ ngữ khẩu ngữ/cảm thán suồng sã như *"thôi nè"*, *"vui lắm luôn"*, *"nha chị"*, *"nha"*). | - **Câu sửa đề xuất:** *"Dạ em chào chị ạ. Học phí lớp vẽ gốm bên em hiện tại là 200.000đ/người. Về chính sách đổi lịch, bên em hỗ trợ đổi lịch miễn phí nếu chị báo trước tối thiểu 1 ngày ạ."* |
| **TỔNG ĐIỂM** | **7.0 / 10** |  |  |
```

**Link trò chuyện:**https://share.gemini.google/jCjccpdZ2OQ8
