# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `e6a7b8fb41ac3a02a5de0cee3fad7c35a675e7b127978d15b2e1b8352ca12533`; slice `B3-center`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_152940.jpg, adasind_167700.jpg, adasind_212280.jpg. Frame thiếu trong export: không.
TP=13; FP=2; FN=5; số lần đối chiếu=18; mean IoU của TP=0.838.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.722 | 0.935 | 0.889 |
| precision | 0.867 | 0.556 | 0.000 |
| recall | 0.722 | 0.604 | 0.000 |
| jaccard | 0.650 | 0.493 | 0.000 |
| dice | 0.788 | 0.548 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 7 | 0 | 1 | 0.944 | 1.000 | 0.875 | 0.875 | 0.933 |
| Bus | 0 | 0 | 1 | 0.944 | 0.000 | 0.000 | 0.000 | 0.000 |
| Car | 1 | 2 | 0 | 0.889 | 0.333 | 1.000 | 0.333 | 0.500 |
| Pedestrian | 2 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| ThreeWheeler | 0 | 0 | 2 | 0.889 | 0.000 | 0.000 | 0.000 | 0.000 |
| Truck | 3 | 0 | 1 | 0.944 | 1.000 | 0.750 | 0.750 | 0.857 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_152940.jpg | 5 | 0 | 1 | 0.833 | 1.000 | 0.833 |
| adasind_167700.jpg | 6 | 1 | 3 | 0.667 | 0.857 | 0.667 |
| adasind_212280.jpg | 2 | 1 | 1 | 0.667 | 0.667 | 0.667 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Bus | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|---:|
| Bike | 7 | 0 | 0 | 0 | 0 | 0 | 1 |
| Bus | 0 | 0 | 1 | 0 | 0 | 0 | 0 |
| Car | 0 | 0 | 1 | 0 | 0 | 0 | 0 |
| Pedestrian | 0 | 0 | 0 | 2 | 0 | 0 | 0 |
| ThreeWheeler | 0 | 0 | 1 | 0 | 0 | 0 | 1 |
| Truck | 0 | 0 | 0 | 0 | 0 | 3 | 1 |
| <extra> | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
