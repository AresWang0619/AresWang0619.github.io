---
title: Algorithm Learning 

# event: 
event_url: https://leetcode.cn/u/ares-na4/

# location: leetcode
# address:
#   street: 450 Serra Mall
#   city: Stanford
#   region: CA
#   postcode: '94305'
#   country: United States

summary: C/C++/Python 算法学习合集
abstract: '一些算法学习小tips'

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: '2024-04-21T21:25:00Z'
# date_end: ''
# all_day: false

# Schedule page publish date (NOT talk date).
# publishDate: '2021-07-01T00:00:00Z'

authors: [Ares]
tags: []

# Is this a featured talk? (true/false)
featured: false

image:
  caption: 'bigbang theory'
  focal_point: Right


# Markdown Slides (optional).
#   Associate this talk with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides: example

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects:
#   - example
---
<!-- 
{{% callout note %}}
Click on the **Slides** button above to view the built-in slides feature.
{{% /callout %}}

Slides can be added in a few ways:

- **Create** slides using Hugo Blox Builder's [_Slides_](https://docs.hugoblox.com/reference/content-types/) feature and link using `slides` parameter in the front matter of the talk file
- **Upload** an existing slide deck to `static/` and link using `url_slides` parameter in the front matter of the talk file
- **Embed** your slides (e.g. Google Slides) or presentation video on this page using [shortcodes](https://docs.hugoblox.com/reference/markdown/).

Further event details, including [page elements](https://docs.hugoblox.com/reference/markdown/) such as image galleries, can be added to the body of this page. -->
- **区间更新:差分算法**
  > <u>*适用场景*</u> ：适用于一个区间都要加上/减去一个固定的数字。
  >
  > **原理:** 
  > 
  > a_0=0, b_1=a_1=a_0, b_2=a_2-a_1, b_s=a_s-a_{s-1}, b_x=a_x-a_{x-1}, b_{t+1}=a_{t+1}-a_t, b_n=a_n-a_{n-1}
  > 

  > 所以a_1=b_1,a_2=b_1+b_2,a_3=b_1+b_2+b_3...a_n=a_1+a_2+...+a_n
  > 由于要对区间 a_s 到 a_t 之间的 a ,每个都要加 d ,对于 b 相当于只有 b_s 加了 d，b_t+1 多减去了 d ,而其余 b 的大小不变。将区间变化转化为只对新建的b数组中的两 
  > 个数字做变化。
  >
  > **Key part:**
  > 构建差分数组（构建前记得开辟数组空间： `memset(b,0,sizeof(b));`）
  > ```cpp
  > for(int i=1;i<=n;i++){
  >   b[s[i]]=b[s[i]]+d;
  >   b[t[i]+1]=b[t[i]+1]-d;
  > }
  > ```
  > ps:如果是从原数组直接构建差分数组，for循环要倒序，否则构建会错误。
  > ```cpp
  > for(int i=n+1;i>=1;i--){
  >   b[i]=b[i]-b[i-1];
  > }
  > ```
  >
  > <u>*相关例题*</u> ：
  >
  > 4262空调：要让一个数组中的所有数字，每次只能选择两个数字进行+1、-1，要让其全减为0。需要的次数即为该差分数组中所有正数的和。

---

- **二分算法**
  > <u>*适用场景*</u> ：在区间 [l, r] 间逼近一个数字：
  >
  > **原理:** 
  > 1. 如果 mid 超出区间，则区间在 [l, mid]；
  > 2. 如果 mid 不会超出区间，则区间在 [mid+1, r]。
  > 
  > 直到区间内只剩一个数，结束迭代。
  >
  > **Key part:**
  > ```cpp
  > int l=0,r=n;
  > while(l<n){
  >   int mid=l+r+1>>1;
  >   if(check(mid)) l=mid;
  >   else r=mid-1;
  > }
  > return r;
  > ```

---
- **前缀和**
  > <u>*适用场景*</u>：求任意区间内数字的总和。
  >
  > **原理:** 
  > 构建前缀和数组
  >
  > 设 s_0=0, s_1=a_1, s_2=a_1+a_2, ..., s_{i-1}=a_1+a_2+...+a_{i-1}, s_i=a_1+a_2+...+a_i, s_n=a_1+a_2+...+a_n。
  >
  > 可以知道，s_1-s_{i-1}=a_i, s_i=a_i+s_{i-1}。所以，想得到 a_1+a_2+...+a_r，可以转化为求 s_k-s_{l-1}。
  >
  > ps:
  > 1. 记住要从1开始构建前缀和数组。
  > 2. C++的头部: `#include <iostream>`，`using namespace std;` 包含 `max` 函数。
  > 3. `scanf("%s",str+1)` 相当于数组指针后移，从第一个数字开始。
  >
  >
  > <u>*相关例题*</u>: 
  >
  > 562壁画：用for循环遍历m~n,在此区间内找和max的区间,区间大小为m.


---

- **双指针**
  > <u>*适用场景*</u> ：对于每一个i来说，在一个<u> 单调</u> 递减的数组里找到>=它的最后一个数字。（此处单调指的是一个下标关于另一个下标单调），适用于有序数组，属于优化算法。
  >
  > **原理:** 
  > h指数：大于等于 `h` 的数字至少有 `h` 个（在所有满足 `h` 的数字中取 `max`）。
  >
  > **Key part:**
  > ```cpp
  > for(int i=1,j=n;i<=n;i++){
  >  while(w[j]<i&&j) j--;
  >  if(w[i]>=i-1&&i-j<=l)
  >      res=i;
  > }
  > ```
  > 1. C++ `sort` 用法：`sort(起始位置，终止位置，排序方式)`；例如：`sort(w + 1, w + n + 1, greater<int>());`，`sort(a.begin(), a.> 
  end())`。
  > 2. `b = num.size()`
  >
  >
  > <u>*相关例题*</u>: 
  >
  > 3745 牛的学术圈：用 `for` 循环遍历 `m` 到 `n`，在此区间内找和 `max` 的区间，区间大小为 `m`。

  ---
- **归并排序**
  >
  > **Key part：**
  > ```cpp
  > void merge_sort(int q[], int l, int r){
  >     if(l >= r) return;
  >     
  >     int mid = l + r >> 1;
  >     merge_sort(q, l, mid);
  >     merge_sort(q, mid + 1, r); // 递归
  > 
  >     int k = 0, i = l, j = mid + 1;
  > 
  >     while(i <= mid && j <= r){
  >         if(q[i] <= q[j]){
  >             tmp[k++] = q[i++];
  >         } else {
  >             tmp[k++] = q[j++];
  >         } // 较小的数字加入 tmp 数组
  >     } 
  > 
  >     while(i <= mid) tmp[k++] = q[i++];
  >     while(j <= r) tmp[k++] = q[j++]; // 处理一个数组已经复制完的情况
  > 
  >     for(i = l, j = 0; j <= k; i++, j++)
  >         q[i] = tmp[j];
  > }
  > ```

  > <u>*相关例题*</u>: 
  >
  > 505 火柴排队:
  > 
  > 1. 若结果跟数组内具体大小无关，只需相对大小，即可进行离散化，将数组内的数字离散化到1~n。
  > 
  > **离散化Key part：**
  > ```cpp
  > for(int i = 1; i <= n; i++) p[i] = i; // 先将下标记录
  > sort(p + 1, p + n + 1, [&](int x, int y){
  >       return a[x] < a[y];
  >   }); // sort 完之后满足 a_p1 < a_p2 < a_p3 ...
  > 
  > for(int i = 1; i <= n; i++){
  >     a[p[i]] = i;
  > }
  > ```
  >
  > 2. A、B 数组都是乱序的，则对其进行数组映射，将数组 A 内的数字映射为 1，2，3，4，5...，用 C 数组存储谁映射到谁：A 当中第 1 个数映射到 1 (第 i 个数映射到 i)，B 数组通过 C 数组来构建。
  > 
  > **数组映射构建Key part：**
  > ```cpp
  > // A 的映射
  > for(int i = 1; i <= n; i++){
  >     a[p[i]] = i;
  > }
  > 
  > // C 数组的构建
  > for(int i = 1; i <= n; i++){
  >     c[a[i]] = i;
  > }
  > 
  > // B 数组的构建
  > for(int i = 1; i <= n; i++){
  >     b[i] = c[b[i]];
  > }
  > ```
  > 
  > 3. 所以，至此，题目可以转化为：两个数组 a, b，要使得其中数字差值 min，首先要将 a，b 数组进行排序，求他们的逆序对数（通过归并排序求得），逆序对数就等于最少需要交换的次数。若当 a 映射后形成升序的数组，但是 b 还是乱序的，所以最终的交换次数 = b 中的逆序对数。
  > 
  > **逆序对数Key part：**
  > ```cpp
  > int res = (merge_sort(l, mid) + merge_sort(mid + 1, r)) % MOD;
  > // 当出现逆序对，因为 i < mid < j，只有 i~mid 之间的数字要做交换
  > if(b[j] < b[i]) res = (res + mid - i + 1) % MOD;
  > ```
