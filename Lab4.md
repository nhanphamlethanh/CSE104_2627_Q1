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