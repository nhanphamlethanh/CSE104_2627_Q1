### **EIAPP21222FQ1**
```bash
Gửi tiết kiệm:
- Số tiền: N đồng
- Thời gian: M tháng
- Biết: kỳ hạn càng dài --> lãi suất càng cao

? Tìm số tiền tối đa có thể nhận được sau M tháng

VD:
N = 10_000
M = 14 
=> Gửi 1 kỳ hạn 12 tháng (lãi: 6.92%)
sau đó gửi tiếp 1 kỳ hạn 2 tháng (lãi: 3.92%)

Sau kỳ hạn 12 tháng:
    balance = 10_000 * (1 + 6.92/100) = 10_692
Sau kỳ hạn 2 tháng:
    balance = 10_692 * (1 + 3.92/100/12*2) = 10_761

VD:
N = 10_000
M = 27 tháng = 2 * 12 + 3
=> Gửi:
    + 2 kỳ hạn 12 tháng
    + 1 kỳ hạn 3 tháng
Sau 2 kỳ hạn 12 tháng:
    balance = 10_000 * (1 + 6.92/100)^2 = 11_431.8864
Sau 1 kỳ hạn 3 tháng:
    balance = 11_431.8864 * (1 + 3.95/100/12*3)

Ý tưởng giải:
- Input:
    double N
    int M
    double[] rate = {3.90, 3.92, 3.95, ..., 6.92}
- Tính kỳ hạn:
    + Số kỳ hạn 12 tháng:
        year = M / 12
    + Xác định kỳ hạn còn lại (số tháng còn lại):
        month = M % 12
VD:
N = 10_000
M = 27 tháng = 2 * 12 + 3
balance = N = 10_000
full_years = M / 12 = 2
left_months = M % 12 = 3

Sau (M / 12) năm:
    balance = balance * (1 + 6.92/100)^full_years
Sau kỳ hạn (M % 12) tháng:
    balance = balance * (1 + rate[left_months-1]/100/12*left_months)
```

### **EIAPP21222FQ2**
```bash
Gửi tiết kiệm:

VD:
N = 14 tháng
T1: 
    + Gửi 1000 đồng => số tiền này sẽ ở trong ngân hàng 14 tháng
    => Kỳ hạn: 12 tháng + 2 tháng
    => balance1 = 1000 * (1 + 6.92/100)^1 * (1 + 3.92/100/12*2)
T2: 
    + Gửi 2000 => số tiền này sẽ ở trong ngân hàng 13 tháng
    => Kỳ hạn: 12 tháng + 1 tháng
    => balance2 =
...
T14:
    + Gửi 1000 => số tiền này sẽ ở trong ngân hàng 1 tháng
    => Kỳ hạn: 1 tháng
    => balance14
Tính tổng:
    balance = balance1 + balance2 +...+balance14
```