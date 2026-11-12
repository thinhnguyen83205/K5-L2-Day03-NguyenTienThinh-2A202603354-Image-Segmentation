# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603354
- Ngày / CVAT local: 12/11/2026 / CVAT local
- Công cụ đã dùng: CVAT

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` (cần sửa export) | 2 / 2, nhưng 2 annotation lỗi mask | 30 |
| cp1_holes | `cp1_holes.zip` | 1 / 1 | 3 |
| cp2_slice | `cp2_slice.zip` | 1 / 1 | 3 |
| cp5_occlusion | `cp5_occlusion.zip` (chưa có annotation) | 0 / 1 | 3 |
| cp3_thin | `cp3_thin.zip` | 1 / 1 | 3 |
| cp4_curb | `cp4_curb.zip` | 1 / 1 | 3 |
| cp6_coverage | `cp6_coverage.zip` | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Kiểm tra ZIP: `hard_panoptic.zip` có 2 annotation thiếu polygon/RLE hợp lệ; cần kiểm tra và export lại từ CVAT. `cp5_occlusion.zip` có 1 ảnh nhưng 0 annotation; chưa thể tính là ảnh đã làm. Các ZIP còn lại có dữ liệu theo kiểm tra cấu trúc; việc này không xác nhận độ đúng của mask.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: [CHƯA CÓ THÔNG TIN — BỔ SUNG TRẢI NGHIỆM THỰC TẾ]
- Class và quy tắc tôi dùng để chọn biên: [CHƯA CÓ THÔNG TIN — BỔ SUNG QUY TẮC ĐÃ DÙNG]
- Nếu dùng gợi ý sau đó: [CHƯA CÓ THÔNG TIN — GHI CÁCH XỬ LÝ; NẾU KHÔNG DÙNG, GHI “KHÔNG DÙNG” VÀ MỘT QUYẾT ĐỊNH THỰC TẾ]
- Nếu không dùng gợi ý: ghi “không dùng” và nêu một quyết định gán nhãn thực tế của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: hard_panoptic, annotation 1 và 2 trong ZIP export.
- Lỗi thuộc loại: khác — annotation thiếu polygon/RLE hợp lệ.
- Bằng chứng tôi nhìn thấy: công cụ kiểm tra ZIP báo hai annotation không có mask polygon/RLE hợp lệ.
- Quy tắc và hành động sửa: chưa sửa; cần mở task Hard trong CVAT, kiểm tra mask của hai annotation, Save và export lại COCO 1.0.
- Sau sửa đã Save và export lại chưa? Chưa; ZIP hiện tại vẫn cần sửa.

Scorecard tiers hiện có: 31.6/82 (Easy 9.2/20, Medium 21.7/32, Hard 0.7/30); đây là điểm tự đánh giá hiện tại, chưa phải kết quả sau khi sửa. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | [CHƯA CÓ THÔNG TIN — TASK/ẢNH/VÙNG] | [HAI CÁCH HIỂU THỰC TẾ] | [CHỨNG CỨ, QUY TẮC VÀ QUYẾT ĐỊNH/CÂU HỎI] |
| 2 | [CHƯA CÓ THÔNG TIN — TASK/ẢNH/VÙNG] | [HAI CÁCH HIỂU THỰC TẾ] | [CHỨNG CỨ, QUY TẮC VÀ QUYẾT ĐỊNH/CÂU HỎI] |
| 3 | [CHƯA CÓ THÔNG TIN — TASK/ẢNH/VÙNG] | [HAI CÁCH HIỂU THỰC TẾ] | [CHỨNG CỨ, QUY TẮC VÀ QUYẾT ĐỊNH/CÂU HỎI] |
