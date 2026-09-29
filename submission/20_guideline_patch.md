# Guideline patch

- **Rule mới đề xuất:** Khi vật chỉ thấy được phần đuôi hoặc hai bánh sau (không đủ đặc điểm để phân biệt chắc chắn Car với ThreeWheeler theo R04), người soát phải ghi finding với `why=E5_unresolved`, nêu rõ góc nhìn camera và lý do chưa chắc chắn, thay vì tự ý chọn một class mặc định.
- **Áp dụng cho:** class Car/ThreeWheeler, các vật ở xa hoặc góc khuất, chủ yếu ở zone center và mid.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R04 chỉ liệt kê ánh xạ tên xe (van→Car, minibus→Bus...) nhưng không hướng dẫn khi thiếu đặc điểm nhận dạng. Bằng chứng: finding round `calib`, object_ref `L7+R3` (xe chỉ thấy hai bánh sau, L gán Car còn R gán ThreeWheeler, chưa đủ bằng chứng kết luận bên nào sai); và finding round `r3_diag`, `adasind_117120.jpg L7` (ThreeWheeler không khớp cả reference lẫn model ở zone center).
- **`rules_version` mới:** v1.0.0 → v1.1.0
- **Hiệu lực từ:** round tiếp theo sau khi guideline được duyệt (áp dụng từ P2 của slice kế tiếp, không hồi tố cho B2-center đã khóa).