# Danh sách lớp v0 — Nguyễn Viết Minh Hoàng · G05

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | face (box) | một mặt tài xế mỗi khung hình | Tìm mặt người lái, cắt vùng cho các bước sau (điểm mặt, mắt, đầu) | Có; mặt nghiêng, đội mũ hoặc kính râm có thể bị che một phần |
| 2 | face13 (skeleton 13 điểm) | khóe ngoài/trong, mí trên/dưới mỗi mắt, mũi, 2 khóe miệng, môi trên/dưới | Nền để tính EAR, góc đầu, ngáp | Có, nhưng mắt chỉ cao khoảng 30 px nên điểm mí lệch vài px là EAR sai |
| 3 | eye_left / eye_right | open / closed / unknown | Phát hiện nhắm mắt lâu, buồn ngủ | Có, trừ khi kính phản xạ LED hoặc kính râm che mắt thì ghi unknown |
| 4 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Biết tài xế đang nhìn đâu; nhìn gương khi chuyển làn là lái đúng, nhìn xuống đùi là mất tập trung | Hạn chế: gán theo vùng nhìn, không đoán bằng con ngươi trên ảnh IR |
| 5 | glasses | unknown / none / clear / sun | Chấm model theo điều kiện (kính râm thường yếu nhất), tách ca che mắt | Có; kính trong có đốm phản xạ, kính râm tùy loại có thể vẫn tối |
| 6 | hand (box) | whose (driver/passenger), side (left/right của chính người đó), on_wheel (unknown/yes/no) | Phát hiện tay rời vô lăng, tay cầm vật | Có (hình dạng) |
| 7 | phone (box) | held / mounted / lap | Phát hiện mất tập trung do điện thoại; tách cầm tay với để trên giá để không báo nhầm | Có nhờ hình dạng, nhưng nhỏ và hay bị ngón tay che |
| 8 | camera_blocked | no / yes | Biết camera bị che hoặc dán băng dính, để hệ thống không im lặng sai | Có |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person (box) | seat: driver / front_passenger / rear_left / rear_middle / rear_right | Biết ghế nào có người; nền cho nhắc dây, chỉnh túi khí | Có; hàng ghế sau xa đèn nên tối, vẫn phải gán nếu nhận ra người |
| 2 | seatbelt (thuộc tính của person) | unknown / worn_correct / worn_incorrect / not_worn | Nhắc thắt dây, phát hiện đeo sai (dưới nách, sau lưng) | Có nhờ hình dạng và mép vải; dây mảnh, trùng màu áo thì mờ |
| 3 | child_seat (box) | seat; occupied: unknown / no | Biết ghế trẻ em đang trống hay có trẻ; điều kiện để cảnh báo trẻ bị bỏ quên | Có (hình dạng); bên trong bị chăn hoặc người che thì để unknown |
| 4 | infant_seat (box) | seat; facing: rear / front | Ghế em bé quay ngược gần như không thấy bên trong, cần tách riêng để dùng thêm radar | Có phần vỏ ghế; hướng lắp khó xác định khi bị che |
| 5 | object (box) | seat; type: bag / box / cup / other | Nhắc đồ bỏ quên; tránh nhầm túi, áo khoác với người | Có nhờ hình dạng, không nhận vật bằng màu |
| 6 | frame_meta (tag) | modality: ir / rgb; light: unknown / day / night; camera_blocked: no / yes | Cắt kết quả theo điều kiện, biết model yếu ở đâu | Có |
| 7 | face (box) cho người ngồi ghế sau | gaze_zone, eye_*, glasses | Hỗ trợ xác định có người sống ở ghế đó, và tư thế | Có nhưng yếu vì xa đèn; chỉ gán khi nhìn thấy |

## 2 câu hỏi leo thang

1. Câu hỏi: Khi ghế trẻ em có trẻ ngồi thì `child_seat.occupied` gán là gì? Schema v1 chỉ có `unknown` và `no`, trong khi slide 54 có `yes`.
   Khung ví dụ: S02 (ir/rgb), trẻ ngồi ở ghế trẻ em bên phải ảnh.
   Bạn tạm gán thế nào và vì sao: Tạm để `unknown` cho `child_seat` và gán riêng một box `person` cho trẻ cùng `seat`. Không gán `no` vì ghế không trống; không thể gán `yes` vì schema chưa có giá trị đó.

2. Câu hỏi: Khi có 2 hành khách trong cùng một khung, thuộc tính `hand.whose` chỉ có driver/passenger nên không biết tay của hành khách nào, và script kiểm tra báo lỗi "2 tay cùng side" vì đếm theo cả khung chứ không theo người.
   Khung ví dụ: S08 (ir/rgb), người lớn ở ghế sau và trẻ ở ghế bên cạnh.
   Bạn tạm gán thế nào và vì sao: Giữ nguyên side đúng của từng người (trái/phải của chính người đó, không theo phía ảnh). Để qua script, tạm bỏ box tay của người lớn, nên đây là cách làm tạm. Cần thêm thuộc tính `seat` hoặc id người cho `hand`.