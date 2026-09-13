# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** Trịnh Đức Huy  
> **Mã Sinh Viên / Mã Học viên:** 2A202602865  
> **Chủ đề Lựa chọn:** Trợ lý Học vụ & Tra cứu Lịch thi VinUni:* Tra cứu điểm GPA, lịch thi và đặt lịch tư vấn học vụ với Cố vấn.

---

## 1. BẢNG CHẤM ĐIỂM AGENTIC FIT SCORING MATRIX (ĐÁNH GIÁ CHỦ ĐỀ)

| Tiêu chí Đánh giá | Mức độ (1 - 5) | Giải trình chi tiết lý do chọn điểm |
| :--- | :---: | :--- |
| **1. Multi-step Reasoning** | 4 / 5 | Yêu cầu kết hợp tra cứu và đặt lịch cần nhiều bước nối tiếp: xác định mã sinh viên, tra cứu hồ sơ/GPA và cố vấn học tập, lấy thông tin thời gian hẹn, sau đó đặt lịch và tổng hợp kết quả. Chấm 4 vì chuỗi xử lý có phụ thuộc dữ liệu nhưng tương đối ngắn; câu hỏi tra cứu đơn lẻ chỉ cần một bước. |
| **2. Tool Interaction** | 5 / 5 | Hệ thống cần gọi công cụ qua MCP Server để lấy dữ liệu học vụ bằng `academic_query` và thực hiện đặt lịch bằng `schedule_appointment`; mô hình không thể chỉ sinh văn bản để hoàn thành các thao tác này. Bản lab hiện dùng dữ liệu mô phỏng, còn tra cứu lịch thi cần bổ sung công cụ và nguồn dữ liệu tương ứng. |
| **3. Dynamic Decision** | 4 / 5 | Bước tiếp theo phụ thuộc kết quả công cụ: nếu tìm thấy sinh viên thì dùng thông tin cố vấn trả về để đặt lịch; nếu nhận `NOT_FOUND` thì thông báo và yêu cầu kiểm tra mã; nếu thiếu thời gian hẹn thì cần hỏi bổ sung. Chấm 4 vì có rẽ nhánh theo quan sát nhưng số tình huống và phương án xử lý còn giới hạn. |
| **4. Long Horizon Goal** | 3 / 5 | Hệ thống cần giữ mục tiêu hỗ trợ học vụ và các thông tin như mã sinh viên, cố vấn, thời gian hẹn xuyên suốt các bước tra cứu, bổ sung thông tin và đặt lịch. Chấm 3 vì mục tiêu thường hoàn tất trong một phiên ngắn, chưa đòi hỏi theo dõi tiến độ học tập hay quản lý lịch qua nhiều ngày. |
| **TỔNG ĐIỂM AGENTIC FIT** | **16 / 20** | *Tổng điểm 16/20 > 12/20: Bài toán rất phù hợp triển khai Agentic System, đặc biệt với luồng tra cứu học vụ rồi đặt lịch tư vấn dựa trên dữ liệu trả về. Đây là đánh giá mức độ phù hợp của chủ đề, không phải xác nhận các chức năng đã được triển khai và nghiệm thu đầy đủ.* |

---

## 2. TRÍCH XUẤT KẾT QUẢ WATERFALL TRACE LOG (SAU KHI CHẠY TEST SUITE TRÊN API THẬT)

> ⚠️ **YÊU CẦU NGHIỆM THU:** Mở tệp `.env` điền `GEMINI_API_KEY` (hoặc `OPENAI_API_KEY`) để kết nối LLM thật trước khi thực thi `python src/app.py --all`. Bài nộp chỉ dùng Mock Offline Provider sẽ không đạt điểm nghiệm thực tế.

Dán 1 đoạn trích xuất log tiêu biểu từ file `docs/trace_waterfall.json` sinh ra từ phản hồi LLM API thật:

```json
[
  {
    "step": 1,
    "query": "Đặt lịch hẹn tư vấn cho SV2026001 vào 14:00 ngày 15/09/2026 với PGS.TS Nguyễn Văn A",
    "action_type": "TOOL_EXECUTION",
    "tool_name": "schedule_appointment",
    "arguments": {
      "student_id": "SV2026001",
      "datetime_str": "14:00 15/09/2026",
      "advisor_name": "PGS.TS Nguyễn Văn A"
    },
    "observation": {
      "status": "SUCCESS",
      "booking_id": "BK-SV2026001-99",
      "student_id": "SV2026001",
      "datetime": "14:00 15/09/2026",
      "advisor": "PGS.TS Nguyễn Văn A",
      "message": "Đặt lịch thành công cho sinh viên SV2026001 với PGS.TS Nguyễn Văn A vào lúc 14:00 15/09/2026."
    },
    "latency_ms": 3016.63
  },
  {
    "step": 2,
    "query": "Đặt lịch hẹn tư vấn cho SV2026001 vào 14:00 ngày 15/09/2026 với PGS.TS Nguyễn Văn A",
    "action_type": "FINAL_ANSWER",
    "thought": "Tổng hợp kết quả từ MCP Server thành công.",
    "output": "Đặt lịch thành công cho sinh viên SV2026001 với PGS.TS Nguyễn Văn A vào lúc 14:00 15/09/2026.",
    "latency_ms": 10.0
  }
```

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI

- [x] Đã điền API Key thật trong `.env` và xác nhận Agent chạy mượt mà trên LLM API thật (Gemini/OpenAI).
- **Tổng số Test Cases đã chạy thành công:** ___ / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** ___ lượt.
- **Kết quả đẩy Repo nộp bài:** [ ] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

> ✅ **HOÀN TẤT NỘP BÀI:** Sao chép đường link GitHub Repository cá nhân của bạn và dán vào ô nộp bài trên hệ thống LMS VLearn để hoàn tất Bài Lab 3!
