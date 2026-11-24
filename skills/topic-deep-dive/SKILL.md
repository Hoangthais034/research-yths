---
name: topic-deep-dive
description: Tìm hiểu một đề tài, công việc, phần việc, công ty hoặc vấn đề từ tài liệu nội bộ (Outline, wiki) và nguồn chính thức, rồi làm báo cáo hiện trạng, vấn đề, các cách giải quyết, giải pháp tối ưu, có dẫn chứng link. Dùng khi được giao "tìm hiểu", "đọc tài liệu rồi report", "phân tích dự án", "so sánh các phương án", "nên làm theo hướng nào".
---

# Tìm hiểu sâu một đề tài và làm báo cáo

Dùng khi người dùng (BA) được giao tìm hiểu một dự án, một công ty khách hàng, một phần việc hay một vấn đề, rồi báo cáo lại cho sếp kèm ý kiến nên làm theo hướng nào.

## 1. Xác định sếp cần gì

- Đọc kỹ tin nhắn giao việc (ảnh chat, email). Ghi lại: đối tượng cần tìm hiểu, các lựa chọn cần so sánh, và câu sếp thật sự muốn trả lời.
- Mặc định báo cáo phải trả lời đủ 4 câu, theo đúng thứ tự: (1) đối tượng là gì, đang vận hành thế nào; (2) đang gặp vấn đề gì; (3) các cách giải quyết hiện có; (4) giải pháp tối ưu nhất và vì sao. Báo cáo chỉ so sánh công cụ mà thiếu bối cảnh là chưa đạt.

## 2. Đọc hết nguồn nội bộ

- Outline: mở bằng Claude in Chrome (phiên đã đăng nhập của người dùng). Gọi API bằng JavaScript trong trang thay vì chụp màn hình:
  - `POST /api/documents.info {id}` lấy nội dung markdown; `POST /api/documents.list {parentDocumentId}` duyệt cây trang con, lấy cả `url` và `updatedAt`.
  - Trả về từng đoạn khoảng 15–19 nghìn ký tự. Bỏ link ảnh, thay URL bằng [url] và đổi ký tự `? & =` thành dấu cách, nếu không kết quả bị chặn vì giống query string.
  - Nếu API trả lỗi hoặc trang chuyển về Login: nhờ người dùng đăng nhập lại, không đoán nội dung.
  - Không dùng tính năng tải file (download) của Outline.
- Đọc hết, không dừng ở mục lục. Ghi lại trang nào đã đọc và ngày cập nhật cuối.
- Tìm riêng các trang "đề xuất", "cải tiến", "phương án": đây thường là các cách giải quyết hiện có.
- Ảnh minh chứng cần dùng: cuộn tới ảnh bằng `scrollIntoView`, chụp cả màn hình ở tỷ lệ 1 rồi cắt bằng PIL.

## 3. Bổ sung nguồn ngoài

- Với sản phẩm, phiên bản, giá, giấy phép: tra trang chính thức của hãng (release notes, tài liệu) để xác minh lại những gì tài liệu nội bộ viết.
- Ghi rõ ô nào "chưa xác minh" thay vì điền theo trí nhớ.

## 4. Dựng tài liệu theo từng lớp

Làm lần lượt, mỗi bước là một artifact riêng, để báo cáo cuối dựa vào đó:

1. **Tóm tắt cho người mới** (Docs): dự án là gì, ai làm gì, BA cần hiểu gì và làm gì.
2. **Luồng vận hành hiện tại** (trang HTML để dễ tùy biến): sơ đồ làn bơi theo bộ phận, từng bước kèm ảnh minh chứng, bảng bộ phận × công cụ, chuỗi chứng từ của một ví dụ có thật, các chỗ luồng bị đứt, câu hỏi cần xác nhận.
3. **Trang tìm hiểu chi tiết** (HTML): so sánh các lựa chọn theo bảng có màu, đối chiếu từng vấn đề với từng lựa chọn, kết quả chạy thử nếu có.
4. **Báo cáo gửi sếp** (Docs): theo khung ở mục 5.

## 5. Khung báo cáo

- **Tóm tắt:** 4 gạch đầu dòng trả lời 4 câu ở mục 1.
- **1. Đối tượng là gì:** sản phẩm, cách làm, các bộ phận (bảng việc chính + công cụ), luồng chính, những gì tài liệu chưa nói.
- **2. Vấn đề:** bảng toàn bộ vấn đề theo nhóm, kèm trạng thái; phần "gốc của vấn đề" gắn nhãn nhận định riêng, có một ví dụ cụ thể.
- **3. Các cách giải quyết hiện có:** (a) đơn vị đang tự vá thế nào và giới hạn; (b) các hướng đang bàn, bảng cách làm / điểm được / điểm vướng, tóm tắt đề xuất có sẵn trên wiki; (c) so sánh các công cụ nếu có, kèm kết quả chạy thử.
- **4. Giải pháp tối ưu nhất:** chọn một hướng, nói vì sao không chọn các hướng còn lại, khi nào nên đổi phương án; lộ trình theo giai đoạn có cổng kiểm tra, mỗi giai đoạn ghi giải quyết vấn đề nào.
- **5. Rủi ro:** bảng rủi ro / dấu hiệu / cách giảm.
- **6. Câu hỏi cần chốt và việc tiếp theo.**
- **Nguồn.**

## 6. Dẫn chứng

- Mọi link dẫn chứng lấy từ trang gốc trên Outline (hoặc wiki gốc), không dẫn sang artifact do Claude tự làm.
- Cuối mỗi mục có dòng nghiêng "Dẫn chứng: …" chỉ rõ trang nào cho số liệu nào.
- Mục Nguồn chia nhóm, mỗi trang ghi ngày cập nhật cuối, và ghi ngày đọc.
- Bảng hoặc con số tự tổng hợp (không có trong nguồn) phải ghi rõ là "kết quả đối chiếu riêng".

## 7. Kiểm tra trước khi giao

- Đối chiếu lại từng con số với trang nguồn (tìm chuỗi trong nội dung trang), và kiểm tra con số đó thuộc kịch bản nào. Ví dụ sai đã gặp: ba con số giá thành là BOM / thực tế / có chi phí chung, không phải ba con số "lệch nhau"; số chứng từ lấy từ kịch bản thử, không phải đơn thật.
- Đếm lại các tổng (số ô xanh, số vấn đề theo trạng thái); ghi chú chỗ tài liệu gốc tự mâu thuẫn.
- Rà toàn bộ bằng skill research-yths:vietnamese-readability-review: giải thích thuật ngữ lần đầu, gắn nhãn "Đề xuất:", "Nhận định riêng:" cho ý kiến riêng, giọng trung tính, không dùng "em", "tôi", "người viết".
- Sửa của người dùng trong doc chỉ được gợi ý (suggestion), không tự thay.

## 8. Bàn giao

- Soạn sẵn tin nhắn trả lời sếp (bản gọn kèm link và bản rất ngắn), xưng hô bình thường trong tin nhắn. Không tự gửi.
- Nhắc người dùng bật chia sẻ doc trước khi gửi link.
- Liệt kê câu hỏi còn mở và chỗ cần người dùng xác nhận.
