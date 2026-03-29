---
title: reviewing prefix array and KMP algorithm
date: 2026-03-29
author: jjiho0707
---

reference : https://cp-algorithms.com/string/prefix-function.html

KMP algorithm is used when we want to find out how many string pattern occurs in given text.
This algorithm starts from **prefix array** (or fail array)

definition of prefix array $\pi[i]$, for string s[] (these arrays use 0-based indexing)
$pi[i]$ is the maximum length of substring starting from s[0] that equals to substring ending with s[i].
more precisely,

$\pi [i] = max_{k=0,1,2,\cdots,i} (s[0 : k-1] == s[i-k+1 :i])$ (if there's no match, then 0.)

because of this array's special structure, we can make $\pi$ array in linear time $O(n)$. by following algorithm schema



set pi[0] = 0
for i=1:
    consider j = pi[i-1]
    if s[j] == s[i],
        then clearly s[i] is j+1.
    else
        we have to try all prefix ending with s[i-1]. so,
        for j>0:
            j = pi[j-1]
            if s[j] == s[i] then j++ and break.
        s[i] = 0 (there's no match)

this can be written in more compressive cpp code.

```cpp
int pi[MAXN] = {0};
    prefix_function(string s){
        int n = s.length();
        pi[0] = 0;
        for(int i=1;i<n;i++){
            int j=pi[i-1];
            while(s[j]!=s[i] and j>0){
                j = pi[j-1];
            }
            if(s[j]==s[i]){
                s[i] = ++j;
            }
        }
    }
```
from this prefix array, we can count easily how many string a pattern occurs in the target text.
suppose the string pattern that we want to count s[]
and the target pattern t[].
concatenate this two string with separator #(this character should be not included in both string s,t)
i.e. s # t
then make prefix array for this concatenated string.
by the separator, if the value pi[i] in text t equals to n,(the length of pattern string) then we just add one to total count. 
so the time complexity is $O(n+m)$ (n is the length of pattern $s$, and m is the length of target text $t$)



        







