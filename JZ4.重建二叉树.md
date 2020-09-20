#### JZ4.重建二叉树

##### 题目描述

```markdown
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。
```

##### 前置知识

+ 前序遍历序列：根左右
+ 中序遍历序列：左根右

##### 思路

1.  如果数组为空，返回null
2. 如果数组的长度为1，新建一个根节点并返回
3. 通过pre[0]获取根节点的值，并找出root节点在中序遍历序列中所处的位置
4. 递归生成左右子树：中序遍历序列中根节点左边的为左子树的节点，右边的为右子树的节点
   1. 对左子树的所有节点进行递归建树
   2. 对右子树的所有节点进行递归建树

##### 关键点

```markdown
Arrays.copyOfRange(T[ ] original,int from,int to)

将一个原始的数组original，从下标from开始复制，复制到上标to，生成一个新的数组。注意这里包括下标from，不包括上标to。[左闭右开)

使用前需要导入java.util.Arrays包

比循环复制数组效率要高
```

##### 代码

```java
import java.util.Arrays;
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

public class Solution {
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        if(pre.length == 0){
            return null;
        }
        
        //根节点为前序遍历第一个节点
        int rootVal = pre[0];
        
        //数组长度仅为1的时候就要处理
        if(pre.length == 1){
            return new TreeNode(rootVal);
        }
        
        // 我们先找到root所在的位置，确定好前序和中序左子树和右子树序列的范围
        TreeNode root = new TreeNode(rootVal);
        int rootIndex = 0;
        for(int i = 0; i < in.length; i++){
            if(rootVal == in[i]){
                rootIndex = i;
                break;
            }
        }
        
        // 递归，假设root的左右子树都已经构建完毕，那么只要将左右子树安到root左右即可
        root.left = reConstructBinaryTree(Arrays.copyOfRange(pre,1,rootIndex+1),Arrays.copyOfRange(in,0,rootIndex));
        root.right = reConstructBinaryTree(Arrays.copyOfRange(pre,rootIndex+1,pre.length),Arrays.copyOfRange(in,rootIndex+1,in.length));
        return root;
        
    }
}
```



