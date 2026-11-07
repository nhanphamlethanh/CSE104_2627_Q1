### **EIUMARKUP**
```bash
int N
int cost = 200;
int total_bill = 0;

while (N > 100) {
    total_bill += 100*cost;

    if (cost > 180) {
        cost--;
    }
    
    N -= 100;
}
total_bill += N*cost;
```

### **EIVCHR1**
```bash
long N = sc.nextLong();
long discount = Math.min(N/100*30, 50_000L);
long pay = N - discount;
```

### **EIVCHR2**
```bash
int N = sc.nextInt();
long maxDiscount = 0;
long pay = 0;

for (int i=0; i<N; i++) {
    long price = sc.nextLong();
    pay += price;

    long discount = Math.min(price/100*30, 50_000L);
    if (discount > maxDiscount) {
        maxDiscount = discount;
    }
}
pay -= maxDiscount;
```
### **EIVCHR3**
```bash
int N
int M

long[] prices = new long[N];
long pay = 0;

for (int i=0; i<N; i++) {
    prices[i] = sc.nextLong();
    pay += prices[i];
}

Arrays.sort(prices);

for (int i=N-1; i>= Math.max(0, N-M); i--) {
    pay -= Math.min(50_000L, prices[i]/100*30);
}
```

VD:
N = 10
M = 7

0 1 2 3 4 5 6 7 8 9


N = 10
M = 12

0 1 2 3 4 5 6 7 8 9



### **EIBANKRATE** - Lãi đơn (Simple Interest)
```bash
- Lãi: 9%/năm
- Số tiền gửi: N đồng
- Thời gian gửi: M tháng

double N = sc.nextDouble();
int M = sc.nextInt();

double balance = N * (1 + 0.09/12*M);
```
### **EIDINRATE** - Lãi kép (Compound Interest)
```bash
int T = sc.nextInt();

while (T-- > 0) {
    double N = sc.nextDouble();
    double L = sc.nextDouble();
    double M = sc.nextDouble();

    double balance = N;
    int year = 0;

    while (balance < M) {
        balance = balance * (1 + L/100);
        year++;
    }
    sysout(year);
}

```


```bash
VD: 
N = 100 triệu
I = 10%/năm
T = 14 tháng => 1 năm 2 tháng

Nếu lãi đơn:
    balance = 100 triệu + 100 triệu * 0.1 / 12 * 14 = 111_666_667
    balance = N * (1 + 0.09 / 12 * M)

Nếu lãi kép:
    balance = 100 triệu
    Sau năm 1: 
        balance = 100 triệu + (100 triệu * 0.1) = 110 triệu
        balance = balance * (1 + rate)
    Sau 2 tháng còn lại: 
        balance = 110 triệu + 110 triệu * 0.1 / 12 * 2 = 111_833_333
```
```bash
VD: 
N = 100 triệu
I = 10%/năm
T = 37 tháng => 3 năm 1 tháng

Ban đầu:
    balance = 100 triệu
Sau năm 1:
    balance = balance * (1 + rate)
            = 100 triệu * (1 + 0.1) = 110 triệu
Sau năm 2:
    balance = balance * (1 + rate)
            = 110 triệu * (1 + 0.1) = 121 triệu
Sau năm 3:
    balance = balance * (1 + rate)
            = 121 triệu * (1 + 0.1) = 136.1 triệu 
Sau 1 tháng còn lại:
    balance = balance * (1 + rate/12*1)
            = 136.1 triệu * (1 + 0.1/12*1) = 137.2 triệu

Đặt M = 137 triệu
=> Sau bao nhiêu năm thì balance đạt 137 triệu? => 4 năm
```


### **EISALARY2**
```bash
Với mỗi emp, tính:
    1. Tổng số giờ hành chính: office_hour
    2. Tổng số lương hành chính: office_wage
    3. Tổng số giờ OT: ot_hour
    4. Tổng số lương OT: ot_wage
Tính tổng của N nhân viên:
    1. Tổng số giờ hành chính: total_office_hour
    2. Tổng số lương hành chính: total_office_wage
    3. Tổng số giờ OT: total_ot_hour
    4. Tổng số lương OT: total_ot_wage
Tính trung bình:
    1. Lương hành chính: avg_office_wage = total_office_wage / total_office_hour
    2. Lương OT: tương tự
```