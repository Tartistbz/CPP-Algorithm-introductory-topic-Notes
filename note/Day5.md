# P1304 哥德巴赫猜想

## 题目描述

输入一个偶数 $N$，验证 $4\sim N$ 所有偶数是否符合哥德巴赫猜想：任一大于 $2$ 的偶数都可写成两个质数之和。如果一个数不止一种分法，则输出第一个加数相比其他分法最小的方案。例如 $10$，$10=3+7=5+5$，则 $10=5+5$ 是错误答案。

## 输入格式

第一行输入一个正偶数 $N$

## 输出格式

输出 $\dfrac{N-2}{2}$ 行。对于第 $i$ 行：

首先先输出正偶数 $2i+2$，然后输出等号，再输出加和为 $2i+2$ 且第一个加数最小的两个质数，以加号隔开。

## 样例 #1

### 样例输入 #1

```
10
```

### 样例输出 #1

```
4=2+2
6=3+3
8=3+5
10=3+7
```

## 提示

数据保证，$ 4 \leq N\leq10000$。

mycode:

```cpp
#include <iostream>
#include <cmath>
using namespace std;
bool is_prime(int num){
    if(num<2)return false;
    int count=0;
    for(int i=1;i<=sqrt(num);++i){
        if(num%i==0)
            count++;
    }
    if(count==1){
        return true;
    }else{
        return false;
    }
}
int main(){
    int n;
    cin>>n;
    for(int i=4;i<=n;i+=2){
        for (int j = 2; j < i; j++)
        {
            if(is_prime(j)&&is_prime(i-j)){
                cout<<i<<"="<<j<<"+"<<i-j<<endl;
                break;
            }
        }
    }
}

```

# P1307 [NOIP2011 普及组] 数字反转

## 题目描述

给定一个整数 $N$，请将该数各个位上数字反转得到一个新数。新数也应满足整数的常见形式，即除非给定的原数为零，否则反转后得到的新数的最高位数字不应为零（参见样例 2）。

## 输入格式

一个整数 $N$。

## 输出格式

一个整数，表示反转后的新数。

## 样例 #1

### 样例输入 #1

```
123
```

### 样例输出 #1

```
321
```

## 样例 #2

### 样例输入 #2

```
-380
```

### 样例输出 #2

```
-83
```

## 提示

**【数据范围】**

$-1,000,000,000\leq N\leq 1,000,000,000 $。

noip2011 普及组第一题

mycode:

```cpp
#include <iostream>
#include <string>
#include <algorithm> 
using namespace std;
int main() {
    int a;
    cin>>a;
    bool isNegative = a<0;
    if(isNegative){
        a=-a;
    }
    string numStr = to_string(a);
    reverse(numStr.begin(),numStr.end());
    int startIndex = 0;
    while(startIndex<numStr.size() && numStr[startIndex]=='0'){
        startIndex++;
    }
    if(startIndex == numStr.size()){
        cout<<0;
    }else{
        numStr = numStr.substr(startIndex);
        int result = isNegative ? -stoi(numStr) : stoi(numStr);
        cout<<result;
    }
}
```

库函数的力量

# P1317低洼地

## 题目描述

一组数，分别表示地平线的高度变化。高度值为整数，相邻高度用直线连接。找出并统计有多少个可能积水的低洼地？

如图：地高变化为 $[0,1,0,2,1,2,0,0,2,0]$。

![](https://img-blog.csdnimg.cn/img_convert/7b5cfbfa20fd477a5baf160476f5bf17.png)

## 输入格式

两行，第一行 $n,$ 表示有 $n$ 个数。第 $2$ 行连续 $n$ 个数表示地平线高度变化的数据，保证首尾为 $0$。$(3 \le n \le 10000,0 \le $ 高度 $ \le 1000)$。

## 输出格式

一个数，可能积水低洼地的数目。

## 样例 #1

### 样例输入 #1

```
10
0 1 0 2 1 2 0 0 2 0
```

### 样例输出 #1

```
3
```

mycode:

```cpp
#include <iostream>
using namespace std;
int main() {
    int n;
    cin >> n;
    int heights[n];
    for (int i = 0; i < n; i++) {
        cin >> heights[i];
    }
    int count = 0;
    bool isDown = false;
    for(int j =1; j<n-1; j++){
        if(heights[j]<heights[j-1]) isDown = true;
        if(heights[j]<heights[j+1] && isDown){
            count++;
            isDown = false;
        } 
        if(heights[j]>heights[j+1]) isDown = false;
    }
    cout<<count;
    return 0;
}

```

