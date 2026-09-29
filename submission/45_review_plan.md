# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| adasind_086220.jpg | 5 SPURIOUS (L5, L7, L9, L1+M7, L4+M8) và 1 MISSING đã escalate (R4) | Frame có nhiều lỗi SPURIOUS nhất và có ca escalate chưa giải quyết; zone center của frame này đóng góp phần lớn vào 25/37 ca SPURIOUS toàn slice | Ảnh gốc frame, overlay box R4 so với reference, các dòng r1_craft/r3_diag liên quan trong findings.csv |
| adasind_117120.jpg | 4 SPURIOUS L_only (L2, L4, L6, L7) và 2 LR_noM | Nhiều ca ranh giới Car/ThreeWheeler/Bus chưa rõ (liên quan đề xuất sửa R04); cần thống nhất cách đọc trước khi áp dụng cho slice khác | Ảnh gốc frame, dòng L7 trong model_compare.md, các dòng r3_diag tương ứng |

Giới hạn của kết luận từ ba frame ADASIND: Ba frame không đủ đại diện cho phân bố lỗi thật của 50.000 frame hay của cả bốn camera SVM. Số liệu trên chỉ phản ánh đúng slice B2-center của mình, dùng để tập luyện quy trình review, không dùng để suy ra tỷ lệ lỗi hay xếp hạng camera nào tốt hơn.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv`: kiểm tra tổng theo từng camera và từng loại normal/hard đã đúng như phân bổ đề xuất, đồng thời xem lại danh sách frame được chọn (nếu có) để tránh nhiều frame liền kề của cùng một cảnh bị tính là nhiều ca độc lập — ví dụ nhiều frame liên tiếp quay cùng một ngã tư chỉ nên tính là một ca, không phải nhiều ca hard riêng biệt. Kế hoạch 200 frame này chỉ giúp tìm ra ca cần soi kỹ (dựa trên rủi ro và loại khó), chưa đo được tỷ lệ lỗi thật của cả tập 50.000 frame, vì mẫu chưa qua kiểm chứng và chưa có gold set đã phê duyệt để so sánh.