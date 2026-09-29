# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B2 | ATTRIBUTE | 1 |
| center | B2 | MISSING | 10 |
| center | B2 | SPURIOUS | 25 |
| center | C0 | SPURIOUS | 1 |
| edge | B2 | SPURIOUS | 1 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B2 | BOX_GEOMETRY | 1 |
| mid | B2 | MISSING | 3 |
| mid | B2 | SPURIOUS | 10 |
| unknown | C0 | IGNORE_SCOPE | 1 |

## Top defects
- SPURIOUS: 37 (ví dụ frame adasind_019560.jpg)
- MISSING: 13 (ví dụ frame adasind_062370.jpg)
- WRONG_CLASS: 1 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: Lỗi nổi bật nhất là SPURIOUS (37 ca), tập trung ở zone center (25/37) nhiều hơn hẳn mid (10/37) và edge (1/37). Phần lớn các ca này đến từ round r3_diag, cell L_only hoặc M_only: có 5 ca L_only (why=E5_unresolved, ví dụ adasind_062370.jpg L6, adasind_086220.jpg L5/L7/L9, adasind_117120.jpg L2/L4/L6/L7) nghi là box thừa do mình vẽ, và phần lớn còn lại là M_only (why=E4_model_domain) tức model tự báo thêm vật mà cả nhãn của mình và reference đều không thấy — đây là giới hạn của model, không phải lỗi nhãn theo R11. MISSING (13 ca) chủ yếu là LR_noM (người và reference đồng ý nhưng model bỏ sót, cũng why=E4_model_domain) và một số R_only (reference có nhưng nhãn mình không có, why=E1_annotator_error, ví dụ adasind_062370.jpg R7/R8 và adasind_086220.jpg R4).
- Cách sửa và ai nhận việc (`owner`): Các ca why=E4_model_domain (phần lớn SPURIOUS và MISSING) thuộc về owner=ai_team, không cần sửa nhãn, chỉ ghi nhận giới hạn model. Các ca why=E5_unresolved và E1_annotator_error
