# Tự đánh giá — Bạch Đặng Ngọc Tuấn · G01

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S02_rgb.png | person, infant_seat | ok | Vị trí ghế `rear_right` và `rear_left` đúng chuẩn xe, hộp sát mép | Có |
| S06_ir.png | child_seat, infant_seat | ok | Đã có đầy đủ tag `frame_meta` (modality=ir, light=unknown), nhãn ghế chuẩn | Có |
| D01.png | person, face, face13, hand | ok | Mắt trái có y lớn hơn (ảnh xoay 90°), tay trên vô lăng `on_wheel=yes` chính xác | Có |
| D04.png | face, face13, hand | ok | Điểm mắt bên phải khuất góc quay nghiêng đã đánh cờ `outside` thay vì ước lượng mò | Có |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

- **Lỗi:** Quên tạo tag `frame_meta` ngay đầu mỗi frame, và nhầm thuộc tính `modality = rgb` trên ảnh camera NIR của tài xế (`D01`–`D06`).
- **Vì sao mình mắc:** Do phản xạ ban đầu tập trung ngay vào việc vẽ bounding box cho người và vật thể; đồng thời thấy ảnh ban ngày hoặc ảnh đen trắng rõ nét thì theo quán tính gán nhầm sang modality `rgb`.
- **Lần sau tránh bằng cách:** Áp dụng nghiêm ngặt quy trình 4 bước của GUIDE §4.3: Luôn gắn tag `frame_meta` trước tiên cho mọi khung hình, kiểm tra tiền tố tên file (`D##` và đuôi `_ir` luôn bắt buộc là `ir`).

## 3. Ghi chú về disagreement_log

- **Một dòng bạn của mình đúng và mình sai:** Dòng `D01.png` - `frame_meta.modality` (bạn gán `ir`, mình gán `rgb`).
- **Mình học được gì từ dòng đó:** Mình nhận ra rằng dù ảnh nhìn sáng rõ như ảnh đơn sắc ban ngày, camera DMS trong Drive&Act thực chất là cảm biến cận hồng ngoại (NIR 850/940nm) chuyên dụng để ghi hình buồng lái. Việc nhận thức đúng modality là cực kỳ quan trọng để dữ liệu đầu vào không bị huấn luyện sai lệch tính chất quang học của cảm biến. Mình đã cập nhật toàn bộ sang `ir` ở phiên bản `export_final_v2.zip`.
