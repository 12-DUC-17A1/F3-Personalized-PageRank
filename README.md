# F3 — Ứng dụng Personalized PageRank trong khuyến nghị kết nối trên mạng xã hội

Đồ án học phần **Hệ khuyến nghị** — Trường Đại học Kinh tế - Kỹ thuật Công nghiệp (UNETI).
Sinh viên: Đặng Minh Đức — 23174600031 — DHKL17A1HN.

## Bài toán
Gợi ý cho mỗi người dùng 10 người nên kết bạn, chỉ dựa trên cấu trúc mạng quan hệ bạn bè (bài toán dự đoán liên kết).

## Dữ liệu
SNAP Social Circles: Facebook (`data/facebook_combined.txt`) — 4.039 người dùng, 88.234 quan hệ bạn bè.
Nguồn: https://snap.stanford.edu/data/ego-Facebook.html

## Phương pháp
- **Mô hình:** Personalized PageRank, π = α·e_q + (1 − α)·Pᵀπ, với α là xác suất restart (Chương 11 tài liệu học tập).
- **Baseline:** Common Neighbors, Jaccard Coefficient, Adamic-Adar.
- **Đánh giá:** edge holdout 80/20 có giữ cây khung ngẫu nhiên trong train; Precision@10, Recall@10, NDCG@10 (Chương 8); α chọn bằng tập validation.

## Kết quả sơ bộ (một lần chia, seed = 42)

| Phương pháp | Precision@10 (%) | Recall@10 (%) | NDCG@10 |
|---|---|---|---|
| Common Neighbors | 37,04 | 48,86 | 0,5978 |
| Jaccard | 35,05 | 43,46 | 0,5513 |
| Adamic-Adar | 37,97 | 50,51 | 0,6150 |
| PPR, α = 0,1 | 31,43 | 41,55 | 0,5135 |
| **PPR, α = 0,7 (chọn bằng validation)** | **38,55** | **51,45** | **0,6255** |

## Cách chạy
```
pip install numpy scipy pandas matplotlib networkx
```
Mở `f3_ppr.ipynb` và chọn **Run All** (khoảng 1–2 phút). Notebook sinh ra hai hình `hinh_*.png` và hai bảng `ket_qua_*.csv`.

## Cấu trúc thư mục
```
f3_ppr.ipynb                  notebook chính
data/facebook_combined.txt    dữ liệu
hinh_phan_phoi_bac.png        phân phối số bạn bè
hinh_khao_sat_alpha.png       ảnh hưởng của α
ket_qua_so_bo.csv             bảng so sánh sơ bộ
ket_qua_khao_sat_alpha.csv    kết quả khảo sát α
```
