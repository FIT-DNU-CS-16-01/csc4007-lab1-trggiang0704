# IMDB Review Dataset (as introduced in Maas et al., 2011)

> **Scope note:** This data card is filled **only from information stated in the paper**
> “Learning Word Vectors for Sentiment Analysis” (ACL 2011) and the dataset URL given in the paper.
> Whenever the paper does not provide enough detail, the field is marked **Not specified in the paper**.

---

# 🔷 Additional Audit Information (From Lab Analysis)

## Data Auditing Summary

- Total samples: 50,000  
- Label distribution: Balanced (25,000 positive, 25,000 negative)  

### Data Quality Issues Identified:
- **HTML artifacts:**  
  - BEFORE: 29,202 samples contained HTML tags  
  - AFTER: 0 (cleaned successfully)  

- **Duplicates:**  
  - 832 exact duplicates (~1.66%)  

- **Text length outliers:**  
  - Max length: 13,593 characters  
  - 6 samples exceed threshold (10,000)  

- **Label noise (Cleanlab):**  
  - ~2% samples suspected incorrect  
  - Review of top 5 samples:
    - 3 mislabeled → corrected  
    - 2 ambiguous  

- **Data leakage risk:**  
  - Risk if preprocessing is applied before splitting  

---

## Validation (Great Expectations)

- Evaluated expectations: 6  
- Passed: 5  
- Failed: 1  
- Success rate: 83.33%  

### Failure Details:
- Some samples exceed max text length constraint (10,000 characters)

---

## Labeling Quality (Cleanlab)

- Suspected noisy labels: ~2%  
- Causes:
  - Rating-based labeling mismatch with text  
  - Mixed sentiment  
  - Sarcasm  
  - Ambiguous/neutral tone  

---

## Transformations (Before vs After)

| Metric | BEFORE | AFTER |
|------|--------|-------|
| HTML tags | 29,202 | 0 |
| Max length | 13,704 | 13,593 |
| Duplicate count | 824 | 832 |

---

## Additional Risks (From Lab)

- Duplicate data → inflated performance  
- Label noise → reduced model accuracy  
- Outliers → unstable training  
- Leakage → invalid evaluation  

---

Write a short summary describing your dataset (limit
200 words). Include information about the content
and topic of the data, sources and motivations for the
dataset, benefits and the problems or use cases it is
suitable for.

The paper introduces a publicly released **IMDB movie review dataset** for sentiment analysis. The dataset contains **50,000 movie reviews** collected from IMDB, with an **even number of positive and negative reviews**. To focus on clear polarity classification, the dataset includes only **highly polarized reviews**: reviews with score **≤ 4/10** are labeled negative, and reviews with score **≥ 7/10** are labeled positive; **neutral reviews are excluded**. The dataset is evenly split into **25,000 training** and **25,000 test** reviews, and uses **disjoint sets of movies** for training and testing to reduce leakage from movie-specific words and repeated content patterns. The dataset was introduced as a **more robust benchmark** than smaller prior sentiment datasets and is suitable for **research on sentiment classification, benchmark evaluation, and sentiment-aware representation learning**.

#### Dataset Link
- Dataset page: http://www.andrew-maas.net/data/sentiment
- Paper: https://aclanthology.org/P11-1015.pdf

#### Data Card Author(s)
- **Student (Lab Author):** Data auditing, validation, and labeling analysis added based on lab results

---

## Dataset Overview (Extended with Lab Statistics)

#### Dataset Snapshot (Updated with Lab Results)

Category | Data
--- | ---
Number of Instances | 50,000 reviews
Labeled Classes | 2 (positive, negative)
Label Distribution | Balanced (25k / 25k)
Train/Test Split | 25k / 25k (lab split)
Max Length | 13,593 characters
Median Length | 954 characters
Duplicates | 832 (~1.66%)
HTML Artifacts | 0 after cleaning
Label Noise | ~2% suspected (Cleanlab)

---

## Transformations (Lab Processing)

### Cleaning
- Removed HTML tags (`<br/>`, etc.)
- Reduced HTML artifacts from 29k → 0

### Remaining Issues
- Duplicate data not removed  
- Long text outliers not truncated  

---

## Annotations & Labeling (Extended)

### Lab Findings
- Cleanlab identified ~2% suspicious labels  

### Label Review (Top 5 Cleanlab Samples)

| ID | Nội dung đánh giá (tóm tắt) | Nhãn gốc | Đánh giá lại | Kết luận | Lý do |
|----|---------------------------|----------|-------------|----------|------|
| 11668 | Nội dung tích cực (“great movie”, “I loved it”) | 0 (negative) | Positive | Sửa nhãn (0 → 1) | Nội dung rõ ràng tích cực nhưng bị gán nhãn sai |
| 22259 | Nội dung tiêu cực (“bad”, “leaves something to be desired”) | 1 (positive) | Negative | Sửa nhãn (1 → 0) | Nội dung mang cảm xúc tiêu cực |
| 22257 | Có cả khen và chê nhưng thiên về tiêu cực | 1 (positive) | Negative | Sửa nhãn (1 → 0) | Tổng thể đánh giá tiêu cực |
| 16634 | Nội dung mỉa mai, vừa chê vừa nói “worth watching” | 0/1 | Không rõ | Ambiguous | Có yếu tố sarcasm, khó xác định |
| 31245 | Nội dung trung tính, chủ yếu mô tả | 0/1 | Không rõ | Ambiguous | Không thể hiện rõ cảm xúc |

### Interpretation
Label noise exists due to:
- Rating-based labeling mismatch  
- Mixed sentiment reviews  
- Sarcasm  

---

## Validation Types (Extended)

### Great Expectations Result
- FAIL (83.33% pass rate)

### Reason
- Text length constraint violated (6 samples > 10,000 chars)

---

## Data Limitations (Extended)

- Contains label noise (~2%)  
- Contains duplicate data (~1.66%)  
- Contains extreme-length outliers  
- No neutral class  
- Sensitive to sarcasm and mixed sentiment  

---

## Intended Use (Extended)

- NLP research  
- Sentiment analysis  
- Benchmark evaluation  

---

## Not Recommended Use

- Production systems without further cleaning  
- Fine-grained sentiment tasks  
- Neutral sentiment classification  

---

(Rest of template remains unchanged — Not specified in the paper)