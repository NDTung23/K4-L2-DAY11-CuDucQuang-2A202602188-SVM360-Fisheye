# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.


| Zone   | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
| ------ | ----- | --------- | ---------- | ------------------------------- | ---------------------------- | -------------------- |
| center | 13    | 3         | 7          | 7                               | 10                           | SPURIOUS (7)         |
| mid    | 6     | 0         | 3          | 3                               | 5                            | SPURIOUS (3)         |
| edge   | 1     | 0         | 0          | 0                               | 1                            | —                    |


## Nhận xét

## Nhận xét

- Zone center gãy nhiều nhất ở cả hai phía: L spurious 7/13 và M thiếu 7, M thừa 10 (so với mid: L spurious 3/6, M thiếu 3, M thừa 5; edge gần như không có vấn đề). Center là nơi vật gần và dày đặc nhất trong ba frame của mình.
- Giả thuyết: (1) IoU sweep cho thấy số L khớp giảm từ 10 xuống 8 ở center khi tăng ngưỡng từ 0.5 lên 0.7, nghĩa là một số box của mình lỏng hơn vật thật chứ không hẳn sai hoàn toàn; (2) nhiều box Car nhỏ ở center bị lệch loại (precision Car chỉ 0.400, 6/10 box Car không khớp reference) có thể do xe ở xa, hình dạng mờ, dễ nhầm Car với ThreeWheeler hoặc Bus theo R04; (3) model M cũng gãy mạnh ở center (M thừa 10, M thiếu 7), cho thấy đây có thể là vùng khó chung, không riêng gì nhãn của mình. Giới hạn: ba frame không đủ để suy rộng, mọi giả thuyết trên chỉ áp dụng cho slice B2-center này.

