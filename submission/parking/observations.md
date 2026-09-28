# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): Tôi vẽ 4 polyline, đều là vạch ngắn chạy xiên, vuông góc với hàng đỗ, và mỗi vạch là ranh giới giữa hai ô liền kề.
  - Hai vạch ở hàng giữa, ngay dưới vạch dọc dài y≈540: (172,522)→(250,564) và (285,520)→(421,555).
  - Hai vạch ở hàng tiền cảnh: (402,652)→(527,719) ở giữa đáy ảnh và (695,624)→(957,685) ở bên phải.
  - Mỗi polyline dừng đúng chỗ sơn trắng kết thúc. Vạch (402,652) chạm mép dưới ảnh nên dừng ở y=719, không kéo ra ngoài khung.
  - Đối chiếu với ảnh contrast: cũng như ảnh core, các vạch này tạo thành các ô song song và có khoảng cách lặp lại đều. Đó là dấu hiệu của vạch chia ô, không phải vạch lối đi.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao:
  - Không vẽ vạch dọc dài chạy ngang ảnh ở y≈530–545, nối từ x=0 sang phải. Đó là vạch cuối/đầu ô (vạch ranh giữa hai hàng đỗ quay đầu vào nhau), không phải ranh giới giữa hai ô riêng lẻ.
  - Không vẽ vạch gần dọc ở mép trái (≈(50,570)→(60,525)). Vạch này bị mờ, và vì phối cảnh nên không chắc nó là vạch chia ô hay vạch biên đầu hàng.
  - Không vẽ các vạch mờ ở hậu cảnh gần hàng rào (y<500), vì quá xa để xác định chúng chia ô nào.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không:
  - Polygon phủ lối xe chạy trống giữa hàng đỗ giữa và hàng tiền cảnh: mép trên y≈578, mép trái x=110, mép phải x=910.
  - Mép dưới đi xiên từ (910,598) qua (690,612), (398,640) tới (110,656). Mép này dừng ngay trước điểm bắt đầu của các vạch chia ô tiền cảnh, để không lấn vào ô đỗ.
  - Trong vùng này không có xe, curb hay cây che. Xe đỏ duy nhất nằm ở hậu cảnh (≈(195–220,458–478)), cách xa polygon.
  - Theo quy ước, polygon chỉ nói "mặt đường nhìn thấy trống"; nó không kết luận xe có thể đi an toàn qua vùng này.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”):
  - Vạch gần dọc ở mép trái (x≈50–60): cần hỏi đó là vạch chia ô hay vạch biên/đầu hàng.
  - Giới hạn xa của free_space: tôi dừng ở y≈578, vì phía trên là vùng có vạch hàng đỗ giữa. Nếu guideline muốn tính cả lối xe hậu cảnh (y≈480–500) thì cần thêm một polygon thứ hai.
