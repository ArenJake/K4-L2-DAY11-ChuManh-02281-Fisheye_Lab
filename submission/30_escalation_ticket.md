# Escalation ticket

## Ticket 1

- **Frame:** `B3-center / adasind_212280.jpg`, object `L4+R3` (local-quality: Car so với Bus, IoU 0.926; model `M6` cũng dự đoán Car).
- **Ảnh chụp:** [model overlay](screenshots/adasind_212280_model_overlay.png); đối chiếu thêm ảnh nguồn `assets/images/adasind_212280.jpg` ở độ phân giải gốc.
- **Expected impact:** Nếu class sai, local-quality tính một FP cho class đang vẽ và một FN cho class tham chiếu; precision/recall theo `Car` và `Bus` bị ảnh hưởng. Hiện chỉ là một object trong slice ba frame, chưa chứng minh lỗi taxonomy phổ biến hay rủi ro production.
- **Owner:** `qa` adjudicator; guideline owner tham gia nếu dấu hiệu nhìn thấy không đủ để áp dụng R04.
- **Recommendation:** Chưa rework. Hai reviewer độc lập xem ảnh gốc (không chỉ overlay/model), ghi dấu hiệu thân xe đủ phân biệt passenger van `Car` với minibus `Bus` theo R04; adjudicator ghi quyết định và evidence vào `findings.csv`/`40_decision_log.csv`. Nếu crop không cho phép phân biệt, giữ `E5_unresolved`, yêu cầu kiểm data/source hoặc áp dụng quy tắc đề xuất R12 sau khi được duyệt; không dùng phiếu đa số L/R/M làm ground truth.
