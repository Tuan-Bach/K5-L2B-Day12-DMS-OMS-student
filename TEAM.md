# TEAM — Ngày 12

Mã bộ ảnh: **G01** · Hình thức: **cá nhân**

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Bạch Đặng Ngọc Tuấn | 2A202603314 | có | Bạn cùng lớp (Mã G01) | 103 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- **`S03` & `S05` (`child_seat.occupied`):** Bạn để `unknown` theo đúng văn bản guideline gốc, mình để `yes` theo thông báo cập nhật trực tiếp tại lớp của Coach. Cả hai đã trao đổi và thống nhất ghi nhận điểm khác biệt này vào `disagreement_log.csv`.
- **`D01`–`D06` (`frame_meta.modality`):** Ban đầu mình để `rgb` cho chuỗi ảnh tài xế, sau khi review chéo thấy bạn chọn `ir` là hoàn toàn chính xác theo GUIDE §4.3 (ảnh hồng ngoại NIR). Mình đã đồng ý và cập nhật lại bài gán sang phiên bản `v2`.

## Cá nhân

### BachDangNgocTuan-2A202603314
- **Phần mình làm:** Tự hoàn thiện gán nhãn 22 khung hình cho bộ mã `G01` trên CVAT local; chạy script `cabin_check.py` đạt 0 lỗi ở cả 2 Checkpoint A, B và lần cuối; thực hiện `diff` và phân tích toàn bộ 103 dòng bất đồng với file của bạn ghép cặp; cập nhật sửa đổi sang bản `v2`.
- **Điều mình học được hôm nay:** 
  1. Hiểu sâu sắc nguyên tắc "Không thấy thì unknown" trong gán nhãn dữ liệu xe tự hành, không được phỏng đoán dựa trên cảm tính.
  2. Nắm rõ sự khác nhau giữa ảnh cận hồng ngoại thật (NIR thật 940nm trên Drive&Act) và ảnh hồng ngoại mô phỏng (IR-sim trên SVIRO).
  3. Thành thạo quy ước gọi vị trí ghế theo chiều chuyển động của xe (trái ảnh là `rear_right`), độc lập với hướng đặt camera.
