---
title: Algorithms Learning 

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
# date: '2021-07-01T13:00:00Z'
# date_end: ''
# all_day: false

# Schedule page publish date (NOT talk date).
# publishDate: '2021-07-01T00:00:00Z'

authors: []
tags: []

# Is this a featured talk? (true/false)
featured: false

image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/bzdhc5b3Bxs)'
  focal_point: Right

# links:
#   - icon: twitter
#     icon_pack: fab
#     name: Follow
#     url: https://twitter.com/georgecushen
# url_code: ''
# url_pdf: ''
# url_slides: ''
# url_video: ''

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
  > *适用场景：* 适用于一个区间都要加上/减去一个固定的数字。
  > *原理：*  
  记 $a_0=0$, $b_1=a_1=a_0$, $b_2=a_2-a_1$，依此类推，$b_s=a_s-a_{s-1}$，$b_x=a_x-a_{x-1}$，$b_{t+1}=a_{t+1}-a_t$，$b_n=a_n-a_{n-1}$
  所以a1=b1,a2=b1+b2,a3=b1+b2+b3...an=a1+a2+...+an
  由于要对区间as到at之间的a,每个都要加d,对于b相当于只有bs加了d，bt+1多减去了d,而其余b的大小不变。将区间变化转化为只对新建的b数组中的两个数字做变化。

  > 构建差分数组（构建前记得开辟数组空间： `memset(b,0,size of b);`）
  > ```cpp
  > for(int i=1;i<=n;i++){
  >   b[s[i]]=b[s[i]]+d;
  >   b[t[i]+1]=b[t[i]+1]-d;
  > }
  > ```
  > ps:如果是从原数组直接构建差分数组，for循环要倒序，否则构建会错误。
  > ```cpp
  > for(int i=n+1;i>=1;i--){
  >   b[i]=b[i]-b[i]-1;
  > }
  > ``
  >
  > *相关例题：*
  > 空调：要让一个数组中的所有数字，每次只能选择两个数字进行+1、-1，要让其全减为0。需要的次数即为该差分数组中所有正数的和。


- **二分算法**
  > 在区间[l,r]间逼近一个数字：（1）mid超出区间，则区间在