---
layout: post
title:  "Redis 数据结构与对象"
categories: redis 
tags: redis 数据结构 跳表
author: sukbear
---

* content
{:toc}
# Redis 数据结构与对象
## SDS 简单动态字符串
#### sds结构
```c
struct sdshdr{
    //所保存字符串的长度
    int len;
    //buf数组中未使用的长度
    int free;
    //字节数组，保存字符串
    char buf[];   
}
```
#### SDS和C字符串的区别
- 常数复杂度获取字符串长度 strlen。
- 杜绝缓冲区溢出:strcat函数执行时假定用户在执行这个函数时已分配足够多的内存（空间），sds在执行拼接操作时会检查长度然后决定是否扩展。
- 减少修改字符串时带来的内存重新分配的次数（利用未使用空间，实现空间预分配和惰性空间释放两种优化策略）
- 二进制安全
- 兼容部分c字符串函数

#### 总结
![](http://sowcar.com/t6/680/1552398532x1965165908.jpg)