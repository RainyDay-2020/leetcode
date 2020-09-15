#### JZ1.二维数组中的查找

##### 题目描述

```markdown
给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。（注意：规定B[0] = A[1] * A[2] * ... * A[n-1]，B[n-1] = A[0] * A[1] * ... * A[n-2];）
对于A长度为1的情况，B无意义，故而无法构建，因此该情况不会存在。
```

##### 前置知识

##### 思路

1. 两重for循环，在遍历数组A的时候，A[i]赋值为1，计算B[i]。**注意：**需要使用一个临时变量将A[i]的值先保存起来，然后for循环结束后再改变回来。

2. 因为不能用除法，可将B[i]分为两部分计算

   + `left[i]=A[0]*A[1]*...*A[i-1]`

   + `right[i]=A[i+1]*...*A[n-1]`

   + 但是存在的弊端是，如果对每个B[i],0<=i<n，都这么要求的话，显然时间复杂度太高。整个结果如图所示

     ![3](D:\笔记\Git\刷题笔记\牛客网.assets\3.png)

   进一步：

   + `left[i+1]=A[0]*A[1]*...*A[i-1]*A[i]`
   + `right[i+1] = A[i+2]*...*A[n-1]`

   所以

   + `left[i+1]=left[i]*A[i]`
   + `right[i] = A[i+1]*right[i+1]`
   + `B[i]=left[i]*right[i]`

   说明：

   + 即结果为对角矩阵。下三角，从零开始循环，下三角从n-1开始循环，用B[i]代替let[i]，用临时变量tmp代替right[i]

##### 关键点

+ 方法一中是否保存了A[i]的值，计算B[i]时，将A[i]看作1
+ 方法二的关键点在于图，下三角从上往下计算，上三角从下往上计算。累乘

##### 代码

**法一**

```java
import java.util.ArrayList;
public class Solution {
    public int[] multiply(int[] A) {
        int[] B = new int[A.length];
        for(int i = 0; i < A.length; i++){
            int tmp = A[i]; //用临时变量保存A[i]的值
            A[i] = 1;
            B[i] = 1;
            for(int j = 0; j < B.length; j++){
                B[i] *= A[j];
            }
            A[i] = tmp; // 恢复A[i]的值
        }
        return B;
    }
}
```

**法二**

```java
import java.util.ArrayList;
public class Solution {
    public int[] multiply(int[] A) {
        int[] B = new int[A.length];
        B[0] = 1;
        for(int i = 1; i< A.length; i++){
            B[i] = B[i - 1] * A[i-1];
        }
        int tmp = 1;
        for(int j = A.length-2; j >= 0; j--){
            tmp *= A[j+1];
            B[j] *= tmp;
        }
        return B;
    }
}
```



