# 二分查找

### 模板

网上很多利用排除法的左边界右边界什么的一大堆模板，看的人挺晕，目前就我做的题而言，没有必要。

这里只用一种最简单的模板和四个变形来解决二分查找问题。

```java
public int bsearch(int[] a, int n, int value) { 
    int low = 0; 
    int high = n - 1; 
    while (low <= high) { 
        int mid = (low + high) / 2; 
        if (a[mid] == value) { 
            return mid; 
        } else if (a[mid] < value) { 
            low = mid + 1; 
        } else { 
            high = mid - 1; 
        } 
    } 
    return -1;
}
```

如上，分三部分的模板，是最简单最容易理解的二分查找模板。

对于以上模板无法解决的几个变体问题，如：

- 查找第一个值等于给定值的元素
- 查找最后一个值等于给定值的元素
- 查找第一个大于等于给定值的元素
- 查找最后一个小于等于给定值的元素

模板如下：

```java
//查找第一个值等于给定值的元素
public int bsearch(int[] a, int n, int value) { 
    int low = 0; 
    int high = n - 1; 
    while (low <= high) {
        int mid = low + ((high - low) >> 1); 
        if (a[mid] > value) { 
            high = mid - 1; 
        } else if (a[mid] < value) { 
            low = mid + 1; 
        } else { 
            if ((mid == 0) || (a[mid - 1] != value)) return mid; 
            else high = mid - 1; 
        } 
    } 
    return -1;
}
```



```java
//查找最后一个值等于给定值的元素
public int bsearch(int[] a, int n, int value) { 
    int low = 0; 
    int high = n - 1; 
    while (low <= high) { 
        int mid = low + ((high - low) >> 1); 
        if (a[mid] > value) { 
            high = mid - 1; 
        } else if (a[mid] < value) { 
            low = mid + 1; 
        } else { 
            if ((mid == n - 1) || (a[mid + 1] != value)) return mid; 
            else low = mid + 1; 
        } 
    } 
    return -1;
}
```

```java
//查找第一个大于等于给定值的元素
public int bsearch(int[] a, int n, int value) {
  int low = 0;
  int high = n - 1;
  while (low <= high) {
    int mid =  low + ((high - low) >> 1);
    if (a[mid] >= value) {
      if ((mid == 0) || (a[mid - 1] < value)) return mid;
      else high = mid - 1;
    } else {
      low = mid + 1;
    }
  }
  return -1;
}
```

```java
//查找最后一个小于等于给定值的元素
public int bsearch7(int[] a, int n, int value) {
  int low = 0;
  int high = n - 1;
  while (low <= high) {
    int mid =  low + ((high - low) >> 1);
    if (a[mid] > value) {
      high = mid - 1;
    } else {
      if ((mid == n - 1) || (a[mid + 1] > value)) return mid;
      else low = mid + 1;
    }
  }
  return -1;
}
```





### 一些记录

https://leetcode-cn.com/problems/search-insert-position/solution/te-bie-hao-yong-de-er-fen-cha-fa-fa-mo-ban-python-/

上面链接使用排除法，分两部分而不是三部分处理，循环条件是`while(left<right)`而不是`while(left<=right)`。

除此外说了左右边界的一些问题，`left=mid+1;right=mid;`的情况计算mid时向下取整；`left=mid;right=mid-1;`的情况计算mid时向上取整

https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/er-fen-cha-zhao-xiang-jie

这个基本同上。