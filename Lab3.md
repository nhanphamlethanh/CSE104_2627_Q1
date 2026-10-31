### **EIMEMCARD**
```bash
int n
double total = 0;
double rate = 0;

for (int i=0; i<n; i++)
    double price = sc.nextDouble();
    total += price;
    
    double discount = price * rate;
    sysout(discount);

    if (total >= 200_000_000) {
        rate = 0.07;
    }
    else if (total >= 50_000_000) {
        rate = 0.05;
    }
    else if (total >= 20_000_000) {
        rate = 0.03;
    }
    else if (total >= 1_000_000) {
        rate = 0.02;
    }

```

### **EIGROSS**
```bash
Yêu cầu: tính tax
Biết:
    - net
    - tax rate = 10%

Công thức:
    tax = gross * tax_rate
    gross = net + tax
    tax = (net + tax) * 0.1
    tax = 0.1*net + 0.1*tax
    0.9*tax = 0.1*net
=> tax = net / 9


```