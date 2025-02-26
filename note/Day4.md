最近刚开学，贪玩加忙别的事，搁置了
# P1161 开灯

## 题目描述

在一条无限长的路上，有一排无限长的路灯，编号为 $1,2,3,4,\dots$。

每一盏灯只有两种可能的状态，开或者关。如果按一下某一盏灯的开关，那么这盏灯的状态将发生改变。如果原来是开，将变成关。如果原来是关，将变成开。

在刚开始的时候，所有的灯都是关的。小明每次可以进行如下的操作：

指定两个数，$a,t$（$a$ 为实数，$t$ 为正整数）。将编号为 $\lfloor a\rfloor,\lfloor 2 \times a\rfloor,\lfloor3 \times a\rfloor,\dots,\lfloor t  \times a\rfloor$ 的灯的开关各按一次。其中 $\lfloor k \rfloor$ 表示实数 $k$ 的整数部分。

在小明进行了 $n$ 次操作后，小明突然发现，这个时候只有一盏灯是开的，小明很想知道这盏灯的编号，可是这盏灯离小明太远了，小明看不清编号是多少。

幸好，小明还记得之前的 $n$ 次操作。于是小明找到了你，你能帮他计算出这盏开着的灯的编号吗？

## 输入格式

第一行一个正整数 $n$，表示 $n$ 次操作。

接下来有 $n$ 行，每行两个数，$a_i,t_i$。其中 $a_i$ 是实数，小数点后一定有 $6$ 位，$t_i$ 是正整数。

## 输出格式

仅一个正整数，那盏开着的灯的编号。

## 样例 #1

### 样例输入 #1

```
3
1.618034 13
2.618034 7
1.000000 21
```

### 样例输出 #1

```
20
```

## 提示

记 $T=\sum \limits_{i=1}^n t_i = t_1+t_2+t_3+\dots+t_n$。

- 对于 $30\%$ 的数据，满足 $T \le 1000$；
- 对于 $80\%$ 的数据，满足 $T \le 200000$；
- 对于 $100\%$ 的数据，满足 $T \le 2000000$；
- 对于 $100\%$ 的数据，满足 $n \le 5000$，$1 \le a_i<1000$，$1 \le t_i \le T$。

数据保证，在经过 $n$ 次操作后，有且只有一盏灯是开的，不必判错。而且对于所有的 $i$ 来说，$t_i\times a_i$ 的最大值不超过 $2000000$。

mycode:

```cpp
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;
const int MAX_SIZE = 2000001;
int main(){
    int n;
    cin >> n;
    vector<int> lights(MAX_SIZE,0);
    for(int i=0;i<n;i++){
        int t;
        double a;
        cin >> a >> t;
        for(int j=1;j<=t;j++){
            int light_index = (int)(a*j);
            //int light_index = static_cast<int>(std::floor(a * j));
            lights[light_index] ^= 1;
        }
    }
    int j = 1;
    while (lights[j] == 0)
    {
        j++;
    }
    printf("%d",j);
}

```

tips:

```cpp
int light_index = static_cast<int>(std::floor(a * j));
```

标准库floor方法，向下取整

`lights[light_index] ^= 1;`：这个操作使用异或（XOR）运算符来切换灯的状态。如果灯是关（0），按下开关后变为开（1）；如果灯是开（1），按下开关后变为关（0）。

# P1179 [NOIP2010 普及组] 数字统计

## 题目描述

请统计某个给定范围 $[L, R]$ 的所有整数中，数字 $2$ 出现的次数。

比如给定范围 $[2, 22]$，数字 $2$ 在数 $2$ 中出现了 $1$ 次，在数 $12$ 中出现 $1$ 次，在数 $20$ 中出现 $1$ 次，在数 $21$ 中出现 $1$ 次，在数 $22$ 中出现 $2$ 次，所以数字 $2$ 在该范围内一共出现了 $6$ 次。

## 输入格式

$2$ 个正整数 $L$ 和 $R$，之间用一个空格隔开。

## 输出格式

数字 $2$ 出现的次数。

## 样例 #1

### 样例输入 #1

```
2 22
```

### 样例输出 #1

```
6
```

## 样例 #2

### 样例输入 #2

```
2 100
```

### 样例输出 #2

```
20
```

## 提示

$1 ≤ L ≤R≤ 100000$。

NOIP2010 普及组 第一题

mycode:

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main(){
    int L,R;
    cin >> L >> R;
    int n = 0;
    for(int i=L;i<=R;i++){
        string numStr = to_string(i);
        n += count(numStr.begin(),numStr.end(),'2');
    } 
    cout << n;
}

```

tips:

### 字符串转换

```cpp
std::string numStr = std::to_string(i);
```

- `std::to_string(i)` 将整数 `i` 转换为字符串类型。这样我们可以方便地操作每个数字的字符。

### 4. 统计字符

```cpp
count += std::count(numStr.begin(), numStr.end(), '2');
```

- `std::count` 是 C++ 标准库中的一个函数，用于统计范围内特定元素的出现次数。
- `numStr.begin()` 和 `numStr.end()` 分别表示字符串的起始和结束迭代器，形成一个迭代范围。
- `'2'` 是我们要统计的字符。`std::count` 将返回字符 `'2'` 在字符串 `numStr` 中出现的次数，并将这个值累加到 `count` 变量中。

# P1200[USACO1.1] 你的飞碟在这儿 Your Ride Is Here

## 题目描述

众所周知，在每一个彗星后都有一只 UFO。这些 UFO 时常来收集地球上的忠诚支持者。不幸的是，他们的飞碟每次出行都只能带上一组支持者。因此，他们要用一种聪明的方案让这些小组提前知道谁会被彗星带走。他们为每个彗星起了一个名字，通过这些名字来决定这个小组是不是被带走的那个特定的小组（你认为是谁给这些彗星取的名字呢？）。关于如何搭配的细节会在下面告诉你；你的任务是写一个程序，通过小组名和彗星名来决定这个小组是否能被那颗彗星后面的 UFO 带走。


小组名和彗星名都以下列方式转换成一个数字：最终的数字就是名字中所有字母的积，其中 $\texttt A$ 是 $1$，$\texttt Z$ 是 $26$。例如，$\texttt{USACO}$ 小组就是 $21 \times 19 \times 1 \times 3 \times 15=17955$。如果小组的数字 $\bmod 47$ 等于彗星的数字 $\bmod 47$,你就得告诉这个小组需要准备好被带走！（记住“$a \bmod b$”是 $a$ 除以 $b$ 的余数，例如 $34 \bmod 10$ 等于 $4$）


写出一个程序，读入彗星名和小组名并算出用上面的方案能否将两个名字搭配起来，如果能搭配，就输出 `GO`，否则输出 `STAY`。小组名和彗星名均是没有空格或标点的一串大写字母（不超过 $6$ 个字母）。

## 输入格式

第1行：一个长度为 $1$ 到 $6$ 的大写字母串，表示彗星的名字。

第2行：一个长度为 $1$ 到 $6$ 的大写字母串，表示队伍的名字。

## 输出格式

## 样例 #1

### 样例输入 #1

```
COMETQ
HVNGAT
```

### 样例输出 #1

```
GO
```

## 样例 #2

### 样例输入 #2

```
ABSTAR
USACO
```

### 样例输出 #2

```
STAY
```

## 提示

题目翻译来自 NOCOW。

USACO Training Section 1.1

mycode:

```cpp
#include <iostream>
#include <string>
using namespace std;
int compute_string(string name){
    int count = 1;
    for(char ch : name){
        count *= (ch - 'A' +1);
    }
    return count;
}
int main(){
    string starName,groupName;
    cin >> starName >> groupName;
    int s= compute_string(starName)%47;
    int g = compute_string(groupName)%47;
    if(s==g){
        cout<<"GO";
    }else{
        cout<<"STAY";
    }
}

```

tips:

范围 `for` 循环是一种简洁的遍历容器或数组的方法。除了用于字符串，还可以用于其他 STL 容器，如 `vector`、`list`、`set` 等。以下是一些常见的用法：

### 1. 用于数组

对于普通数组，你可以使用范围 `for` 循环遍历元素：

```cpp
int arr[] = {1, 2, 3, 4, 5};
for (int num : arr) {
    // 处理每个元素 num
}
```

### 2. 用于 `std::vector`

`std::vector` 是 C++ STL 中的动态数组，可以使用范围 `for` 循环：

```cpp
#include <vector>

vector<int> vec = {1, 2, 3, 4, 5};
for (int num : vec) {
    // 处理每个元素 num
}
```

### 3. 用于 `std::string`

如之前所述，你可以直接遍历字符串：

```cpp
string myString = "HELLO";
for (char ch : myString) {
    // 处理每个字符 ch
}
```

### 4. 用于其他 STL 容器

你也可以用于 `std::set` 或 `std::map` 的 `key` 或 `value`：

```cpp
#include <set>

set<int> mySet = {1, 2, 3};
for (int num : mySet) {
    // 处理每个元素 num
}
```

### 5. 用于 `std::map`

遍历 `std::map` 的键值对：

```cpp
#include <map>

map<string, int> myMap = {{"A", 1}, {"B", 2}};
for (const auto& pair : myMap) {
    cout << pair.first << ": " << pair.second << endl; // 访问键和值
}
```

### 总结

范围 `for` 循环提供了一种简洁易懂的方式来遍历容器中的元素，减少了代码量并提高了可读性

