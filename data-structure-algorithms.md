## 算法&数据结构篇
* 链表种类（腾讯－内推3面）
* 哈夫曼树用途？原理（腾讯－内推2面）
* hash算法种类？（腾讯－内推2面）
* 你知道的排序算法（腾讯－内推2面）
* 排序算法比较纬度？（腾讯－内推2面）

* 10G大小的qq号码（有重复），2G内存的电脑。排序按照qq号码次数由多到少输出。（腾讯－内推1面）  
  利用hash算法hash到文件中，统计次数，然后多路归并

* 手写二叉树的后序非递归遍历（腾讯－校招1面）  
  这里写出来的时候，面试官不认同，后来和他讲明白了
  ```javascript
  function postOrder(root) {
    if(!root) {
      return;
    }
    let stack = [];
    let ptr = root, pre;
    while(ptr && ptr.left != null) {
      stack.push(ptr);
      ptr = ptr.left;
    }
    while(ptr.right == null || ptr.right == pre) {
      visit(ptr);
      pre = ptr;
      if(stack.length == 0) {
        return;
      }
      ptr = stack.shift();
    }
    stack.push(ptr);
    ptr = ptr.right;
  }
  ```
* 口述快排（腾讯－校招1面）
* 手写字符串匹配（百度－校招1面）  
朴素模式
```javascript
function indexOf(str, subStr) {
  for(let i = 0, ii = str.length; i < ii; ) {
    if(str.charAt(i) === subStr.charAt(0)) {
      let j, jj;
      for(j = 1, jj = subStr.length; j < jj; ) {
        if(str.charAt(i + j) !== subStr.charAt(j)) {
          break;
        }
      }
      if(j == jj) {
        return i;
      }
    }
    i += 1;
  }
  return -1;
}
```
* hash算法冲突问题（百度－校招1面）
* 手写归并排序递归和非递归（今日头条－校招1面）
```javascript
function merge(arr, start, mid, end) {
  let temp = [];
  let i = start, j = mid;
  while(i < mid && j <= end) {
    if(arr[i] <= arr[j]) {
      temp.push(arr[i]);
    } else {
      temp.push(arr[j]);
    }
  }
  if(i < mid) {
    temp = temp.concat(arr.slice(i, mid));
  }
  if(j <= end) {
    temp = temp.concat(arr.slice(j, end + 1));
  }
  for(let i = start, j = 0; i <= end; ) {
    arr[i++] = temp[j++];
  }
}
function mergeSort(arr, start, end) {
  let mid;
  if(start < end) {
    mid = (start + end ) / 2;
    mergeSort(arr, start, mid);
    mergeSort(arr, mid + 1, end);
    merge(arr, start, mid, end);
  }
}
```
* 编辑距离算法（今日头条－校招2面）
* 手写快排实现（今日头条－校招3面）
```javascript
function partion(arr, start, end) {
  let pviot = arr[start];
  while(start < end) {
    while(start < end && arr[end] >= pviot) {
      end--;
    }
    arr[start] = arr[end];
    while(start < end && arr[start] <= pviot) {
      start++;
    }
    arr[end] = arr[start];
  }
  return start;
}

function quickSort(arr, start, end) {
  if(start < end) {
    let mid = partion(arr, start, end);
    quickSort(arr, start, mid - 1);
    quickSort(arr, mid + 1, end);
  }
}
```
* 网页中距离当前鼠标位置最近的链接（小米－校招3面）  
我的想法是把把页面中的链接抽象成点，计算的时候就是```o(n)```

* 树中节点含有url，请求所有节点中的链接，考虑系统并发 （小米－校招3面）
* 合并两个有序数组，使之仍然有序（美团－实习1面）
* 数组去重（美团－实习1面）