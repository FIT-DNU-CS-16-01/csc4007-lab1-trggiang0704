# Cleanlab — Label Issues Summary
- suspected_label_issues_count: 1000
- suspected_label_issues_ratio: 0.0200
- export_top_k: 200

---

## Label Review (Top 5 Cleanlab Samples)

| ID | Nội dung đánh giá (tóm tắt) | Nhãn gốc | Đánh giá lại | Kết luận | Lý do |
|----|---------------------------|----------|-------------|----------|------|
| 11668 | Nội dung tích cực (“great movie”, “I loved it”) | 0 (negative) | Positive | Sửa nhãn (0 → 1) | Nội dung rõ ràng tích cực nhưng bị gán nhãn sai |
| 22259 | Nội dung tiêu cực (“bad”, “leaves something to be desired”) | 1 (positive) | Negative | Sửa nhãn (1 → 0) | Nội dung mang cảm xúc tiêu cực |
| 22257 | Có cả khen và chê nhưng thiên về tiêu cực | 1 (positive) | Negative | Sửa nhãn (1 → 0) | Tổng thể đánh giá tiêu cực |
| 16634 | Nội dung mỉa mai, vừa chê vừa nói “worth watching” | 0/1 | Không rõ | Ambiguous | Có yếu tố sarcasm, khó xác định |
| 31245 | Nội dung trung tính, chủ yếu mô tả | 0/1 | Không rõ | Ambiguous | Không thể hiện rõ cảm xúc |

---

**Kết luận:**
- Trong 5 mẫu được kiểm tra:
  - 3 mẫu bị gán nhãn sai → cần sửa
  - 2 mẫu mơ hồ → khó xác định chính xác
- Điều này cho thấy dataset tồn tại **label noise**, phù hợp với kết quả Cleanlab (~2% nghi vấn).