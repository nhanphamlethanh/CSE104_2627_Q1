https://github.com/nhanphamlethanh/CSE104_2627_Q1

### **EIDISCOUNT2**
```bash
Bài toán chiết khấu:

- Dưới 5 triệu: không chiết khấu
- Các ngưỡng chiết khấu:
    Level 1: 5 - 20 triệu             3%
    Level 2: 20 - 100 triệu           5%
    Level 3: 100 - 300 triệu          7%
    Level 4: 300 - 600 triệu          10%
    Level 5: 600 - 900 triệu          12%
    Level 6: > 900 triệu              15%

"Tỉ lệ chiết khấu được áp dụng trên từng mức, không áp dụng trên toàn bộ hóa đơn" 

- Input: N --> số tiền ban đầu trên hóa đơn
- Output: số tiền thực tế phải trả sau khi được chiết khấu

VD: N = 30 triệu

    Level 0: 5 triệu đầu tiên: không chiết khấu
    Level 1: 15 triệu tiếp theo: chiết khấu 3% 
        => discount = 15 triệu * 3% = 450_000
    Level 2: 10 triệu tiếp theo: chiết khấu 5%
        => discount = 10 triệu * 5% = 500_000
    => total_discount = 950_000
    => pay = 30 triệu - 950_000 = 29_050_000
```
```bash
Hướng dẫn:
- Với mỗi ngưỡng:
    1. Tính số tiền được áp chiết khấu: amount
    2. Tính số tiền được giảm: discount
    3. Cộng discount vào total_discount
```