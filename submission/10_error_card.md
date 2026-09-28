# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B3 | MISSING | 4 |
| center | B3 | SPURIOUS | 3 |
| center | C0 | SPURIOUS | 1 |
| edge | B3 | MISSING | 2 |
| edge | B3 | SPURIOUS | 4 |
| edge | B3 | WRONG_CLASS | 2 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B3 | BOX_GEOMETRY | 1 |
| mid | B3 | IGNORE_SCOPE | 3 |
| mid | B3 | MISSING | 6 |
| mid | B3 | SPURIOUS | 4 |
| mid | C0 | MISSING | 1 |
| mid | C0 | WRONG_CLASS | 1 |

## Top defects
- MISSING: 13 (ví dụ frame adasind_019560.jpg)
- SPURIOUS: 12 (ví dụ frame adasind_019560.jpg)
- WRONG_CLASS: 4 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Hai lỗi có số dòng cao nhất là `MISSING` (13) và `SPURIOUS` (12), tiếp theo là `WRONG_CLASS` (4). Đây là số dòng finding qua nhiều round, không phải số vật thể duy nhất: cùng một đối tượng có thể xuất hiện trong compare và diagnostic hoặc có dòng riêng cho L/R/M. Vì vậy không diễn giải 13/12 thành tỷ lệ lỗi của slice.

- **Nguyên nhân khả dĩ:** Có ít nhất hai cơ chế khác nhau. Ở `B3-center / adasind_167700.jpg`, `R2+M7` (Bike) và `R8+M9` (Truck) cùng được reference và model định vị nhưng L không có box phù hợp; đây là bằng chứng mạnh cho hai lần bỏ sót của annotator theo R01. Ngược lại, nhiều `M_only` là dự đoán thừa/lệch của model, không phải bằng chứng rằng nhãn L sai. Cặp `L8/R6` Car/ThreeWheeler và `L4/R3` Car/Bus là bất đồng class ở rìa cần adjudication, không nên gộp thành lỗi chắc chắn của một bên.
- **Cách sửa / owner:** Rework hai box Bike và Truck sau khi kiểm ảnh gốc, owner `annotator`; giữ nhãn L khi chỉ model có box, owner theo dõi `ai_team`; chuyển hai xung đột class và box model chồng lấn cho QA adjudication, chưa sửa cho đến khi có quyết định. `L6/L7` ở frame 167700 và `L3` ở 212280 cần kiểm lại ignore scope theo R06–R09 trước khi dùng làm bằng chứng cho lỗi object.
- **Bằng chứng:** [Finding list](findings.csv), [local quality conflicts](r3_diag/local_quality_conflicts.csv), [model overlay](r3_diag/model_compare.html), [zone table](r3_diag/zone_table.md), R01/R04/R06–R09 trong `docs/02-rules-vi.md`. Ảnh chụp overlay: [adasind_167700](screenshots/adasind_167700_model_overlay.png) (hai box cần rework và xung đột rìa), [adasind_212280](screenshots/adasind_212280_model_overlay.png) (Car/Bus và box model). Các ảnh này là bằng chứng xem overlay, không thay ảnh gốc độ phân giải đầy đủ.

Giới hạn: ba frame của một slice ADASIND không đại diện toàn tập; teaching reference chưa phải gold set; local quality chỉ chấm rectangle H≥40 với matcher lab và IoU≥0.50, không chấm polygon/track. Precision/recall và các tổng trong card là mô tả theo quy tắc lab, không phải ước lượng production hay kết luận về bốn camera.
