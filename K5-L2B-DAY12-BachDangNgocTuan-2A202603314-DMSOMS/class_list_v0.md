# Danh sách lớp v0 — Bạch Đặng Ngọc Tuấn · G01

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_left / eye_right | open / closed / unknown | Phát hiện buồn ngủ (mắt nhắm lâu > ngưỡng cho phép - chỉ số PERCLOS) hoặc vi ngủ (microsleep) để cảnh báo tài xế nghỉ ngơi. | Có, camera NIR bắt độ mở khe mắt và phản xạ võng mạc rất tốt trong bóng tối, trừ khi bị đốm lóa kính râm che. |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện mất tập trung (nhìn xuống đùi, nhìn màn hình trung tâm quá lâu thay vì quan sát đường phía trước) khi xe đang di chuyển. | Có, dựa trên sự kết hợp giữa hướng xoay khuôn mặt và góc nhìn của đồng tử mắt. |
| 3 | glasses | none / clear / sun / unknown | Phân loại kính để hệ thống tự cân chỉnh thuật toán nhận diện mắt (tránh báo động giả khi mắt nằm sau tròng kính phản quang). | Có, NIR nhìn xuyên được phần lớn tròng kính râm và kính cận thông thường. |
| 4 | hand.on_wheel | yes / no / unknown | Giám sát việc buông tay lái (Hands-Off Detection) trong các tính năng tự lái cấp độ L2/L2+ (như giữ làn, bám đuôi xe trước). | Có, hình dạng bàn tay và bề mặt vô lăng phân tách rất sắc nét trên ảnh hồng ngoại. |
| 5 | phone.state | held / mounted / lap | Phát hiện hành vi sử dụng điện thoại trái quy định khi điều khiển xe (áp tai nghe gọi, cầm tay nhắn tin lướt mạng). | Có, nhận diện được hình chữ nhật phản xạ bề mặt đặc trưng của khung vỏ và màn hình điện thoại. |
| 6 | person.seatbelt (driver) | worn_correct / worn_incorrect / not_worn / unknown | Nhắc nhở tài xế thắt dây an toàn trước khi khởi hành và kích hoạt túi khí thích ứng đúng chuẩn an toàn khi xảy ra va chạm. | Có, dải dây đai có vật liệu phản xạ NIR khác biệt so với vải áo thông thường. |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person.seat | rear_left / rear_middle / rear_right | Đếm số lượng và xác định vị trí hành khách ngồi hàng ghế sau để điều chỉnh điều hòa đa vùng, tính toán tải trọng phanh và kích hoạt túi khí rèm. | Có, thân người lớn thể hiện rõ hình khối dưới camera IR. |
| 2 | person.seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Cảnh báo nhắc nhở hành khách hàng ghế sau thắt dây an toàn theo tiêu chuẩn an toàn Euro NCAP. | Có thể nhìn thấy dải chéo, tuy nhiên khó nhận diện hơn trên nền áo tối màu. |
| 3 | child_seat | occupied: yes / no / unknown | Nhận diện ghế trẻ em và trạng thái có người ngồi: cảnh báo bỏ quên trẻ em trên xe (Child Presence Detection - CPD) khi xe đã tắt máy. | Có, hình khối cấu trúc và đai an toàn của ghế trẻ em rất đặc trưng. |
| 4 | infant_seat | facing: rear / front | Xác định nôi xách em bé quay ngược hay quay xuôi để tự động ngắt túi khí ghế nhằm bảo vệ vùng đầu cổ của trẻ sơ sinh khi xảy ra va chạm. | Có, hình dạng tay xách và hướng nôi phân biệt rõ ràng trên IR. |
| 5 | object.type | bag / box / cup / other | Phát hiện hành lý, đồ vật để quên trên ghế khi hành khách rời xe; phát hiện vật thể nặng không được cố định có nguy cơ văng đập khi phanh gấp. | Có, nhận diện qua đường viền biên dạng hình học của vật thể. |
| 6 | frame_meta.camera_blocked | yes / no | Tự chẩn đoán lỗi cảm biến (Sensor Fault Detection): cảnh báo người lái khi camera giám sát cabin bị áo khoác hoặc đồ đạc vô tình che khuất. | Có, toàn bộ khung hình hoặc một phần camera bị tối đen/mất tín hiệu phản xạ. |

## 2 câu hỏi leo thang

1. **Câu hỏi:** Khi một đồ vật (như túi xách hoặc ba lô) được đặt nằm lọt thỏm ngay bên trong ghế trẻ em `child_seat`, quy tắc gán nhãn chuẩn nên ưu tiên gộp chung hay tách rời, và thuộc tính `occupied` của ghế trẻ em sẽ ghi nhận như thế nào nếu hệ thống chưa hỗ trợ nhãn riêng cho đồ chơi/vật dụng đi kèm?
   - **Khung ví dụ:** `S03_rgb.png` / `S03_ir.png` (ghế `rear_left`).
   - **Bạn tạm gán thế nào và vì sao:** Tạm thời gán 1 box `child_seat` (`occupied = yes` theo thông báo tại lớp của coach) và vẽ thêm 1 box `object` (`type = bag`, cùng `seat = rear_left`). Cách này giúp vừa bảo toàn thông tin về sự hiện diện của ghế trẻ em cho chức năng an toàn ghế, vừa giúp model nhận diện vật thể để quên bên trong.

2. **Câu hỏi:** Trong trường hợp tài xế đeo kính râm có lớp phủ phân cực/chống tia hồng ngoại khiến toàn bộ tròng kính bị đen kịt hoàn toàn dưới ánh sáng đèn NIR 940nm, hệ thống DMS nên ghi nhận vùng nhìn `gaze_zone` dựa theo hướng quay đầu (Head Pose) hay bắt buộc phải để `other/unknown`?
   - **Khung ví dụ:** `D05.png` (khuôn mặt tài xế nghiêng và đeo kính râm).
   - **Bạn tạm gán thế nào và vì sao:** Tạm thời gán `glasses = sun`, `eye_left = unknown`, `eye_right = unknown`, đánh cờ `occluded` cho toàn bộ các điểm mí/khóe mắt của `face13`, và để `gaze_zone = other`. Lý do là tuân thủ nghiêm ngặt nguyên tắc cốt lõi "Không thấy thì unknown", không suy đoán hướng nhìn của mắt khi đồng tử bị lớp tráng kính cản quang hoàn toàn.
