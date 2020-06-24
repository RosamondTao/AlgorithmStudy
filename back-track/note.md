# 回溯算法

### 三问题

1、路径：也就是已经做出的选择。

2、选择列表：也就是你当前可以做的选择。

3、结束条件：也就是到达决策树底层，无法再做选择的条件。



### 算法框架

```java
List result = new LinkedList();
public void backtrack(路径,选择列表){
    if(满足结束条件){
        result.add(结果);
        return;
    }
    for(选择：选择列表){
        做出选择;
        backtrack(路径,选择列表);
        撤销选择;
    }
}
```





### 去重

题目示例：（4）组合总和2（5）全排列2

为方便去重，一般有两步重要代码。

1、排列：`Arrays.sort(candidates)`

2、剪枝：`if(i!=index && candidates[i-1]==candidates[i]) continue; `or`if(i!=0 && candidates[i]==candidates[i-1] && used[i-1]) continue;`