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

- Tính amount tại mỗi ngưỡng:
    Chỉ có 2 trường hợp xảy ra:
        1. Nếu N >= max của ngưỡng:
            amount = max - min
        2. Ngược lại:
            amount = N - min

long N;
long total_discount = 0;

Cách 1: if-else
Xét level 1:
    if (N >= 5_000_000) {
        long amount = Math.min(N, 20_000_000) - 5_000_000;
        long discount = amount / 100 * 3;
        total_discount += discount;
    }
Xét level 2:
    if (N >= 20_000_000) {
        long amount = Math.min(N, 100_000_000) - 20_000_000;
        long discount = amount / 100 * 5;
        total_discount += discount;
    }
Tương tự xét level 3-5.
Xét level 6:
    if (N >= 900_000_000) {
        long amount = N - 900_000_000;
        long discount = amount / 100 * 15;
        total_discount += discount;
    }
long pay = N - total_discount;
sysout(pay);
```

```bash
Cách 2: 2 arrays + for loop
long[] upper_bounds = {20_000_000, 100_000_000,
                 300_000_000, 600_000_000, 900_000_000, Long.MAX_VALUE};
long[] rate = {3, 5, 7, 10, 12, 15};

long lower_bound = 5_000_000;

for (int i=0; i<rate.length; i++) {
    if (N >= lower_bound) {
        long amount = Math.min(N, upper_bounds[i]) - lower_bound;
        long discount = amount / 100 * rate[i];
        total_discount += discount;
        lower_bound = upper_bounds[i]; // Cập nhật giá trị min cho ngưỡng tiếp theo
    }
    else {
        break;
    }
}
```