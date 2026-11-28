### **EIUFF**
```bash
X: tiền gửi ban đầu
r%: lãi suất tháng
Y: số tiền rút mỗi tháng
f%: tỷ suất lạm phát

Yêu cầu: đủ tiền để rút trong N-1 tháng
Tính: X

X = Y * sum( (1+f/100)^i * (1+r/100)^(N-1-i)) / (1 + r/100)^N
```
Công thức tính X:

$$X = \frac{Y \sum_{i=0}^{N-1} \left(1 + \frac{f}{100}\right)^i \left(1 + \frac{r}{100}\right)^{N-1-i}}{\left(1 + \frac{r}{100}\right)^N}$$

```bash
double r
double f
double Y
int N

N -= 1;
double factor = 0;
for (int i=0; i<N; i++) {
    factor += Math.pow( (1 + f/100), i) * Math.pow( (1 + r/100), (N-1-i))
}
double X = Y * factor / Math.pow( (1 + r/100), N);
```
```bash
Suy công thức:

T1: balance = X(1+r) - Y
T2: (X(1+r) - Y)(1+r) - Y(1+f)
    X(1+r)^2 - Y(1+r) - Y(1+f)
T3: X(1+r)^3 - Y(1+r)^2 - Y(1+f)(1+r) - Y(1+f)^2
T4: X(1+r)^4 - Y(1+r)^3 - Y(1+f)(1+r)^2 - Y(1+f)^2(1+r) - Y(1+f)^3
T5: X(1+r)^5 - Y(1+r)^4 - Y(1+f)(1+r)^3 - Y(1+f)^2(1+r)^2 - Y(1+f)^3(1+r) - Y(1+f)^4
    X(1+r)^5 - Y ( (1+r)^4 + (1+f)(1+r)^3 + (1+f)^2(1+r)^2 + (1+f)^3(1+r) + (1+f)^4)

=>  X(1+r)^N - Y * sum ( (1+f)^i * (1+r)^(N-1-i) ) với i thuộc [0, N-1]
```

### **EIUBALANCE**
```bash
M tháng đầu tiên: đi làm
    Mỗi tháng:
        1. Nhận lương Mi
        2. Trừ chi tiêu
        3. Gửi tiết kiệm phần dư surplus = Mi - expense
M tháng sau: đi du lịch
    Mỗi tháng, tài khoản tiết kiệm:
        1. Cộng lãi
        2. Trừ chi tiêu
Input:
    M: số tháng
    M_i: tiền lương mỗi tháng
    X: tiền chi tiêu tháng đầu
    r%: lãi gửi
    f%: lạm phát
Output: số dư tài khoản
```

```bash
int M;
double[] income = new double[M];
double X;
double r;
double f;

double balance = 0;
double expense = X;

for (int i=0; i<M; i++) {
    double surplus = income[i] - expense;
    balance += surplus;
    balance *= (1 + r/100/12);
    expense *= (1 + f/100/12);
}
for (int i=0; i<M; i++) {
    balance *= (1 + r/100/12);
    balance -= expense;
    expense *= (1 + f/100/12);
}
```

### **EIURETIRE2**
```bash
Tìm X0: số tiền chi tiêu tháng đầu tiên

T1 - T_N:
    balance += income
    balance -= expense
    balance *= (1 + r)
    expense *= (1 + f)
T_N+1 - T1200:
    balance -= expense
    balance *= (1 + r)
    expense *= (1 + f)
```
Binary search:
```bash
static int N;
static double r;
static double f;
static double[] income = new double[N];

static boolean findX(double X, double[] income, double r, double f, int N) {
    double balance = 0;
    double expense = X;

    for (int i=0; i<1200; i++) {
        if (i < N) {
            balance += income[i];
        }
        balance -= expense;
        balance *= (1 + r/100/12);
        expense *= (1 + f/100/12);
    }
    if (balance >= 0) {
        return true;
    }
    else {
        return false;
    }
}

main() {
    double low = 0;
    double high = 1e12;

    for (int i=0; i<100; i++) {
        double mid = low + (high-low)/2;

        boolean isX = findX(mid, income, r, f, N);

        if (isX) {
            low = mid;
        }
        else {
            high = mid;
        }
    }
    sysout((long) Math.floor(low));
}
```

### **Home Strategy**
```bash
Mua nhà trong N tháng.
Giá nhà:
    - Khởi điểm: P0
    - Tỷ suất tăng lạm phát theo tháng: f
    - f thay đổi sau mỗi 5 năm
Gửi tiết kiệm:
    - Mỗi tháng: X đồng
    - Lãi theo tháng: r
    - r thay đổi sau mỗi 5 năm
Biết:
    - Khi savings >= 30%*giá nhà hiện tại: mua nhà
    - Vay phần tiền còn thiếu
    - Lãi vay theo tháng: c
Tính: X
```

```bash
static int N
static double P0
static double c
static double[] fi = new double[8]
static double[] ri = new double[8]

static boolean simulateX(double X) {
    double savings = 0;
    double house_price = P0;
    double debt = 0;
    int loan_start_month = 0;
    double r = ri[0];
    double f = fi[0];

    for (int i=0; i<N; i++) {
        int k = i / 60;
        r = ri[k];
        f = fi[k];
        if (savings < house_price*0.3) {
            savings += X;
            savings *= (1 + r);
        }
        else {
            debt = house_price - savings;
            loan_start_month = i;
            break;
        }
        house_price *= (1 + f);
    }
    for (int i=loan_start_month; i<N; i++) {
        debt *= (1 + c);
        debt -= X;
    }
    if (debt > 0) {
        return false;
    }
    else {
        return true;
    }

}

main() {

    for (int i=0; i<8; i++) {
        if ()
    }

    double low
    double high

    while() {
        double mid

        boolean isX = simulateX(mid, ....);

        if (isX) {

        }
        else {

        }
    }
}




```