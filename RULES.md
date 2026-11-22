# RULES — Lab Ngày 12



## 2. Ảnh ở yên trong lớp

1. Ảnh chỉ nằm trên máy bạn và trong CVAT local (`localhost`). Không tải lên Drive, GitHub, chatbot AI, hay CVAT online.
2. **Không chụp màn hình ảnh cabin gửi nhóm chat.** Hỏi bằng tên ảnh, ví dụ "G05 S03_ir, ghế trái ảnh".
3. File export (`.zip` CVAT 1.1 **không kèm ảnh**) chỉ chứa toạ độ và thuộc tính, nên đổi cho bạn qua USB, AirDrop hoặc LMS được.
4. Nếu dùng GitHub để nộp, `.gitignore` phải chặn `*.png`, `*.jpg`. Repo chỉ chứa XML/zip export, log, markdown.
5. Hết khóa, xóa thư mục `Gxx/` và chạy `docker compose down -v` nếu không cần giữ dữ liệu CVAT.

Lý do: SVIRO dùng giấy phép CC BY-NC-SA 4.0, còn Drive&Act chỉ cho phép dùng để học tập và nghiên cứu. Ảnh cabin chứa mặt người thật (Drive&Act).

## 3. Dùng AI

- **Được** hỏi AI về CVAT, Python, cách hiểu một khái niệm (NIR, gaze zone…), hoặc nhờ AI góp ý câu chữ của danh sách lớp.


## 4. Khi kẹt

1. Tra [COMMON_ERRORS.md](COMMON_ERRORS.md).
2. Hỏi bạn cùng mã (bằng tên ảnh).
3. Giơ tay hỏi coach. Ca guideline không nói tới: ghi vào ghi chú ca khó và chọn `unknown`/`other`, đừng tự đặt luật mới.

Đừng sửa XML bằng tay để qua `cabin_check`. Nếu export bị mất thuộc tính, báo coach và ghi vào báo cáo.

## 5. Nếu nộp qua GitHub (theo quy ước K5)

- Dù làm nhóm hay cá nhân, **mỗi người tự nộp repo của mình**: `K5-L2-DAY12-HoVaTen-MSSV-DMSOMS` (không dấu, không khoảng trắng). Nội dung repo giống thư mục nộp ở SUBMISSION.
- Mỗi người ít nhất 2 commit cho phần của mình.
- Nộp link repo hoặc file zip lên LMS: https://aithucchien.vinuni.edu.vn

## 6. Nộp muộn và sửa sau hạn

- Hạn nộp ghi ở [SUBMISSION.md](SUBMISSION.md). Coach thông báo trên LMS nếu có thay đổi về hạn nộp.
- Nộp sau hạn: bị trừ điểm theo quy định chung của khóa. Nộp muộn vẫn tốt hơn không nộp.
- Thiếu một trong E1–E5: coach ghi "chưa đủ bằng chứng" và hẹn bổ sung (RUBRIC). Chỉ nộp bổ sung đúng file được hẹn, trong thời hạn coach hẹn.
- Sau hạn, không sửa nhãn trong `export_final*.zip` đã nộp. Lỗi phát hiện thêm thì ghi vào `self_review.md` thay vì nộp lại export.
