#### JZ8.跳台阶

##### 题目描述

```markdown
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。
```

##### 前置知识

##### 思路

1. f(n) = f(n-1) + f(n-2)
2. f(1) = 1; f(2) = 2

##### 关键点

##### 代码

```java
public class Solution {
    public int JumpFloor(int target) {
        if(target < 0){
            return 0;
        }
        if(target ==1 || target == 2){
            return target;
        }
        int first = 1, second = 2, third = 0;
        for (int i = 3; i <= target; i++) {
            third = first + second;
            first = second;
            second = third;
        }
        return third;
    }
}
```

