# Tự đánh giá — Nguyễn Viết Minh Hoàng · G05

## 1. Tự rà soát 4 cảnh

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb | person (ghế sau trái) | box | Box ước lượng bằng mắt, gồm cả chân kéo ra mép ảnh nên lệch vài px; dây an toàn bị che nên để `seatbelt=unknown` thay vì đoán | Chưa, cần chỉnh lại box trên CVAT |
| S08_rgb | hand (người phụ nữ, ghế sau trái) | missing | Từng gán đúng (tay trái) nhưng bị xoá để qua lỗi "2 tay cùng side"; thực ra là script đếm theo cả frame, không theo từng người | Chưa, cần thêm lại box tay |
| D02 | hand ×2 (tài xế) | lr_flip | `side` suy ra từ bố cục ảnh xoay 90° (cửa ở dưới, console ở trên), chưa đối chiếu với nguồn nào khác; có thể bị đảo trái/phải | Chưa kiểm chứng |
| D04 | person (tài xế) | guess | Người đang cầm dây an toàn nhưng vẫn gán `worn_correct`; dây vắt qua thân nhưng chưa chắc đã cài đúng | Chưa, cân nhắc đổi sang `unknown` |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: `guess` — điền attribute (`light`, `seatbelt`, `side`) dựa trên suy đoán từ hình thay vì để `unknown` khi chưa đủ bằng chứng.

Vì sao  mắc: Mình tự suy `light` (day/night) từ độ sáng ảnh RGB trong khi đây là ảnh dựng SVIRO, nên 16 frame S bị script báo sai cùng lúc. Với `side` và `seatbelt` mình cũng chọn giá trị "nghe có lý" thay vì giá trị chắc chắn.

Lần sau tránh bằng cách: Đọc quy ước của bộ dữ liệu trước khi gán attribute (ảnh dựng thì `light=unknown`), chỉ gán khi nhìn thấy rõ, còn lại để `unknown`. Chạy script kiểm tra trước khi upload và rà lại các attribute đã đoán.

## 3. Ghi chú về disagreement_log
