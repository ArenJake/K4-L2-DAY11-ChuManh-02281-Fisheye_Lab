# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 10 | 1 | 0 | 2 | 3 | MISSING (1) |
| mid | 6 | 2 | 0 | 3 | 4 | MISSING (2) |
| edge | 2 | 2 | 2 | 2 | 3 | WRONG_CLASS (2) |

## Nhận xét

- L gãy rõ nhất ở edge: chỉ `n_ref=2` nhưng có 2 missing và 2 spurious; center có 1 missing/0 spurious và mid có 2/0. Với M, mid có số lỗi tuyệt đối cao nhất (3 missing, 4 thừa), còn edge không ghép được box nào (2 missing, 3 thừa trên `n_ref=2`).
- Méo và cắt cụt ở rìa có thể làm box khó bám phần nhìn thấy; các conflict `Car`/`ThreeWheeler` và `Car`/`Bus` cũng cần phân xử theo ảnh gốc và R04. Self-QC còn ghi thiếu `ego_body` ở hai frame, nên cần kiểm scope/ignore trước khi quy nguyên nhân cho nhãn. Đây chỉ là ba frame của `B3-center`, số đếm edge rất nhỏ; `center/mid/edge` là khoảng cách tương đối tới tâm vòng kính, không nói vật gần/xa xe hay camera trước/sau và không đại diện toàn bộ tập.
