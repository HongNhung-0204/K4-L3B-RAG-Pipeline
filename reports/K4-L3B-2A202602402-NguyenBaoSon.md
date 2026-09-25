# Báo cáo đóng góp cá nhân

## Thông tin

- Họ và tên: Nguyễn Bảo Sơn
- Mã học viên: 2A202602402
- Nhóm: Uống nước đẹp da
- Repository: https://github.com/HongNhung-0204/K4-L3B-RAG-Pipeline
- Nhánh làm việc: `NguyenBaoSon`
- Commit đối chiếu: `57800f6` (`Task 1,2,3`, tác giả `NguyenBaoSonTLU`, ngày 25/09/2026)

## Phần việc đã thực hiện

| Module/deliverable | Việc tôi trực tiếp làm | File/commit/PR | Trạng thái |
| --- | --- | --- | --- |
| Task 1 và dữ liệu legal | Đưa 3 chính sách Shopee vào `data/landing/legal/` dưới dạng DOCX; hoàn thiện script kiểm tra cấu trúc DOCX, nội dung và metadata nguồn. | `src/task1_collect_legal_docs.py`, `data/landing/legal/*.docx`, `57800f6` | Partial: tài liệu có nguồn là trang HTML; script xác nhận file đã thu thập, không tải DOCX gốc từ Shopee. |
| Task 2 và dữ liệu news | Chuẩn bị 7 bản Markdown có URL/ngày thu thập và tạo JSON tương ứng; bổ sung tùy chọn `--refresh` bằng Crawl4AI. | `src/task2_crawl_news.py`, `data/landing/news/*.md`, `data/landing/news/*.json`, `57800f6` | Partial: luồng từ snapshot đã chạy; chưa kiểm chứng crawl trực tiếp bằng `--refresh`. |
| Task 3 | Chuyển 3 DOCX và 7 JSON sang Markdown trong `data/standardized/`, giữ metadata và chỉ ghi file khi nội dung đổi. | `src/task3_convert_markdown.py`, `data/standardized/`, `57800f6` | Done |
| Dữ liệu đánh giá | Lập 15 câu hỏi có câu trả lời và ngữ cảnh đối chiếu trên 10 tài liệu; ghi nhận tình trạng đánh giá trong báo cáo nhóm. | `group_project/evaluation/golden_dataset.json`, `group_project/evaluation/RESULT.md`, `57800f6` | Partial: chưa có điểm RAG hay kết quả A/B do Task 4–10 chưa chạy được. |

## Quyết định kỹ thuật quan trọng

1. **Quyết định:** Dùng các bản tài liệu đã thu thập làm đầu vào mặc định và giữ `source_url` cùng ngày thu thập trong metadata. **Lý do/evidence:** ba DOCX và bảy Markdown đã có trong repo; chạy Task 1 xác nhận 3 file, Task 2 tạo 7 JSON. **Trade-off:** dữ liệu có thể cũ; các URL Shopee trỏ đến trang HTML và việc crawl lại chưa được kiểm chứng.
2. **Quyết định:** Trích các đoạn Markdown sẵn có trực tiếp từ cấu trúc DOCX và chỉ ghi đầu ra khi thay đổi. **Lý do/evidence:** MarkItDown trong môi trường hiện tại thiếu phần phụ thuộc DOCX; chạy Task 3 tạo 3 legal và 7 news, lần chạy tiếp theo báo `Current` cho cả 10 file. **Trade-off:** với DOCX có bố cục Word phức tạp, cần bộ chuyển đổi DOCX đầy đủ để bảo toàn định dạng.

## Kiểm thử và kết quả

- Đã chạy `python -m src.task1_collect_legal_docs`: xác nhận 3 DOCX hợp lệ và có URL nguồn trong metadata.
- Đã chạy `python -m src.task2_crawl_news`: tạo 7 JSON; mỗi file có `url`, `title`, `date_crawled`, `content_markdown` và nội dung không rỗng.
- Đã chạy `python -m src.task3_convert_markdown` hai lần: có 3 file legal và 7 file news chuẩn hóa; lần thứ hai không ghi lại file nào.
- Đã đối chiếu 15/15 `expected_context` với file `source` tương ứng và chạy `pytest tests/test_acceptance.py -q`: **5 passed**. Trước khi bổ sung bộ dữ liệu và báo cáo đánh giá, bài kiểm tra này có **3 passed, 2 failed**.
- Lỗi đã xử lý: DOCX thiếu phần phụ thuộc MarkItDown được đọc qua XML; một tài liệu legal thiếu dấu kết thúc front matter đã được chuẩn hóa.

## Điều còn hạn chế

- Phần tôi làm chưa xác minh việc tải lại nội dung trực tiếp từ bảy trang Shopee; điểm faithfulness, relevance, recall, precision và so sánh A/B cũng chưa được đo vì pipeline truy xuất và sinh câu trả lời chưa hoàn chỉnh.
- Nếu có thêm thời gian, tôi sẽ chạy `--refresh` trên từng URL công khai, đối chiếu nội dung mới với snapshot và cập nhật metadata ngày thu thập khi crawl thành công.

## Xác nhận đóng góp

Tôi xác nhận nội dung trên phản ánh phần việc được ghi trong commit `57800f6` và các kết quả chạy nêu trên; tôi có thể giải thích hoặc chạy lại các bước này trong buổi demo.

- Ngày: 25/09/2026
- Tên thành viên: Nguyễn Bảo Sơn
    