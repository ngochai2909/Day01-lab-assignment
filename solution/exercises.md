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
> Khi temperature = 0.0, model luôn trả về cùng một câu trả lời, rất nhất quán và khô khan. Tăng lên 0.5 hay 1.0 thì câu trả lời bắt đầu có sự đa dạng hơn về cách diễn đạt, đôi khi kèm thêm chi tiết bất ngờ. Đến 1.5 thì câu văn trở nên phóng khoáng hơn hẳn, nhưng cũng có lúc hơi lạc đề hoặc thêm thông tin không cần thiết — kiểu như model đang "sáng tác" hơn là "trả lời".

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Mình sẽ đặt khoảng **0.2**. Chatbot hỗ trợ khách hàng cần ưu tiên sự chính xác và nhất quán — khách hỏi về chính sách hoàn tiền thì phải được câu trả lời đúng, không phải câu trả lời "sáng tạo". Temperature thấp giúp model bám sát thông tin có sẵn, tránh bịa đặt.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Tổng token output mỗi ngày: 10.000 × 3 × 350 = **10.500.000 token** = 10.500 K token  
> - GPT-4o: 10.500 × $0.010 = **$105/ngày**  
> - GPT-4o-mini: 10.500 × $0.0006 = **$6.3/ngày**  
>
> Vậy GPT-4o đắt hơn khoảng **16–17 lần** so với GPT-4o-mini cho cùng một workload. Tính ra mỗi tháng chênh lệch gần $3.000 — không nhỏ chút nào.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> **GPT-4o xứng đáng hơn:** Khi làm công cụ hỗ trợ lập trình viên phân tích bug phức tạp hoặc review code production — ở đây một câu trả lời sai có thể gây lỗi nghiêm trọng, và người dùng sẵn sàng trả thêm tiền để có chất lượng cao hơn.  
> **GPT-4o-mini phù hợp hơn:** Khi xây dựng tính năng tóm tắt tiêu đề email hoặc phân loại feedback ngắn của khách hàng — task đơn giản, volume lớn, không cần độ suy luận cao, dùng mini là đủ mà tiết kiệm đáng kể.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Tính năng streaming phát huy tác dụng tối đa với các câu trả lời dài (như giải thích kiến thức, viết mã code). Việc hiển thị văn bản theo thời gian thực giúp xóa bỏ khoảng thời gian chờ đợi trống, tạo cảm giác phản hồi nhanh và tương tác tự nhiên. Ngược lại, non-streaming lại lý tưởng khi hệ thống cần xử lý ẩn dữ liệu đầu ra trước khi hiển thị (như bóc tách định dạng JSON, kiểm duyệt từ ngữ), hoặc đối với các tác vụ tạo ra phản hồi cực ngắn (dưới 2 giây) nhằm giảm bớt sự phức tạp không cần thiết cho mã nguồn.


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
