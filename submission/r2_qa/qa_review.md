# QA review · B2-center

Mã khóa: B214-53BB

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_117120.jpg | L9 | R03 | Pedestrian L9 nằm gọn trong box ThreeWheeler L7; cần kiểm tra trên ảnh người này ngồi trong xe hay đứng cạnh. Nếu ngồi trong xe thì không được có box riêng. |
| adasind_117120.jpg | L8 | R05 | Cờ occluded của CVAT bật nhưng thuộc tính occluded là false; hai giá trị chưa khớp, cần đối chiếu với ảnh xem xe có bị che không. |
| adasind_062370.jpg | L6 | R01 | Box Car cao khoảng 44 px, sát ngưỡng H=40; nếu box lỏng thì chiều cao thật có thể dưới 40 và không cần box. |
| adasind_086220.jpg | L9 | R03 | Box Bike nằm trọn trong box ThreeWheeler L3; cần xem trên ảnh đây là xe hai bánh riêng hay một phần của xe ba bánh. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.