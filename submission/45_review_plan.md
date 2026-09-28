# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `B3-center / adasind_167700.jpg` | 2 `IGNORE_SCOPE` (L6/L7), 2 `MISSING` (R2 Bike, R8 Truck), 1 `WRONG_CLASS` (L8/R6 Car vs ThreeWheeler); attribute conflicts cũng được ghi trong local-quality | Nhiều loại lỗi cùng frame; hai vật bị thiếu có hỗ trợ độc lập từ reference và model, còn ignore scope có thể ảnh hưởng cách đọc box. Class rìa vẫn cần người phân xử, không coi reference là gold. | [Model overlay](screenshots/adasind_167700_model_overlay.png), [compare](r1_craft/compare.md), [local conflicts](r3_diag/local_quality_conflicts.csv), ảnh gốc `assets/images/adasind_167700.jpg`; ghi kết quả adjudication vào findings/decision log. |
| `B3-center / adasind_212280.jpg` | 1 `IGNORE_SCOPE` (L3), 1 `WRONG_CLASS` Car/Bus (L4/R3; IoU 0.926), thêm model-only boxes quanh vật thể rìa | Kiểm cùng lúc R04 class mapping và ranh giới ignore; model Car đồng ý với L nhưng không phân xử được reference Bus. | [Model overlay](screenshots/adasind_212280_model_overlay.png), [local conflicts](r3_diag/local_quality_conflicts.csv), ảnh gốc `assets/images/adasind_212280.jpg`; second reviewer ghi class cues và quyết định. |

Giới hạn: đây là hai frame trong một slice ba frame, cùng `B3-center`; chúng được chọn vì có finding đáng xử lý, không phải mẫu ngẫu nhiên. Kết quả hữu ích để tìm lỗi và lên việc rework, không ước lượng prevalence, không đại diện các zone/camera khác và không xác nhận chất lượng model hay reference trên ADASIND nói chung.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập): kiểm đủ đúng tám ô camera × normal/hard, xác minh tổng 200, rồi lập manifest gồm camera, session/route, timestamp, điều kiện sáng/thời tiết, scenario tag và lý do chọn. Chọn từ nhiều session và khoảng thời gian tách nhau; đặt trần số frame cho cùng một event/scene; review riêng các hard-case như seam, occlusion, glare, low light và vulnerable road users. So sánh độ phủ với taxonomy/risk list cho từng camera và ghi rõ ô nào còn thiếu; nếu một ô thiếu scenario đa dạng, chọn thêm session thay vì lấy burst frame kề nhau.

Phân bổ hiện tại là risk-enriched planning, không phải random sample có inclusion probability đã định. Nó giúp tìm tình huống khó nhưng không cho tỷ lệ lỗi không chệch; muốn ước lượng prevalence cần frame sampling frame, xác suất chọn biết trước, nhãn adjudicated và trọng số theo population/scene.
