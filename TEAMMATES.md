# TEAMMATES

Thông tin thành viên nhóm **Uống nước đẹp da**.

| STT | Họ và tên             | Mã học viên | Vai trò                                        | Nhánh / Phần việc phụ trách                                                                                                                                   |
| --- | --------------------- | ----------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Nguyễn Thị Hồng Nhung | 2A202602557 | Developer — Retrieval Engineer                 | Branch `NguyenThiHongNhung` — Task 4 (Chunking & Indexing), Task 5 (Semantic Search), Task 6 (Lexical Search), Task 7 (RRF Reranking), kiểm thử retrieval     |
| 2   | Nguyễn Bảo Sơn        | 2A202602402 | Developer — Data Engineer                      | Branch `NguyenBaoSon` — Task 1 (Thu thập dữ liệu legal), Task 2 (Crawl dữ liệu news), Task 3 (Chuẩn hóa Markdown), xây dựng golden dataset và evaluation data |
| 3   | Vũ Văn Điền           | 2A202602418 | Developer — AI Pipeline & Application Engineer | Branch `VuVanDien-2A202602418` — Task 8 (PageIndex fallback), Task 9 (Retrieval Pipeline), Task 10 (Generation & Citation), Streamlit UI, debug pipeline      |

## Phân công tổng quan

* **Nguyễn Thị Hồng Nhung**

  * Phụ trách xây dựng tầng xử lý và truy xuất dữ liệu:

    * Chunking tài liệu.
    * Tạo vector index bằng ChromaDB.
    * Dense retrieval, BM25 retrieval.
    * Hybrid retrieval bằng RRF.

* **Nguyễn Bảo Sơn**

  * Phụ trách thu thập và chuẩn hóa dữ liệu đầu vào:

    * Thu thập tài liệu legal Shopee.
    * Crawl và lưu dữ liệu news.
    * Chuyển đổi dữ liệu sang Markdown chuẩn hóa.
    * Chuẩn bị bộ dữ liệu đánh giá.

* **Vũ Văn Điền**

  * Phụ trách hoàn thiện pipeline RAG và ứng dụng:

    * PageIndex fallback.
    * Kết hợp retrieval pipeline.
    * Sinh câu trả lời kèm citation.
    * Xây dựng giao diện Streamlit.
    * Xử lý lỗi tích hợp embedding, LLM và proxy.

## Repository

* Repository: `https://github.com/HongNhung-0204/K4-L3B-RAG-Pipeline.git`
* Nhóm: **Uống nước đẹp da**
