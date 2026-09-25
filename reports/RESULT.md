# RAG evaluation results

## Run information

| Field                              | Value                                                                             |
| ---------------------------------- | --------------------------------------------------------------------------------- |
| Evaluation date                    | 2026-09-25                                                                        |
| Framework and version              | Focused pytest contract checks; chưa chạy RAGAS                                   |
| Evaluator model                    | Chưa có                                                                           |
| Generator model                    | Chưa có; Task 10 chưa hoàn thiện                                                  |
| Embedding model                    | OpenAI `text-embedding-3-small`, dimension 1536                                   |
| Corpus version/commit              | Corpus Shopee return/refund; standardized legal/news; branch `NguyenThiHongNhung` |
| Golden dataset size                | 15 câu theo `group_project/evaluation/golden_dataset.json`                        |
| `top_k`                            | Dense/BM25 smoke test: 3; contract test: 2                                        |
| Fallback threshold and calibration | Chưa áp dụng; Task 9 chưa hoàn thiện                                              |

## Configurations

- **Config A — dense-only:** Đã kiểm tra đường dense trên ChromaDB; chưa đo chất lượng câu trả lời.
- **Config B — hybrid + RRF:** Dense + BM25 + RRF đã có và contract retrieval pass; chưa chạy generation/evaluation.

Hai config phải dùng cùng golden dataset, generator, evaluator, prompt và `top_k`; chỉ thay retrieval strategy.

## Overall scores

| Metric            | Config A | Config B | Delta B−A |
| ----------------- | -------: | -------: | --------: |
| Faithfulness      |      N/A |      N/A |       N/A |
| Answer relevance  |      N/A |      N/A |       N/A |
| Context recall    |      N/A |      N/A |       N/A |
| Context precision |      N/A |      N/A |       N/A |
| **Average**       |      N/A |      N/A |       N/A |

Chưa có điểm hợp lệ vì Task 8–10, generation và quy trình đánh giá RAGAS chưa được chạy end-to-end. Không dùng số lượng test pass để thay thế cho bốn metric chất lượng.

## A/B comparison

- Cấu hình tốt hơn: Chưa kết luận.
- Evidence: Hybrid đã trả ranked list đúng schema và RRF đã được kiểm tra công thức; chưa có điểm answer-level để so sánh A/B.
- Trade-off về latency/cost: Hybrid cần thêm BM25 và RRF; OpenAI embedding phát sinh chi phí API, nhưng BM25/RRF không cần thêm model.

## Worst performers

|   # | Question              | Config | Faithfulness | Relevance | Recall | Precision | Failure stage | Root cause                         |
| --: | --------------------- | ------ | -----------: | --------: | -----: | --------: | ------------- | ---------------------------------- |
|   1 | Chưa có lượt đánh giá | N/A    |          N/A |       N/A |    N/A |       N/A | generation    | Task 10 chưa chạy                  |
|   2 | Chưa có lượt đánh giá | N/A    |          N/A |       N/A |    N/A |       N/A | retrieval     | Chưa chạy evaluator                |
|   3 | Chưa có lượt đánh giá | N/A    |          N/A |       N/A |    N/A |       N/A | data          | Chưa có phân tích lỗi answer-level |

## Recommendations

| Priority | Action                                           | Evidence from failure analysis                         | Expected impact                       | How to verify                                     |
| -------: | ------------------------------------------------ | ------------------------------------------------------ | ------------------------------------- | ------------------------------------------------- |
|        1 | Hoàn thiện Task 8–10 và chạy end-to-end          | Chưa có generation/fallback/evaluator                  | Có điểm RAGAS và citation để đánh giá | Chạy trên 15 câu golden dataset                   |
|        2 | Chạy A/B dense-only và hybrid + RRF              | Hybrid đã pass contract nhưng chưa có quality score    | Xác định retrieval strategy tốt hơn   | Giữ nguyên prompt, generator, corpus và top-k     |
|        3 | Hiệu chỉnh chunking và threshold bằng query thật | Chunking đã tạo 172 chunks; threshold chưa calibration | Cải thiện recall/precision            | Ghi lại query, score, latency và kết quả chạy lại |

## Bonus experiments

| Experiment                      | Baseline                 | Metric delta | Latency/cost delta | Conclusion                                 |
| ------------------------------- | ------------------------ | -----------: | -----------------: | ------------------------------------------ |
| Focused retrieval contract test | Chưa có quality baseline | 4 tests pass |   Không đo latency | Xác nhận schema, thứ tự, uniqueness và RRF |
