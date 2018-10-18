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

public void  heapCreate(int[] arr, int value, int index) {
  arr[index] = value;
  while(index != 0) {
    parent = (index - 1)/2;
    if(arr[parent] < arr[index]) { /为了使父节点的值比子节点的值大
      swap(arr, parent, index);
      index = parent;
    } else {
      break;
    }
  }
}

public void heapify(int arr, int index, int heapSize) {
  int left = index * 2 + 1;
  int right = index * 2 + 2;
  int largest = index;
  while(left < heapSize) { //首先判断异常，检查左子节点下标是否超出数组范围，然后在循环内判断右子节点下标是否超出数组范围
    if(arr[left] > arr[largest]) {
      largest = left;
    }
    if(right < heapSize && arr[right] > arr[largest]) {
      largest = right;
    }
    if(arr[largest] > arr[index]) {
      swap(arr, largest);
    }
    index = largest;
    left = index * 2 + 1;
    right = index * 2 + 2;
  }
}

public void swap(int[] arr, int index1, int index2) {
  int temp = arr[index1];
  arr[index1] = arr[index2];
  arr[index2] = temp;
}
```
