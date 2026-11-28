### **EIUFF**
```bash
X: tiền gửi ban đầu
r%: lãi suất tháng
Y: số tiền rút mỗi tháng
f%: tỷ suất lạm phát

Yêu cầu: đủ tiền để rút trong N tháng
Tính: X

X = Y * sum( (1+f/100)^i * (1+r/100)^(N-1-i)) / (1 + r/100)^N
```
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