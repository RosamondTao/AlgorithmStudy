# N皇后问题

### 题目来源

https://leetcode-cn.com/problems/n-queens/



### 题目描述

> N皇后问题研究的是如何将 *n* 个皇后放置在 *n*×*n* 的棋盘上，并且使皇后彼此之间不能相互攻击。
>
> 给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。
>
> 每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

示例

> 输入: 4
> 输出: [
>  [".Q..",  // 解法 1
>   "...Q",
>   "Q...",
>   "..Q."],
>
>  ["..Q.",  // 解法 2
>   "Q...",
>   "...Q",
>   ".Q.."]
> ]
> 解释: 4 皇后问题存在两个不同的解法。



### 思路

以四皇后为例，当第一行选择位置0时，path为[0]，并且通过getChosenList方法得到下一行可选的位置列表ChosenList为[2,3]，下一行选择位置2时，path为[0,2]，ChosenList为[]，无可选位置，则剪枝回退选择位置3，继续寻找。

![四皇后](.\images\IMG_0604.PNG)

### 代码

```java
class Solution {
    
    private List<List<String>> res = new ArrayList<>();
    public List<List<String>> solveNQueens(int n) {
        List<Integer> path = new ArrayList<>();
        backTrack(path, n, getChosenList(path,n));
        return res;
    }

    //形参中包含路径path和选择列表chosenList
    private void backTrack(List<Integer> path, int n, List<Integer> chosenList){
        if(path.size()==n){	//终止条件
            res.add(answerPrint(path));
            return;
        }
        if(chosenList.isEmpty()) return;	//如果选择列表为空则剪枝
        for(int choice: chosenList){	//处理选择列表中的每一个选择
            path.add(choice);	//做选择
            backTrack(path, n, getChosenList(path,n));
            path.remove(path.size()-1);	//撤销选择
        }
    }

    //根据已有路径获取选择列表
    private List<Integer> getChosenList(List<Integer> path, int n){
        int currentRow = path.size();
        List<Integer> chosenList = new ArrayList<>();
        for(int i=0; i<n; i++){
            chosenList.add(i);
        }
        for(int row=0; row<currentRow; row++){
            int col = path.get(row);
            int xie = currentRow-row;
            chosenList.remove(Integer.valueOf(col));    //去掉同列
            chosenList.remove(Integer.valueOf(col-xie));    //去掉左斜下
            chosenList.remove(Integer.valueOf(col+xie));    //去掉右斜下
        }
        return chosenList;
    }

    //eg.输入[1,3,0,2],输出[".Q.."， "...Q","Q...","..Q."]
    private List<String> answerPrint(List<Integer> path){
        int n = path.size();
        List<String> pathList = new ArrayList<>();
        for(int i=0; i<n; i++){
            String str = "";
            for(int j=0; j<n; j++){
                if(j==path.get(i)) str+="Q";
                else str+=".";
            }
            pathList.add(str);
        }
        return pathList;
    }
}
```

