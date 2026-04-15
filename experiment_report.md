# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-001
**Name:** Data Quality Lab
**Date:** April 15, 2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Best choice is Laptop at $1200" | 9 | Correct - High-end electronics, valid price |
| Garbage Data (`garbage_data.csv`) | "Best choice is Nuclear Reactor at $999999" | 2 | Wrong - Extreme outlier, unrealistic price |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Garbage data chứa 4 vấn đề chính:

1. **Duplicate IDs** - ID 1 xuất hiện 2 lần (Laptop & Banana) khiến Agent nhầm lẫn
2. **Wrong Data Types** - Price "ten dollars" thay vì số khiến tính toán sai lệch
3. **Extreme Outliers** - Nuclear Reactor với giá $999,999 là dữ liệu không hợp lệ nhưng Agent vẫn chọn (vì nó có price cao nhất)
4. **Null Values** - id=None và category=None làm Agent không thể xử lý chính xác

**Tác động:** Agent chọn sản phẩm không thực tế (Nuclear Reactor) nhưng có giá cao nhất. Tại sao? Vì thuật toán đơn giản của Agent chỉ tìm `max(price)` mà không validate dữ liệu trước. Nếu có outlier, Agent sẽ bị lừa. Clean data chỉ chứa sản phẩm hợp lệ nên Agent trả lời chính xác.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Đồng ý 100%.

Thí nghiệm chứng minh: Cùng một Agent (cùng thuật toán, cùng prompt), kết quả hoàn toàn khác nhau tùy thuộc vào dữ liệu:
- **Clean data** (đã validate) → Accuracy 9/10, câu trả lời hợp lý
- **Garbage data** (full outliers, nulls) → Accuracy 2/10, câu trả lời vô lý

Kết luận: **Dữ liệu là nền tảng**. Dù prompt có tốt đến mấy cũng không thể cứu vãn nếu dữ liệu xấu. Data Quality & Data Observability là chìa khóa để AI Agent hoạt động hiệu quả. Bước Extract + Validate + Transform của ETL pipeline là **cực kỳ quan trọng**.
