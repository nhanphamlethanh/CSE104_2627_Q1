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


### **EIUTRIGLE**
```bash
n = 5
arr = {1, 4, 3, 6, 2}
1 2 3 4 6

Có bao nhiêu tam giác tạo thành được từ các phần tử trong mảng?

Điều kiện:
a b c là 3 cạnh của 1 tam giác khi thỏa mãn:
    a + b > c
và  b + c > a
và  a + c > b

Nếu a < b < c:
    Khi a + b > c
    Thì b + c > a và a + c > b luôn đúng.

0 1 2 3 4 5 6 7
1 2 2 3 4 6 7 9 

int n
int[] arr

int count = 0;

Arrays.sort(arr);

for (int i=n-1; i>1; i--) {
    int a_index = 0;
    int b_index = i-1;
    if (arr[a_index] + arr[b_index] <= arr[i]) {
        a_index++;
    }
    else {
        count += (b_index - a_index);
    }
}
```


### **eiumadis**
```bash
VD: cho mảng A
index: 0 1 2 3 4 5 6 7
value: 2 4 1 2 3 5 6 3

long maxDiff = 0;
long min = A[0];

for (int j=0; i<n; i++) {
    long diff = A[j] - min;
    if (diff > maxDiff) {
        maxDiff = diff;
    }
    if (A[j] < min) {
        min = A[j];
    }
}
sysout(maxDiff);
```

### **eisnail**
```bash
length = V mét
sáng bò A mét
tối lùi B mét

=> một ngày bò được (A-B) mét.
Ngày cuối cùng, bò tối đa A mét.

Giả sử: buổi sáng ngày cuối cùng, ốc sên bò đúng A mét.
=> Trước đó, quãng đường ốc sên bò là: (V-A) mét
=> số ngày cần để bò (V-A) mét là: (V-A) / (A-B)
    Math.ceil((double) (V-A) / (A-B))

=> số ngày để bò hết V mét là: Math.ceil((double) (V-A) / (A-B)) + 1 
```



### **EIUBIRTH**
```bash
Quà màu xanh:
- Số lượng: B
- Giá: X
Quà màu đỏ:
- Số lượng: R
- Giá: Y
Giá đổi màu: Z

Tính min_cost.

Xác định giá tốt nhất để mua mỗi loại quà:
- Màu xanh: 
    + TH1: X (mua đúng giá)
    + Th2: Y + Z (mua màu đỏ và đổi lại)
    => Giá tốt nhất để mua: costBlue = Math.min(X, (Y+Z))
- Màu đỏ: 
    + TH1: Y (mua đúng giá)
    + Th2: X + Z (mua màu xanh và đổi lại)
    => Giá tốt nhất để mua: costRed = Math.min(Y, (X+Z))

=> min_cost = costBlue*B + costRed*R
```



### **EIUCUBES**
```bash
Cho N viên gạch. Hỏi xây được kim tự tháp với tối đa bao nhiêu tầng?

Layer 1: 1
Layer 2: 1 + 2
Layer 3: 1 + 2 + 3
Layer 4: 1 + 2 + 3 + 4
...

VD: N = 25
- Ban đầu, số gạch có là 25:
    left = 25
- Xét layer 1:
    + Số gạch cần: needed = 1
    + left > needed => +1 layer
    + left = 24
- Xét layer 2:
    + Số gạch cần: needed = 3
    + left > needed => +1 layer
    + left = 21


int count = 0;
int left = N;
int layer = 1;
int needed = 1;

while (left >= needed) {
    count++;
    left -= needed;
    layer++;
    needed += layer;
} 
```