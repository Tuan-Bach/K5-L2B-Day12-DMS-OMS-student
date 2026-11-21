# Khai báo dùng AI — Bạch Đặng Ngọc Tuấn

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Antigravity AI Assistant | Hỗ trợ cấu hình Docker/CVAT local, nạp project Day12 và upload tự động 22 ảnh dataset G01 lên CVAT | Tạo task và nạp đúng 22 ảnh cốt lõi theo thứ tự | Kiểm tra giao diện CVAT và API `/api/tasks/38` |
| 2 | Antigravity AI Assistant | Giải thích quy tắc gọi tên ghế theo xe (trái ảnh là rear_right) và quy ước mắt trái trên ảnh D## xoay 90° | Định vị chính xác thuộc tính `seat` và trục y của tọa độ mắt trên ảnh | Tự kiểm tra bằng mắt theo hướng ngồi trong xe |
| 3 | Antigravity AI Assistant | Chạy script kiểm tra `cabin_check.py` để tìm lỗi tự động cho Checkpoint A, B và lần cuối | Phát hiện lỗi thiếu tag frame_meta và cảnh báo để sửa trực tiếp trong CVAT | Chạy lại `python scripts/cabin_check.py check` xác nhận 0 lỗi |
| 4 | Antigravity AI Assistant | Chạy lệnh `cabin_check.py diff` với file bạn gửi và hỗ trợ phân loại 103 dòng bất đồng | Điền đầy đủ verdict, guideline_rule và action vào `disagreement_log.csv` | Tự rà soát lại các dòng quan trọng theo GUIDE Cabin v1.0 |
| 5 | Antigravity AI Assistant | Góp ý và trau chuốt câu chữ cho bản phác thảo danh sách lớp `class_list_v0.md` | Hoàn thiện bảng chức năng an toàn xe cho 6 lớp DMS và 6 lớp OMS | Đối chiếu với slide bài giảng Ngày 12 |
