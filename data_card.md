# Data Card — IMDB Sentiment Dataset
Version: v1.0  
Date: 2026-04-08  

---

# 🔷 Module 0 — Foundational Questions

- **Ai sẽ đọc Data Card?**  
Sinh viên NLP, Machine Learning Engineer, và Researcher sử dụng dataset cho bài toán phân tích cảm xúc.

- **Họ cần quyết định gì?**  
Quyết định dataset có đủ chất lượng để huấn luyện mô hình hay không, có cần làm sạch thêm hay không.

- **Họ cần cảnh báo gì?**  
Dataset có thể chứa nhiễu nhãn (label noise), dữ liệu trùng lặp, outliers và rủi ro data leakage nếu xử lý sai pipeline.

---

# 🔷 Module 1 — ASK

## 👥 Agents
- NLP Students  
- Machine Learning Engineers  
- Researchers  

## 🔍 Lenses / Scopes
- Dataset Snapshot  
- Data Collection  
- Labeling & Annotation  
- Validation (Great Expectations)  
- Data Issues & Risks  
- Transformations  
- Intended Use & Limitations  

---

# 🔷 Module 2 — INSPECT

## ✔ Verified
- Dataset size, label distribution, text length: outputs/datacard_stats.json  
- Great Expectations result: outputs/ge/validation_summary.md  
- Cleanlab label issues: outputs/logs/cleanlab_summary.md  

## ⚠ Estimated
- Impact of label noise on model performance  
- Impact of duplicates on evaluation  

## ❓ To be measured
- Correlation between text length and label  
- Bias across sentiment intensity  

---

# 🔷 Module 3 — ANSWER

## 📊 Dataset Snapshot

- Total samples: 50,000  
- Label distribution:  
  - Negative (0): 25,000  
  - Positive (1): 25,000  
- Data split:  
  - Train: 40,000  
  - Validation: 5,000  
  - Test: 5,000  

### Text length:
- Min: 32  
- Median: 954  
- P95: 3,328  
- Max: 13,593  

---

## 📥 Data Collection

Dataset được thu thập từ các bài review phim trên IMDb.  
Nhãn được suy ra từ rating của người dùng:
- Rating ≥ 7 → Positive  
- Rating ≤ 4 → Negative  

Các review trung tính bị loại bỏ.

---

## 🏷️ Labeling & Annotation

Kết quả từ Cleanlab cho thấy dataset tồn tại **label noise**.

### Review 5 mẫu nghi vấn:
- 3 mẫu bị gán nhãn sai → cần sửa  
- 2 mẫu mơ hồ → ambiguous  

### Nguyên nhân:
- Nhãn được suy ra từ rating, không phải đọc nội dung  
- Có trường hợp:
  - Nội dung khen/chê lẫn lộn  
  - Sarcasm (mỉa mai)  
  - Nội dung trung tính  

👉 Điều này gây ra sự không nhất quán giữa text và label.

---

## ✅ Validation (Great Expectations)

- Evaluated expectations: 6  
- Passed: 5  
- Failed: 1  
- Success rate: 83.33%  

### Nguyên nhân fail:
- Một số mẫu có độ dài > 10,000 ký tự (max = 13,593)  

### Ý nghĩa:
- Tồn tại outliers về độ dài văn bản  

---

## ⚠️ Data Issues & Risks

### 1. HTML noise
- BEFORE: 29,202 samples chứa HTML  
- AFTER: 0  
→ Đã được xử lý

---

### 2. Duplicate data
- ~1.65% dữ liệu bị trùng  
→ Có thể gây “điểm cao ảo”

---

### 3. Data leakage risk
- Nếu fit preprocessing trước khi split  
→ kết quả evaluation không đáng tin  

---

### 4. Text length outliers
- Max length: 13,593  
→ Có thể gây bias và tăng chi phí tính toán  

---

### 5. Label noise
- ~2% dữ liệu bị nghi vấn  
→ ảnh hưởng đến độ chính xác mô hình  

---

## 🔄 Transformations

| Metric | BEFORE | AFTER |
|------|--------|-------|
| HTML tags | 29,202 | 0 |
| Duplicate | 824 | 832 |
| Max length | 13,704 | 13,593 |

👉 Cleaning giúp loại bỏ HTML nhưng chưa xử lý duplicate và outliers.

---

## 🎯 Intended Use

- Huấn luyện mô hình sentiment analysis  
- Nghiên cứu NLP  
- Bài tập học máy  

---

## ⚠️ Limitations

- Có label noise  
- Có duplicate  
- Không có neutral class  
- Có sarcasm khó xử lý  
- Không phù hợp cho production nếu chưa clean thêm  

---

# 🔷 Module 4 — AUDIT

| Criteria | Score |
|--------|------|
| Completeness | 4/5 |
| Accuracy | 5/5 |
| Clarity | 5/5 |
| Timeliness | 5/5 |
| Actionability | 4/5 |

### Ghi chú:
- Data Card đầy đủ nhưng có thể cải thiện thêm phân tích bias và cleaning.

---