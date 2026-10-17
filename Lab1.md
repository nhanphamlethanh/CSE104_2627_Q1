### **EIMONE**
- Có b đồng
- Đổi thành các mệnh giá: 20, 10, 5, 1
- n: số tờ tiền đổi được
- Yêu cầu: n ít nhất có thể

b = 72

xét 20:
n_20 = 72/20 = 3
left = 72%20 = 12

xét 10:
n_10 = 12/10 = 1
left = 12%10 = 2

xét 5:
n_5 = 2/5
left = 2

xét 1:
n_1 = 2

```bash
int b = sc.nextInt();
int left = b;

if (left >= 20) {
    int n = left / 20;
    sysout("20" + " " + n);
    left %= 20;
}
```

### **EIPOINT**
```bash
int[] num = {90, 85, 80, 75, 70, 65, 60, 55, 53, 52, 50, 0};
String[] char = {"A", "A-", "B+", "B", "B-", "C+", "C", "C-", "D+", "D", "D-", "F"};

int score = sc.nextInt();

for (int i=0; i<num.length; i++) {
    if (score >= num[i]) {
        sysout(char[i]);
    }
}
```

### **EIUTHU**
.substring()

VD:
S1 = "trunghoccosotran"
S2 = "trandainghia"

Yêu cầu: tìm độ dài ngắn nhất

S1.length() = 16
S2.length() = 12

độ dài phần trùng lặp: overlap = ?

maxOverlap = Math.min(S1.length(), S2.length()) = 12

suffix = S1.substring()
prefix = S2.substring(0,_) 

```bash
int overlap = 0;
for (int i=maxOverlap; i>0; i--) {
    String suffix = S1.substring(S1.length() - i);
    String prefix = S2.substring(0,i);
    if (suffix.equals(prefix)) {
        overlap = prefix.length();
        break;
    }
}

int shortest_length = S1.length() + S2.length() - overlap;
```

### **EIEVERYN**
```bash
int m
int n 
int[] arr = new int[m];

boolean[] check = new boolean[n+1];

for (int i=0; i<m; i++) {
    if (arr[i] <= n) {
        check[arr[i]] = true;
    }
}
boolean hasAll = true;
for (int i=1; i<=n; i++)
    if (check[i] != true) {
        hasAll = false;
        break;
    }

if (hasAll) 
    YES
else
    NO
```

```bash
VD:
m = 7 
n = 6

5 2 1 2 2 5 3

index 0     1     2     3     4     5     6
            true  true  true        true
```


