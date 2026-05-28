# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> *Câu trả lời của bạn*
Temperature 0.0 cho kết quả rất nhất quán, lặp lại gần như giống nhau mỗi lần — model chọn token có xác suất cao nhất. Khi temperature tăng lên 0.5–1.0, câu trả lời đa dạng hơn, sáng tạo hơn nhưng vẫn mạch lạc. Ở 1.5, phản hồi có thể trở nên ngẫu nhiên, đôi khi lạc đề hoặc mất tự nhiên.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> *Câu trả lời của bạn*
Nên đặt khoảng 0.2–0.3. Chatbot hỗ trợ cần trả lời chính xác, nhất quán và đáng tin cậy — temperature thấp giúp tránh bịa thông tin, đồng thời vẫn đủ linh hoạt để không nghe như robot.
---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> *Câu trả lời của bạn*
10.000 users × 3 calls × 350 tokens = 10.5M tokens/ngày (giả sử input/output ngang nhau: ~175K input + 175K output mỗi 1M).
Chi phí GPT-4o: input $5.00 + output $20.00 = $25/1M token
Chi phí GPT-4o-mini: input $0.15 + output $0.60 = $0.75/1M token
→ GPT-4o đắt hơn khoảng 33 lần so với GPT-4o-mini cho cùng workload.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> *Câu trả lời của bạn*
GPT-4o xứng đáng khi task đòi hỏi lập luận phức tạp, ví dụ phân tích hợp đồng pháp lý hoặc debug code khó — sai sót ở đây gây hậu quả thực tế. Ngược lại, GPT-4o-mini là lựa chọn tốt hơn cho các tác vụ đơn giản, lặp lại nhiều như phân loại email, tóm tắt ngắn, hoặc trả lời FAQ — nơi tốc độ và chi phí quan trọng hơn độ tinh tế.



---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> *Câu trả lời của bạn*
Streaming quan trọng nhất khi response dài và người dùng cần cảm giác phản hồi tức thì — ví dụ chatbot hội thoại, viết bài, hoặc giải thích code — vì hiển thị từng token giúp người dùng bắt đầu đọc ngay thay vì chờ hàng vài giây. Non-streaming phù hợp hơn khi kết quả cần hoàn chỉnh trước khi xử lý tiếp, chẳng hạn gọi API để lấy JSON rồi parse, hoặc các pipeline tự động không có người dùng trực tiếp — lúc đó overhead của streaming không mang lại giá trị gì.

## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
