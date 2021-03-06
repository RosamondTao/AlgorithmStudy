# 并查集

### 查询两个样本是否在一个集合（isSameSet(V a, V b)）

各自从两个样本往上面找，找到最后的对应代表点，如果两个代表点是一样的，则说明两个样本在一个集合。



#### 合并两个集合(union(V a, V b))

从样本开始找代表点，找到后小挂大，即让小的代表点不再指向自己，而是指向大的代表点



### 实战

#### 题目描述

学生实例中有三个网站的昵称这三个字段，每个学生有可能有小号。两个实例中一旦有一个字段相同，则证明这两个实例是同一个学生。现给出一堆实例，请问总共有多少个学生。

#### 解决方法

利用并查集。每个实例相当于一个节点，将判断为同一个学生的实例合并为一个union，最后有几个union就是几个学生。

首先建立三个hashmap，每个map记录一个字段和对应的实例的代表点，循环处理每一个实例，一旦发现某个实例的某个字段在对应的hashmap中已存在，则找出其对应的代表点，将当前处理的实例加入该代表点所在的union中。处理完所有实例后统计总共有多少个union





### 并查集写法

```java
class UF {
    private int count;
    private int[] parent;
    private int[] size;
    public UF(int n) {
        this.count = n; //初始时每个结点表示一个集合，故集合数为n
        parent = new int[n];    
        size = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;  //初始时每个节点所在集合的代表点是自己
            size[i] = 1;    //初始时每个节点所在集合的大小都是1（只有自己）
        }
    }
    public void union(int a, int b) {
        int rootA = find(a);
        int rootB = find(b);
        if (rootA == rootB)
            return;
        // 小挂大
        if (size[rootA] > size[rootB]) {
            //将rootB的代表点重新定为rootA，即将rootB为代表的集合挂在rootA为代表的集合下
            parent[rootB] = rootA;
            size[rootA] += size[rootB];
        } else {
            parent[rootA] = rootB;
            size[rootB] += size[rootA];
        }
        count--;
    }

    public boolean isConnected(int a, int b) {
        int rootA = find(a);
        int rootB = find(b);
        return rootA == rootB;
    }

    private int find(int x) {
        while (parent[x] != x) {
            // 进行路径压缩
            parent[x] = parent[parent[x]];
            x = parent[x];
        }
        return x;
    }

    public int getUnionCount() {
        return count;
    }
}
```

