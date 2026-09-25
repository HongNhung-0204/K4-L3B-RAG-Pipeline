# Individual contribution report

Mỗi thành viên copy template này thành:

```text
reports/<student-id>-<short-name>.md
```

Giới hạn khuyến nghị: 1 trang, không chép lại README hoặc mô tả lý thuyết chung. Báo cáo không phải một bài pipeline cá nhân; mục đích là ghi nhận ownership và bằng chứng đóng góp trong sản phẩm nhóm.

---

## Thông tin

- Họ và tên: Nguyễn Thị Hồng Nhung
- Mã học viên: 2A202602557
- Nhóm: Uống nước đẹp da
- Repository/branch: NguyenThiHongNhung

## Phần việc đã thực hiện

| Module/deliverable | Việc tôi trực tiếp làm                                                                                                                                                                                            | File/commit/PR                                                | Trạng thái |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- | ---------- |
| Task 4             | Đọc Markdown, giữ metadata, chunk recursive với `CHUNK_SIZE=500` và `CHUNK_OVERLAP=50`; embedding qua OpenAI; upsert ChromaDB bằng ID ổn định; lọc chunk chỉ chứa ký tự phân cách và dọn stale IDs khi index lại. | `src/task4_chunking_indexing.py`, branch `NguyenThiHongNhung` | Done       |
| Task 5             | Dense retrieval dùng lại `embed_texts()`, query ChromaDB cosine và chuyển distance thành similarity; trả `SearchResult` đúng schema.                                                                              | `src/task5_semantic_search.py`, branch `NguyenThiHongNhung`   | Done       |
| Task 6             | Xây BM25 trên cùng corpus chunk, tokenize Unicode, sort theo score giảm dần và xử lý corpus nhỏ hoặc rỗng.                                                                                                        | `src/task6_lexical_search.py`, branch `NguyenThiHongNhung`    | Done       |
| Task 7             | Implement RRF theo rank bắt đầu từ 1, gộp theo ID, copy item trước khi đổi score/method và phát hiện ID trùng trong cùng ranked list.                                                                             | `src/task7_reranking.py`, branch `NguyenThiHongNhung`         | Done       |
| Kiểm thử retrieval | Chạy focused contract tests cho chunking, dense, BM25 và RRF; index corpus thật thành công.                                                                                                                       | `tests/test_contracts.py`, ChromaDB local                     | Done       |

Chỉ kê khai công việc có thể đối chiếu bằng file, commit, pull request, test hoặc kết quả evaluation.

## Quyết định kỹ thuật quan trọng

Mô tả tối đa hai quyết định mà bạn trực tiếp tham gia:

1. **Quyết định:** Dùng OpenAI `text-embedding-3-small` cho cả corpus và query.
   **Lý do/evidence:** `embed_texts()` là điểm dùng chung giữa Task 4 và Task 5, giúp model và dimension nhất quán; dimension sử dụng là 1536.
   **Trade-off:** Có chi phí API và phụ thuộc mạng, nhưng không phải tải model local và giữ được cùng một embedding space.

2. **Quyết định:** Giữ chunk recursive `500/50` và dùng upsert với ID dạng `<document>::chunk-<index>`.
   **Lý do/evidence:** Giữ quan hệ chunk-tài liệu, hỗ trợ index lại không nhân bản; sau lọc chunk rác, corpus tạo được 172 chunks.
   **Trade-off:** Chunk nhỏ hơn giúp định vị tốt nhưng tăng số embedding; overlap giữ ngữ cảnh nhưng tăng chi phí.

## Kiểm thử và kết quả

- Test hoặc query tôi đã dùng: `pytest tests/test_contracts.py -q -k "chunk_documents_preserves_identity_and_metadata or semantic_search_uses_shared_embedding_and_contract or lexical_search_returns_bm25_contract or rrf_uses_rank_deduplicates_and_marks_hybrid"`.
- Kết quả trước/sau nếu có: 4 focused contract tests passed; Task 4 index thành công 172 chunks và ChromaDB xác nhận `CHROMA_COUNT=172`.
- Lỗi đã phát hiện và cách xử lý: BM25 trên corpus rất nhỏ có thể trả score 0; vẫn giữ các item trong top-k để bảo toàn ranked list. Dense search từng trả chunk chỉ chứa dấu phân cách, nên đã lọc chunk không có ký tự chữ/số và re-index.

## Điều còn hạn chế

- Một hạn chế cụ thể của phần tôi làm: Chưa có đo A/B đầy đủ giữa dense-only và hybrid trên câu trả lời sinh; Task 8–10 chưa thuộc phần triển khai này.
- Nếu có thêm thời gian, thay đổi đầu tiên tôi sẽ thực hiện: Batching embedding, đo latency/cost và hiệu chỉnh threshold bằng query in-domain/out-of-domain sau khi hoàn thiện pipeline end-to-end.

## Xác nhận đóng góp

Tôi xác nhận nội dung trên phản ánh đúng phần việc của mình và có thể giải thích hoặc chạy lại trong buổi demo.

- Ngày: 2026-09-25
- Tên thành viên: Nguyễn Thị Hồng Nhung
