[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574036&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** student@vinuni.edu.vn
**Name:** Data Quality Lab Student

---

## Mo ta

Bài lab này tập trung xây dựng một ETL Pipeline hoàn chỉnh với các bước:
1. **Extract**: Đọc dữ liệu từ file JSON
2. **Validate**: Loại bỏ dữ liệu không hợp lệ (giá âm, category rỗng)
3. **Transform**: Khuyến mại 10% giá, chuẩn hóa category Title Case, thêm timestamp
4. **Load**: Lưu kết quả ra CSV

Ngoài ra, bài lab cũng kiểm tra tác động của **dữ liệu xấu** lên AI Agent thông qua thí nghiệm với garbage data.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
python generate_garbage.py
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
├── generate_garbage.py      # Tao garbage data
├── agent_simulation.py      # Chay stress test
└── README.md                # File nay
```

---

## Ket qua

**Tóm tắt kết quả ETL Pipeline:**
- **Input**: 5 records từ raw_data.json
- **Valid records**: 3 (Laptop, Chair, Monitor)
- **Dropped records**: 2 (ID 3: giá âm; ID 4: category rỗng)
- **Output**: processed_data.csv với 3 records đã transform

**Kết quả Experiment Report:**
- **Clean Data Agent Response**: Đúng - chọn Laptop ($1200) - Accuracy 9/10
- **Garbage Data Agent Response**: Sai - chọn Nuclear Reactor ($999,999) - Accuracy 2/10
- **Kết luận**: Dữ liệu chất lượng > Prompt chất lượng. Outliers & bad data làm Agent thất bại.
