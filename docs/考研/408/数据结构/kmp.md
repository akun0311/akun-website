字符串匹配

1. 普通的字符串匹配过程，这个时间复杂度是O((n-m+1)m)
n是
m是模式串
这个字符串匹配过程，需要消耗的时间复杂度是比较高的。

2. KMP模式匹配算法
KMP是三个人名字的字母缩写。

首先对模式串进行一个预处理，这个时间复杂度是O(m)
匹配时间是O(n)
