# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

# Exit ticket

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao?

Đây không phải lỗi DUPLICATE. DUPLICATE (theo cách hiểu trong bài) là hai box thừa cho cùng một vật do một người
vẽ nhầm hai lần trên cùng một ảnh của cùng một camera. Còn ở vùng seam, hai camera thật có vùng nhìn chồng lên
nhau nên **đúng theo thiết kế vật lý** là cùng một vật xuất hiện trên cả hai camera cùng lúc, với hai zone bán
kính khác nhau (có thể `edge` ở camera này, `mid` ở camera kia). Đây cần một quy tắc riêng cho seam: xác định vật
nào đang ở vùng chồng, quyết định giữ một box (sau khi hợp nhất) hay giữ cả hai box cho tầng xử lý sau, dựa trên
timestamp, calibration và policy output, chứ không tự ý xoá bớt một box vì tưởng là trùng lặp.

2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera.

Trên cùng một camera: giữ nguyên track ID khi vật còn quan sát được liên tục qua các frame. Thêm một keyframe khi
hình học của vật thay đổi lớn (đổi hướng, đổi kích thước rõ rệt, hoặc bị che/lộ ra thêm) để track phản ánh đúng
vị trí thật ở từng thời điểm. Chuyển trạng thái Outside khi vật ra khỏi trường nhìn của camera đó.

Để nối track qua hai camera (ví dụ vật đi từ camera trái sang camera trước), cần có trước: timestamp đồng bộ giữa
hai camera (để biết cùng một khoảnh khắc), calibration của cả hai camera (để biết cùng một vật trong không gian
thật), và một chính sách rõ ràng về output đích (một track hợp nhất hay giữ hai track riêng có liên kết). Thiếu
một trong ba thứ này thì không nên tự ghép track hay xoá box, mà giữ nguyên hai box riêng và ghi escalate.

3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm?

Ở frame adasind_019560.jpg (P1, C0), object_ref L7+R3: xe ở xa, chỉ thấy hai bánh sau, mình gán Car còn
reference gán ThreeWheeler (finding round calib, why=E5_unresolved, rule_id R04). Mình không tự sửa nhãn theo
reference ngay, vì R04 chỉ nói cách ánh xạ tên xe khi đã nhận diện được loại xe, không nói phải làm gì khi thiếu
đặc điểm nhận dạng; ép theo reference lúc đó sẽ là đoán, không phải áp rule. Mình ghi finding với action=
keep_with_reason, nêu rõ lý do chưa đủ bằng chứng, và đề xuất sửa guideline (20_guideline_patch.md) để lần sau có
hướng dẫn rõ hơn cho ca thiếu đặc điểm nhận dạng, thay vì để mỗi người tự đoán khác nhau.

Nếu làm lại slice này, mình sẽ chụp thêm ảnh cận cảnh phần đầu xe trước khi quyết định class, thay vì chỉ nhìn
một frame duy nhất; và sẽ hỏi rule ignore_region reason=unreadable sớm hơn thay vì để đến P4 mới xem lại.