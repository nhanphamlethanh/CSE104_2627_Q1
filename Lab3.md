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

### **EIGROSS2**

https://docs.google.com/spreadsheets/d/1fPHnuLtHKYqqo8JDuW0ReYolmjSJLnvRmcUkz3zyWEE/edit?pli=1&gid=1700159211#gid=1700159211

```bash
Biết net.
Tính gross.

VD: net = 15_750_000
relief = 11 triệu
taxed: phần lương đã bị áp thuế
taxed = 15_750_000 - 11 triệu = 4_750_000

Level 1:
    - Lương sẽ bị áp thuế: taxable
    lower bound = 0
    upper bound = 5 triệu
    => maximum taxable = 5 triệu
    => số thuế tối đa = 250_000
    - Lương đã bị áp thuế: taxed
    lower bound = 0
    upper bound = 4_750_000
Level 2:
    taxed:
    lower bound = 
    upper bound =





gross = 19_000_000
relief = 9 triệu
=> taxable = 10 triệu => phần lương sẽ bị tính thuế

l1: tax = 250_000
l2: tax = 500_000
=> tax = 750_000
net = gross - tax = 18_250_000
taxed = 18_250_000 - 9 triệu = 9_250_000
taxed = taxable - tax
(net - relief) = (gross - relief) - tax
net = gross - tax

```