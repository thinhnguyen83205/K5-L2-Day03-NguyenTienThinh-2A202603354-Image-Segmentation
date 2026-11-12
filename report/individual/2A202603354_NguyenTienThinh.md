# Báo cáo thực hành Day 3 — 2A202603354

Báo cáo ghi lại trạng thái ZIP và các vấn đề có thể xác minh từ file hiện có. Những chi tiết về thao tác cá nhân mà ZIP không lưu được được ghi rõ là chưa xác minh, không suy đoán thay người làm.

- Mã học viên theo lớp: 2A202603354
- Ngày / CVAT local: 12/11/2026 / CVAT local
- Công cụ đã dùng: CVAT

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Số ảnh dưới đây là số ảnh có trong ZIP export, không tự xác nhận mọi ảnh đã được gán nhãn đầy đủ. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Ảnh trong ZIP / ghi chú kiểm tra | Điểm tối đa (coach chấm sau) |
| --- | --- | --- | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 ảnh; có mask semantic | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 ảnh; 92 annotation COCO | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 ảnh; 2 annotation không có polygon/RLE hợp lệ | 30 |
| cp1_holes | `cp1_holes.zip` | 1 / 1 ảnh; 7 annotation, có hai annotation xe trùng vùng cần kiểm tra | 3 |
| cp2_slice | `cp2_slice.zip` | 1 / 1 ảnh; 18 annotation COCO | 3 |
| cp5_occlusion | `cp5_occlusion.zip` | 1 / 1 ảnh nhưng 0 annotation | 3 |
| cp3_thin | `cp3_thin.zip` | 1 / 1 ảnh; có mask semantic | 3 |
| cp4_curb | `cp4_curb.zip` | 1 / 1 ảnh; có mask semantic | 3 |
| cp6_coverage | `cp6_coverage.zip` | 1 / 1 ảnh; có mask semantic | 3 |
| **Tổng tối đa** | | | **100** |

Đã kiểm tra cấu trúc các ZIP. `hard_panoptic.zip` có annotation ID 1 (class `sky`) và ID 2 (class `car`) thiếu polygon/RLE hợp lệ. Trong `cp1_holes.zip`, annotation ID 4 và 5 cùng class `car`, bounding box, diện tích và RLE mask; đây là một annotation bị lặp trong export. `cp5_occlusion.zip` có ảnh nhưng không có annotation nên chưa thể xem là ảnh đã hoàn thành. Kiểm tra cấu trúc không xác nhận độ đúng của các mask.

## 2. Một quyết định trước khi dùng gợi ý

ZIP không lưu lịch sử thao tác nên không xác định được annotation nào là object đầu tiên tôi tự vẽ, hoặc tôi có dùng gợi ý tự động hay không. Để không suy đoán trải nghiệm, tôi ghi nhận giới hạn bằng chứng và một record có thể tra lại:

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: không xác định được từ ZIP. Record đầu tiên trong COCO export là annotation ID 1, class `person`, ảnh `000000181542.jpg`, bounding box `[597, 126, 16, 30]`; thứ tự export không chứng minh đây là object đầu tiên tôi tự vẽ.
- Class và quy tắc tôi dùng để chọn biên: chưa có dữ liệu lịch sử để xác nhận quy tắc tôi đã dùng cho object đầu tiên. Quy tắc của task là gán từng vật riêng và chỉ theo phần nhìn thấy.
- Nếu dùng gợi ý sau đó: ZIP không cho biết có dùng gợi ý hay không; cần tôi xác nhận từ trải nghiệm thực tế.
- Nếu không dùng gợi ý: cần tôi xác nhận điều này và nêu quyết định gán nhãn thực tế của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Qua kiểm tra ZIP, tôi phát hiện lỗi export nhưng chưa có bằng chứng cho thấy lỗi đã được sửa. Tôi ghi rõ trạng thái hiện tại thay vì nhận là đã sửa.

- Task/ảnh/vùng: `cp1_holes`, ảnh `000000144300.jpg`, vùng xe class `car` tại bounding box `[576, 142, 47, 36]`.
- Lỗi thuộc loại: thừa vật / annotation trùng có khả năng xảy ra.
- Bằng chứng tôi nhìn thấy: annotation ID 4 và 5 có cùng class, bounding box, diện tích và RLE mask nên là cùng một vùng xe được export hai lần.
- Quy tắc và hành động sửa: lỗi đã xác định nhưng chưa sửa trong ZIP. Cần mở task trong CVAT, xóa annotation trùng, Save và export lại COCO 1.0. Đồng thời kiểm tra hai annotation lỗi trong `hard_panoptic.zip` và task `cp5_occlusion` đang không có annotation.
- Sau sửa đã Save và export lại chưa? Chưa có ZIP mới để xác nhận đã sửa.

Scorecard tiers hiện có: 31.6/82 (Easy 9.2/20, Medium 21.7/32, Hard 0.7/30); đây là điểm tự đánh giá hiện tại, chưa phải kết quả sau khi sửa. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Ba điểm dưới đây được xác định khi đối chiếu ảnh và ZIP; ZIP không lưu lại việc tôi đã cân nhắc chúng trong lúc làm. Tôi cần xác nhận đây có phải các ca thực tế mình đã cân nhắc hay không.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| cp1_holes — ảnh `000000144300.jpg`, xe class `car` tại bbox `[576, 142, 47, 36]` | Hai annotation là hai xe khác nhau hay cùng một xe bị gán lặp? | Annotation ID 4 và 5 có cùng RLE mask, bbox và diện tích. Quy tắc task là mỗi vật là một instance riêng. | Export hiện tại ghi trùng cùng một vùng; xóa một annotation trong CVAT, Save và export lại. |
| cp2_slice — ảnh `000000017627.jpg`, các xe gần nhau | Các vùng xe sát nhau là hai instance hay một mask bị nối? | Ảnh có nhiều xe gần nhau; quy tắc task yêu cầu hai xe cùng class vẫn tách thành hai instance. ZIP có 18 annotation nhưng con số này không tự xác nhận các ranh đúng. | Rà lại từng xe và mask trong CVAT; không gộp chỉ vì cùng class hoặc đứng sát nhau. |
| cp5_occlusion — ảnh `000000336232.jpg`, xe vàng ở tiền cảnh và xe máy bên trái | Mask chỉ theo phần nhìn thấy hay kéo dài qua phần bị che/khuất? | Ảnh có các phương tiện chồng lấp; quy tắc task là không vẽ xuyên phần bị che. ZIP hiện có 0 annotation nên chưa kiểm chứng được cách gán nhãn. | Tạo/kiểm tra mask trong CVAT, chỉ gán phần nhìn thấy; giữ một instance cho mỗi vật bị che khuất. |
