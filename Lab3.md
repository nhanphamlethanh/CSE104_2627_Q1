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

```bash
Biết net.
Tính gross.

VD: net = 15_750_000
relief = 11 triệu
taxed: phần lương đã bị áp thuế
taxed = 15_750_000 - 11 triệu = 4_750_000

Bảng quy đổi taxed:
https://docs.google.com/spreadsheets/d/1fPHnuLtHKYqqo8JDuW0ReYolmjSJLnvRmcUkz3zyWEE/edit?pli=1&gid=1700159211#gid=1700159211
```
```bash
long net = sc.nextLong();
long[] upper_bound = {4_750_000, 9_250_000, 16_050_000,
                        27_250_000, 42_250_000, 61_850_000, Long.MAX_VALUE};
int[] rate = {5, 10, 15, 20, 25, 30, 35};
long lower_bound = 0;

long taxed = net - 11_000_000;
long tax = 0;

for (int i=0; i<rate.length; i++) {
    if (taxed > lower_bound) {
        long amount = Math.min(taxed, upper_bound[i]) - lower_bound;
        tax += amount * rate[i] / (100 - rate[i]);
        lower_bound = upper_bound[i];
    } else {
        break;
    }
}
long gross = net + tax;
```

### **DELIVERY FEE OPTIMIZATION**
```bash
VD:
n = 4
k = 2
D = 20%

d1 = 1.2
d2 = 2.0
d3 = 4.1
d4 = 12.3

Xét order 1:
    Quãng đường: d1 = 1.2 => d1 = 2
    => fee = 9999
Order 2:
    d2 = 2.0 = 2
    => fee = 9999
Order 3:
    d3 = 4.1 => d3 = 5
    => fee = 9999 + 3 * 5555 = 26_664
    => after_discount_fee = 26_664 * 0.8 = 21_331
Order 4:
    d4 = 12.3 => d4 = 13
    => fee = 9999 + 3*5555 + 5*4321 + 3*3199 = 57_866
    => after_discount_fee = 57_866 * 0.8 = 46_292

total_fee = 87_621
```

d1 = 2.1
f1 = 9999 + 5555 = 15_554

d2 = 3
f2 = 15_554

d3 = 7.5
f3 = 9999 + 3*5555 + 3*4321 = 39_627

d4 = 10
f4 = 9999 + 3*555 + 5*4321 = 48_269

d5 = 10.1
f5 = 51_468
f5 = 51_468 * 0.9 = 46_321

total_fee = 165325
