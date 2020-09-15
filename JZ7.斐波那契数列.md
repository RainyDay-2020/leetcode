#### JZ7.斐波那契数列

##### 题目描述

```markdown
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0，第1项是1）。
n<=39
```

##### 前置知识

+ 递归
+ 优化

##### 思路

1. 因为普通的递归算法涉及到大量的重复计算，所以采取用数组把计算过程保存下来，然后直接返回数组即可

##### 关键点

##### 代码

```java
public class Solution {
    public int Fibonacci(int n) {
        if(n <= 1){
            return n;
        }
        else
          return  Fibonacci(n-1) + Fibonacci(n-2);
    }
}
```

```java
public class Solution {
    public int Fibonacci(int n) {
        int ans[] = new int[40];
        ans[0] = 0;
        ans[1] = 1;
        for(int i = 2; i <= n; i++){
            ans[i] = ans[i-1] + ans[i-2];
        }
        return ans[n];
    }
}
```

