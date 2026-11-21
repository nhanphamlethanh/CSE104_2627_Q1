### **EIPURCHASE**
```bash
double V        //Giá sản phẩm
int T           //số tháng trả góp
double N        // số tiền trả trước
double M        // số tiền trả góp mỗi tháng

Tính: r         // lãi suất thực

1. Xác định số tiền nợ:
    debt = V - N
2. Cập nhật nợ sau mỗi tháng:
    Vào đầu mỗi tháng, tính và cộng lãi suất cho phần dư nợ còn lại:
        debt = debt * (1 + r)
    Trừ tiền trả góp:
        debt -= M;
    => công thức cập nhật nợ sau mỗi tháng:
        debt = debt * (1 + r) - M;
=> lặp lại trong T tháng:
        0 = (V-N) * (1 + r)^T - M * sum ( (1+r)^i) với i từ 0, T-1

=> binary search:
biến cần tìm: r
1. Xác định domain giá trị của biến cần tìm:
    r thuộc [0, 1]
=> double low = 0;
double high = 1;

2. Viết hàm mô phỏng quá trình cập nhật nợ hàng tháng:
    static double calculateDebt(double V, double N, int T, double M, double r) {
        double debt = V-N;
        for (int i=0; i<T; i++) {
            debt = debt * (1 + r) - M;
        }
        return debt;
    }

```

```bash

while (high - low > 1e-6) {
    double mid = (low + high) / 2;
    
    double remaining_debt = calculateDebt(V, N, T, M, mid);

    if (remaining_debt > 0) {
        high = mid;
    }
    else {
        low = mid;
    }
}
double rate = (high + low)/2;
```


### **EIUPURCHASE3**
```bash
P: giá trị sản phẩm
M: số tiền trả trước
N: số tháng trả góp
R: lãi suất hàng tháng

Tính: X (số tiền khách trả góp mỗi tháng)
```

```bash
1. Số tiền nợ:
    debt = P - M
2. Cập nhật nợ sau mỗi tháng:
    debt = debt * (1 + R) - X
=> Cập nhật nợ sau N tháng:
    debt = (P-M) * (1+R)^N - X*sum( (1+R)^i ) với i chạy từ N-1 tới 0

Biết: sau tháng N, phải trả hết nợ => debt = 0
=> (P-M) * (1+R)^N - X*sum( (1+R)^i ) = 0

=> X = (P-M) * (1+R)^N * R / ((1+R)^N - 1)
Sau T1:
    debt = (P-M) * (1 + R) - X
Sau T2:
    debt = ((P-M) * (1 + R) - X) * (1+R) - X
    debt = (P-M) * (1+R)^2 - X*(1+R) - X
Sau T3:
    debt = ((P-M) * (1+R)^2 - X*(1+R) - X) * (1+R) - X
    debt = (P-M) * (1+R)^3 - X*(1+R)^2 - X*(1+R) - X
Sau T4:
    debt = (P-M) * (1+R)^4 - X*(1+R)^3 - X*(1+R)^2 - X*(1+R) - X
Sau N tháng:
    debt = (P-M) * (1+R)^N - X*sum( (1+R)^i ) với i chạy từ N-1 tới 0
```

```bash
double P
double M
int N
double R

double X = (P-M) * Math.pow( (1+R), N) * R / (Math.pow( (1+R), N) - 1);
sysout(Math.floor(X));
```



### **EIUPASSBOOK**
```bash
Input:
    X: số tiền gửi tiết kiệm
    n: số tháng gửi
    m: số tháng đã gửi
    r1: lãi suất gửi (%/năm)
    r2: lãi suất vay (%/năm)
Process:
    1. Ban đầu, lập sổ tiết kiệm:
        gửi X đồng
        thời hạn n tháng
        lãi suất r1%/năm
    2. Sau m tháng, cần tiền để xây nhà. Có 2 lựa chọn để có tiền:
        Option 1: rút sổ tiết kiệm
            Tại tháng m, chưa hết thời hạn gửi.
            Nếu rút tiền, số tiền sẽ nhận được là X (không lãi).
        Option 2: dùng sổ tiết kiệm để vay thế chấp
            Điều kiện đảm bảo:
                Số tiền tiết kiệm nhận được sau n tháng PHẢI ĐỦ để trả số tiền vay + lãi vay
            Xác định:
                Thời gian vay: (n-m) tháng
                lãi suất: r2%/năm
                Số tiền vay: Y => biến cần tìm (vay được tối đa bao nhiêu để số tiền có được từ n tháng gửi tiết kiểm ĐỦ để trả)
            Tính:
                1. Số tiền có được sau n tháng gửi tiết kiệm
                    passbook_balance = X * (1 + r1/100/12*n);
                2. Viết công thức tính tổng tiền vay + lãi sau (n-m) tháng
                    debt = Y * (1+r2/100)^((n-m)/12) * (1+r2/100/12*((n-m)%12))
                3. Tính Y
                    Biết: passbook_balance = debt
                    => 
        Y = passbook_balance / (1+r2/100)^((n-m)/12) * (1+r2/100/12*((n-m)%12))
Output:
    if (X - Y > 1e-5) {
        sysout(Math.round(X))
    }        
    else {
        sysout(Math.round(Y))
    }
```