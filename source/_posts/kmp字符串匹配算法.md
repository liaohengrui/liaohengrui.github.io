---
title: 'kmp匹配算法'
date: 2019-05-22 16:23:03
tags:
	- 算法
---

我想实现ac自动机

<!--more-->

# 前言
为了解决字符串匹配的难题，通常我们使用正则表达式+工具类解决此类问题。BUT我有一个大胆的想法，想自己动手弄一弄这个匹配问题，于是乎百度到了这个算法KMP
# kmp介绍
一个字符串"abaabaabbabaaabaabbabaab"，找到其中子串“abaabbabaab”。传统做法就是字符串和其子串，一个一个比较，如果匹配失败就往后移动一位，继续死板的重新匹配。所以效率太低。
kmp是如何解决这个问题的呢？
首先我们不难发现如果子串“abaabbabaab”如果出现下面这样的情况
![](https://images.cnblogs.com/cnblogs_com/SYCstudio/1036212/o_KMP2-2.gif)
A的第5位和B的第5位不匹配，匹配失败，我们完全可以跳过N个继续匹配，不用死板的将A往后移一位重新匹配（也就是一开始从A的下标1开始匹配，失败重新下标2开始匹配）。
问题来了如何找到N是多少呢？这就是KMP的核心，找到N，大步移动，省去不必要的匹配比较。
# 前缀数组Next[]
为了解决N,我们使用一个数组Next，我们设置next[0]=-1，表示0号元素的没有前缀与它相匹配。
所以可以推理出next[2]=-1,next[3]=0,next[4]=0...
这里有个技巧，前面的数字好看出来，一眼望穿，但是怎么写代码呢？我先把公式列出来
next[t]=b[next[t-1]]+1
为什么是这样呢？我们不妨这么理解
第T个元素的前缀一定包含了T-1个元素的前缀，如（abab）最后一个b包含了的前缀是ab，那它一定包含了aba最后一个a的前缀a
但是如果如果b[t]!=b[next[t-1]+1]怎么办，沒事啊，抽象的理解下，我需要的是b[t]==b[next[t-1]+1]，既然匹配失败，那么我把t-1=next[t-1]不就行了,反正前缀长的和后缀一样，再去寻找它的前缀即可，于是出现了
```c++
while (j >= 0 && pattern[j + 1] != pattern[i]) {
			j = next[j];
}
```
代码实现
``` c++
int* compute_prefix(const string& pattern) {
	int next[100];
	next[0] = -1;
	for (int i = 1; i < pattern.size(); i++) {
		int j = next[i - 1];
		while (j >= 0 && pattern[j + 1] != pattern[i]) {
			j = next[j];
		}
		if (pattern[j + 1] == pattern[i]) {
			next[i] = j + 1;
		} else {
			next[i] = -1;
		}
	}
	return next;
}
```

# 字符串匹配
这个简单了,既然已近有了前缀数组next，实现它显得轻而易举，不匹配直接跳到前缀去
pos = next[pos - 1] + 1;
代码实现
```c++
void kmp_match(const string& text, const string& pattern) {
	int next[100];
	int* nexts = compute_prefix(pattern);
	for (int i = 0; i < 100; i++) {
		next[i] = nexts[i];
	}
	int i = 0;
	int pos = 0;
	while (i<text.size()) {
		if (text[i] == pattern[pos]) {
			i++;
			pos++;
			if (pos==pattern.size()) {
				cout << "匹配成功  " << i - pos << endl;
				pos = next[pos - 1] + 1;
			}
		} else {
			if (pos == 0) {
				i++;
			} else {
				pos = next[pos - 1] + 1;
			}
		}
	}
}
```