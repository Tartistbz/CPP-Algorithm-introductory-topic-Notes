# P1511 子数整数

## 题目描述

对于一个五位数 $\overline{a_1a_2a_3a_4a_5}$，可将其拆分为三个子数：

$sub_1=\overline{a_1a_2a_3}$

$sub_2=\overline{a_2a_3a_4}$

$sub_3=\overline{a_3a_4a_5}$

例如，五位数 $20207$ 可以拆分成

$sub_1=202$

$sub_2=020\ (=20)$

$sub_3=207$

现在给定一个正整数 $K$，要求你编程求出 $10000$ 到 $30000$ 之间所有满足下述条件的五位数，条件是这些五位数的三个子数 $sub_1,sub_2,sub_3$ 都可被 $K$ 整除。

## 输入格式

一个正整数 $K$。

## 输出格式

每一行为一个满足条件的五位数，要求从小到大输出。不得重复输出或遗漏。如果无解，则输出 `No`。

## 样例 #1

### 样例输入 #1

```
15
```

### 样例输出 #1

```
22555
25555
28555
30000
```

## 提示

$0<K<1000$

My Code:

```cpp
#include <iostream>    
int main(){
   int k = 0,top=0;
   //boool top=false;
   std::cin>>k;
   for(int i=10000;i<=30000;i++){
      int s1 = i/100;
      int s2 = (i-(i/10000)*10000)/10;
      int s3 = i-(i/10000)*10000-((i-(i/10000)*10000)/1000)*1000;
      if (s1%k==0&&s2%k==0&&s3%k==0)
      {
         std::cout<<i<<std::endl;
         top=1;
      }
   }
   while (!top)
   {
      std::cout<<"No"<<std::endl;
      top=1;
   }
}                                                    
```





# P1152欢乐的跳

## 题目描述

一个 $n$ 个元素的整数数组，如果数组两个连续元素之间差的绝对值包括了 $[1,n-1]$ 之间的所有整数，则称之符合“欢乐的跳”，如数组 $\{1,4,2,3\}$ 符合“欢乐的跳”，因为差的绝对值分别为：$3,2,1$。

给定一个数组，你的任务是判断该数组是否符合“欢乐的跳”。

## 输入格式

每组测试数据第一行以一个整数 $n(1 \le n \le 1000)$ 开始，接下来 $n$ 个空格隔开的在 $[-10^8,10^8]$ 之间的整数。

## 输出格式

对于每组测试数据，输出一行若该数组符合“欢乐的跳”则输出 `Jolly`，否则输出 `Not jolly`。

## 样例 #1

### 样例输入 #1

```
4 1 4 2 3
```

### 样例输出 #1

```
Jolly
```

## 样例 #2

### 样例输入 #2

```
5 1 4 2 -1 6
```

### 样例输出 #2

```
Not jolly
```

## 提示

$1 \le n \le 1000$

My Code:

```cpp
#include <iostream>
#include <cmath>

using namespace std;

int main() {
    int n = 0;
    while (cin >> n)
    {
      int num[1000];
      for(int i=0;i<n;i++){
         cin >> num[i];
      }
      if(n==1){
         cout<<"Jolly"<<endl;
         continue;
      }
      bool visited[1000]={false};
      bool isJolly = true;
      for(int i=1;i<n;i++){
         int diff = abs(num[i]-num[i-1]);
         if(diff<1 || diff>=n ||visited[diff]){
            isJolly = false;
            break;
         }
         visited[diff] = true;
      }
      if(isJolly){
         cout<<"Jolly"<<endl;
         break;
      }else{
         cout<<"Not jolly"<<endl;//注意大小写
         break;
      }
    }
}

```

GPT:

```CPP
#include <iostream>
#include <vector>
#include <cmath>
#include <algorithm>

using namespace std;

int main() {
    int n;
    while (cin >> n) {
        vector<int> nums(n);
        for (int i = 0; i < n; ++i) {
            cin >> nums[i];
        }
        
        if (n == 1) {
            cout << "Jolly" << endl;
            continue;
        }
        
        vector<int> differences;
        for (int i = 1; i < n; ++i) {
            int diff = abs(nums[i] - nums[i - 1]);
            differences.push_back(diff);
        }
        
        // Sort and remove duplicates from differences
        sort(differences.begin(), differences.end());
        differences.erase(unique(differences.begin(), differences.end()), differences.end());
        
        // Check if differences contains all numbers from 1 to n-1
        bool isJolly = true;
        for (int i = 1; i <= n - 1; ++i) {
            if (find(differences.begin(), differences.end(), i) == differences.end()) {
                isJolly = false;
                break;
            }
        }
        
        if (isJolly) {
            cout << "Jolly" << endl;
            break;
        } else {
            cout << "Not jolly" << endl;
            break;
        }
    }
    
    return 0;
}

```

### 代码解释

#### 头文件包含

```cpp
#include <iostream>
#include <vector>
#include <cmath>
#include <algorithm>

using namespace std;
```

- **`<iostream>`**：这是C++标准输入输出流库，用于处理输入输出操作，比如 `cin` 和 `cout`。
- **`<vector>`**：这是C++标准容器库中的一部分，用于管理动态数组，提供了更方便和安全的数组操作方法。
- **`<cmath>`**：这是C++数学库，提供了数学运算函数，比如 `abs()` 函数用于计算绝对值。
- **`<algorithm>`**：这是C++算法库，提供了各种常用算法函数，比如 `sort()` 用于排序，`find()` 用于查找元素。

#### 主函数 `main()`

```cpp
int main() {
    int n;
    while (cin >> n) {
        vector<int> nums(n);
        for (int i = 0; i < n; ++i) {
            cin >> nums[i];
        }
        
        if (n == 1) {
            cout << "Jolly" << endl;
            continue;
        }
        
        vector<int> differences;
        for (int i = 1; i < n; ++i) {
            int diff = abs(nums[i] - nums[i - 1]);
            differences.push_back(diff);
        }
        
        // Sort and remove duplicates from differences
        sort(differences.begin(), differences.end());
        differences.erase(unique(differences.begin(), differences.end()), differences.end());
        
        // Check if differences contains all numbers from 1 to n-1
        bool isJolly = true;
        for (int i = 1; i <= n - 1; ++i) {
            if (find(differences.begin(), differences.end(), i) == differences.end()) {
                isJolly = false;
                break;
            }
        }
        
        if (isJolly) {
            cout << "Jolly" << endl;
        } else {
            cout << "Not jolly" << endl;
        }
    }
    
    return 0;
}
```

#### 代码解释

- **输入处理**：
  - `int n;` 定义整数变量 `n` 用于存储数组长度。
  - `while (cin >> n)` 循环读取输入，直到没有更多数据为止。
  - `vector<int> nums(n);` 创建一个整数类型的动态数组 `nums`，大小为 `n`。
  - `for (int i = 0; i < n; ++i)` 循环读取 `n` 个整数存入 `nums` 数组中。
- **特殊情况处理**：
  - `if (n == 1)` 如果数组长度为 `1`，直接输出 `Jolly` 并继续下一次输入处理。
- **计算差的绝对值**：
  - `vector<int> differences;` 创建一个整数类型的动态数组 `differences` 用于存储相邻元素之间的差的绝对值。
  - `for (int i = 1; i < n; ++i)` 循环计算相邻元素之间的差的绝对值，并将其存入 `differences` 数组中。
- **排序与去重**：
  - `sort(differences.begin(), differences.end());` 对 `differences` 数组进行排序，以便后续检查。
  - `differences.erase(unique(differences.begin(), differences.end()), differences.end());` 使用 `unique` 函数去除 `differences` 数组中的重复元素，并返回一个指向新的逻辑末端之后的元素的迭代器。
- **判断是否符合条件**：
  - `bool isJolly = true;` 定义布尔类型变量 `isJolly`，用于标记是否为 "Jolly" 数组。
  - `for (int i = 1; i <= n - 1; ++i)` 循环检查 `differences` 数组中是否包含 `[1, n-1]` 范围内的所有整数。
  - `if (find(differences.begin(), differences.end(), i) == differences.end())` 使用 `find` 函数查找 `differences` 数组中是否包含 `i`，如果不包含则将 `isJolly` 置为 `false`。
- **输出结果**：
  - `if (isJolly)` 如果 `isJolly` 为真，则输出 `"Jolly"`，表示该数组是 "Jolly" 数组。
  - `else` 如果不满足条件，则输出 `"Not jolly"`。

这样的实现利用了标准库提供的容器和算法，使得代码结构更清晰和易于理解，但如果你想更深入地理解和掌握 C++，建议逐步学习和实践这些库函数的使用方式。