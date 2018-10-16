# 给定一个无序的整形数组arr，找到其中的最小的K个数
这是一个较为典型的的topK问题，根据方法的不同，会有三种时间复杂度
1. 时间复杂度O(NlogN)
2. 时间复杂度O(Nlogk)
3. 时间复杂度O(N)

#### 时间复杂度为O(Nlogk)的方法
思路：维护一个有k个数的大根堆，这个堆中元素是目前选出的K个最小的元素，其中堆顶元素是这K个数中最大的哪一个数。
```
public int[] getMinKNumbersByHeap(int[] arr, int k) {
  //首先处理参数异常处理，提升代码稳定性
  if(k < 1 || k > arr.length) {
    return arr;
  }
  int[] heapK = new int[k];
  for(int i = 0; i < k; i++) {
    heapCreate(heapK, arr[i], i); //先建立一个有k个元素的大根堆
  }
  for(int i = k; i < arr.length; i++) {
    if(arr[i] < heapK[0]) {
      heapK[0] = arr[i];
      heapify(heapK, 0, k); //重新调整heapK数组中元素的顺序，保证堆顶元素是最大的哪一个
    }
  }
  return heapK;
}
```
