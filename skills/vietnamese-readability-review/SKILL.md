---
name: vietnamese-readability-review
description: Rà văn bản tiếng Việt (báo cáo, doc, trang Outline/wiki, bản nháp, đoạn dán) tìm câu khó hiểu, viết gọn sai nghĩa, gộp ý, xưng hô sai trong báo cáo, rồi đề xuất câu viết lại. Dùng khi được bảo check/rà tiếng Việt, "rà soát", "check lại tiếng Việt", hoặc trước khi đưa bản nháp tiếng Việt lên tài liệu.
---

# Rà soát tiếng Việt cho dễ hiểu

Mục tiêu: người đọc (ví dụ sếp, khách hàng, người mới vào dự án) đọc một lần là hiểu, không phải đoán ý.

## Quy trình

1. **Đọc toàn bộ văn bản trước.** Chọn cách đọc theo nguồn:
   - Google Doc: Drive `read_file_content` (includeComments: true).
   - Trang web hoặc wiki (Outline, Confluence, Notion qua trình duyệt): mở bằng trình duyệt, đọc bằng `get_page_text`. Luôn đọc lại bản mới nhất vì người dùng có thể đã tự sửa.
   - Claude Docs hoặc artifact: đọc bằng công cụ của connector đó.
   - Bản nháp Claude vừa soạn trong chat, hoặc đoạn người dùng dán: rà trực tiếp.
   Ghi nhận thuật ngữ đã được giải thích ở đâu (phụ lục thuật ngữ, lần đầu xuất hiện).
   Phân biệt phần **người dùng tự viết** với phần **Claude soạn**. Phần người dùng tự viết chỉ được gợi ý (suggestion), không tự ý thay.
2. **Rà từng đoạn theo checklist bên dưới.** Chỉ đánh dấu chỗ thực sự gây khó hiểu, không bắt lỗi văn phong vụn vặt.
3. **Báo cáo kết quả** theo định dạng ở dưới, nhóm theo mục của văn bản, chỗ nặng nhất trước.
4. **Không sửa vào file khi chưa được đồng ý.** Chỉ sửa những chỗ người dùng duyệt. Khi sửa:
   - Google Doc: chỉ thay phần chữ, giữ nguyên font, cỡ chữ, nhãn in đậm, bảng và con số.
   - Trang wiki qua trình duyệt: làm theo cách nhập người dùng đã dặn (gõ hoặc dán từng đoạn, khoảng cách giữa các đoạn). Đặt con trỏ bằng JavaScript thay vì click theo toạ độ, và đọc lại đoạn vừa sửa để kiểm tra.
   - Câu do người dùng tự viết: giữ nguyên trừ khi họ đồng ý bản viết lại.
5. **Tự rà bản nháp của mình.** Khi Claude soạn nội dung tiếng Việt để đưa lên tài liệu, rà bản nháp theo checklist trước khi gửi người dùng duyệt, và sửa luôn những lỗi tìm được.

## Checklist lỗi

| Mã | Lỗi | Dấu hiệu |
|---|---|---|
| L1 | Gộp nhiều ý vào một câu | Câu có từ 3 mệnh đề trở lên, nhiều dấu chấm phẩy, hoặc trên khoảng 35 chữ |
| L2 | Rút gọn sai nghĩa | Cụm từ bị rút thành từ khác nghĩa, ví dụ viết "trình duyệt" khi ý là "gửi lên để duyệt"; "công ghi nhận nguồn" thay cho "giờ công của người nhập dữ liệu tại nguồn" |
| L3 | Thuật ngữ hoặc viết tắt chưa giải thích | Lần đầu xuất hiện mà không có giải thích, không có trong phụ lục thuật ngữ |
| L4 | Danh từ hoá nặng, thiếu chủ thể | Không rõ ai làm, ví dụ "cần xác nhận quan hệ" mà không nói ai xác nhận, quan hệ giữa cái gì với cái gì |
| L5 | Con số không kèm ý nghĩa | Đưa tỷ lệ hoặc phép tính mà không nói con số đó cho thấy điều gì |
| L6 | Suy luận trình bày như sự thật | Nhận định riêng nhưng không gắn nhãn "Giả định:", "Suy ra:", "Đề xuất:", "Nhận định riêng:" |
| L7 | Trộn Anh – Việt không cần thiết | Dùng từ tiếng Anh khi đã có từ tiếng Việt quen thuộc, hoặc dùng cả hai lẫn lộn |
| L8 | Câu hỏi hoặc tiêu đề quá cô đặc | Câu hỏi trong bảng đọc như ghi chú riêng, người ngoài không hiểu đang hỏi gì |
| L9 | Từ nối mơ hồ | "Như vậy", "điều này", "việc đó" mà không rõ chỉ cái gì |
| L10 | Thiếu dấu câu hoặc câu hỏi kép | Câu dài không có dấu phẩy, dấu chấm hoặc dấu hỏi; hai câu hỏi gộp làm một nên người đọc không biết trả lời ý nào |
| L11 | Mất thuật ngữ khi diễn giải | Viết lại cho dễ hiểu nhưng bỏ mất tên thuật ngữ gốc (ví dụ bỏ "Transition requirement", "RTM"), khiến sau này khó tra lại |
| L12 | Đại từ nhân xưng trong báo cáo | Báo cáo, tài liệu gửi người khác có "em", "tôi", "mình", "chúng tôi", "người viết", "người soạn" (chỉ chính tác giả). Thay bằng danh từ hoặc động từ dùng chung: "Đề xuất:", "Nhận định riêng:", "Lộ trình chưa ghi…", "Thứ tự các bước được dựng lại…", câu bị động "được gửi", "được đối chiếu" |

## Nguyên tắc khi viết lại

- Giữ nguyên nghĩa, con số, phép tính và nguồn trích dẫn (Slide số, S1…). Không thêm thông tin mới không có trong nguồn.
- Mỗi câu một ý. Chủ ngữ rõ ràng: ai làm gì.
- Dùng từ rõ nghĩa, tự nhiên; không rút gọn cụm từ thành từ khác nghĩa.
- Thuật ngữ chuyên ngành giữ lại nếu cần, nhưng giải thích ngắn ở lần đầu hoặc trỏ tới phụ lục.
- Ưu tiên câu ngắn hơn bản gốc hoặc dài tương đương; chỉ dài hơn khi bản gốc thiếu ý khiến người đọc phải đoán.
- Nếu có thể, đưa 2 phương án: một bản đầy đủ, một bản ngắn.
- Ghi chú học tập riêng: viết theo giọng người dùng, như người đã hiểu bài tự ghi lại, không viết kiểu văn mẫu.
- Báo cáo và tài liệu gửi người khác (sếp, khách hàng, nhóm dự án): giọng trung tính, không dùng đại từ nhân xưng chỉ tác giả (L12). Ý kiến riêng vẫn phải gắn nhãn rõ (L6).
- Tin nhắn chat gửi trực tiếp cho người khác (không phải báo cáo) thì được xưng hô bình thường.

## Định dạng báo cáo

Cho mỗi chỗ phát hiện:

- **Vị trí:** mục và đoạn (ví dụ "6.2 Câu hỏi mở, dòng 7")
- **Câu gốc:** trích nguyên văn
- **Lỗi:** mã lỗi và một câu giải thích vì sao khó hiểu
- **Viết lại:** câu đề xuất

Cuối báo cáo: tổng số chỗ, chỗ nào nên sửa trước, và hỏi người dùng muốn áp dụng những chỗ nào. Đánh dấu rõ chỗ nào là câu người dùng tự viết (chỉ gợi ý).

Nếu đang rà bản nháp của Claude, có thể đưa luôn bản đã sửa hoàn chỉnh bên dưới danh sách lỗi để người dùng duyệt một lần.

Với văn bản dài, nếu có hơn 15 chỗ thì liệt kê 15 chỗ nặng nhất trước và hỏi có muốn xem tiếp không.
