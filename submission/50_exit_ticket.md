# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao? Cần policy seam riêng; không tự tính là `DUPLICATE`. Hai box là hai quan sát trên hai camera với hệ tọa độ, méo và góc nhìn khác nhau. Giữ camera ID/source box, rồi chỉ link/fuse nếu timestamp đồng bộ, calibration hợp lệ và output policy nói rõ cần hai observation hay một object hợp nhất.
2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera. Cùng camera, giữ ID khi evidence cho thấy cùng vật liên tục; thêm keyframe khi hình học/pose/thấy được thay đổi đủ lớn để biểu diễn, và gán Outside khi vật rời FOV thay vì kéo box/track ra ngoài ảnh. Nối qua camera chỉ sau khi có timestamp đồng bộ, intrinsics/extrinsics và overlap geometry đã kiểm, continuity evidence (appearance/motion/location) cùng policy output đích; ambiguous match cần adjudication, không ghép theo class đơn thuần.
3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm? Ở `B3-center / adasind_212280.jpg`, `L4` là Car còn `R3` là Bus; IoU 0.926 và model `M6` cũng ghi Car. Tôi không lấy đa số L+M làm chân lý; ghi `E5_unresolved`, escalation cho QA theo R04 và giữ ảnh overlay cùng evidence. Nếu làm lại, tôi sẽ ghi ngay dấu hiệu nhìn thấy để phân biệt van với minibus và kiểm ignore scope trước khi khóa, rồi xin review độc lập sớm hơn.
