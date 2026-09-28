# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.


| camera_id | Hard case cần chọn                                                                | Vì sao dễ sai                                                                   | Annotation space / calibration cần giữ                                                        | Cách review trước khi gọi là gold                                                                      |
| --------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| front     | Người đi bộ và xe hai bánh ở xa hoặc sát rìa ảnh; vật bị che một phần bởi xe khác | Vật nhỏ dưới ngưỡng 40 px dễ bị bỏ sót; ranh giới occluded và truncated dễ nhầm | Nhãn trên ảnh fisheye gốc, chưa nắn thẳng; giữ calibration của camera trước và phiên bản rule | Hai người review độc lập trên camera front, đối chiếu xung đột rồi một người thứ ba quyết định ca lệch |
| rear      | Vật thấp hoặc sát thân xe khi lùi; xe đỗ dày đặc trong bãi                        | Vật thấp dễ bị che bởi thân xe ego; nhiều xe sát nhau khó tách box              | Giữ vùng ego_body và lens_border theo đúng góc lắp camera sau                                 | Review riêng cho camera sau; kiểm từng ca ego_body và ignore_region trước khi khóa                     |
| left      | Người và xe hai bánh sát thân xe; cột, tường sát lề                               | Méo mạnh ở mép ảnh làm box lệch; rider và xe hai bánh dễ tách nhầm              | Giữ calibration camera trái; không dùng chung ngưỡng méo với camera khác                      | Review riêng camera trái, ưu tiên ca ở vùng edge; ghi rõ lý do mỗi ca giữ nhãn                         |
| right     | Vật bị cắt ở biên ảnh và vùng loại trừ; nhóm đông người hoặc xe                   | Dễ nhầm truncated với occluded; nhóm đông khó quyết định ignore hay box riêng   | Giữ calibration camera phải và chính sách                                                     |                                                                                                        |


