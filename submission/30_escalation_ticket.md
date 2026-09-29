# Escalation ticket

## Ticket 1

- **Frame:** adasind_086220.jpg
- **Ảnh chụp:** submission/screenshots/adasind_086220_R4.png
- **Expected impact:** Nếu R4 thật sự là vật bị bỏ sót (reference có, nhãn của mình không có), độ phủ (recall) của slice B2-center bị đánh giá thấp hơn thực tế. Nếu về sau slice này được dùng làm dữ liệu tham chiếu hoặc gold set, sai sót này có thể lan sang các quyết định khác.
- **Owner:** annotator
- **Recommendation:** Rework lại frame `adasind_086220.jpg` ở vùng tọa độ box R4 khi có thêm thời gian, đối chiếu trực tiếp trên ảnh gốc (không chỉ dựa vào reference) để xác nhận có vật hay không trước khi quyết định thêm/bỏ box.