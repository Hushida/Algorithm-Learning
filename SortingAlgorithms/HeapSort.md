#堆排序
##堆的分类
堆是一个二叉树，按照节点和左右孩子的大小关系可以分为大顶堆和小顶堆

- 大顶堆：每个节点的值都大于等于它的左右孩子的值
- 小顶堆：每个节点的值都小于等于它的左右孩子的值

##堆排序的步骤

- 步骤一：把给的数值构造成一个大顶堆,arr[n]长度位n

          &emsp; 把数组中的元素按照二叉树的格式存储，节点位置为i，则左孩子
             位置2*i + 1, 右孩子的位置 2*i +2
             创建堆的思路heapify()方法：把当前元素和它的孩子进行比较，找出
             其中的最大值记做max，如果当前元素不是最大，就把它的孩子中
             最大的赋给max。

        

- 步骤二：交换末尾元素和堆顶元素
    
    把堆顶元素和n - 1 位置上的元素进行交换，这样就把最大的元素放到了
    数组末尾。这是堆中的元素数量就减少到n -1个。  此时堆中元素的顺序
    可能不符合最大堆定义，所以需要用heapify()方法重建。然后把堆顶
    最大元素和数组倒数第二的元素交换，重复进行这些步骤。知道堆里面
    没有元素了，这时候堆排序也就好了。是一个从小到大排列的数组。

    代码实现（java）：
    

    ```
   public class Heap {
       private[] a;//数组，从下标1开始
       private int n;//数组中元素的最大个数
       private int count;//已经存储的数据个数
       
       public Heap(int capacity) {
           a = new int[capacity + 1];
           n = capacity;
           count = 0;
       }
       public static void insert(int data) {
           if(count >= n) {
           //堆满了
           return;
           }
           ++count;
           a[count] = data;
           int i = count;
           while(i / 2 > 0 && a[i] > a[i / 2]) {
               //交换下标元素，然后从根节点往下比较
               swap(a, i, i / 2);
               i = i / 2;
           }
       }
       public static void heapify(int[] a, int n, int i) {
           int maxPosition = i;
           while(true) {
               if(i < n && a[i*2] > a[i]) {
                   maxPosition = i*2;
               }
               if(i < n && a[i*2 + 1] > a[i]) {
                   maxPosition = i*2 + 1;
               }
               if(i == maxPosition) {
                   break;
               }
               swap(a, i, maxPosition);
               i = maxPosition;
           }
       }
       /从下标n/2位置的数据开始到1，建立堆，相当于从上层往下层建立堆。下标n/2+1到n的数据是叶子节点，最后一层的不需要对他们建立堆，直接从倒数第二层开始建立堆。建立堆的时间复杂度是O(n)，每一个节点在建立堆的过程中，需要比较和交换的次数和这个节点的高度成正比。求和之后，时间复杂度是O(n)。
       public static void buildHeap(int[] a, int n) {
           for(int i = n/2; i >= 1; i--) {
               heapify(a, n, i);
           }
       }
       //排序：大顶堆建立完之后，数组中的数据按照大顶堆的性质来组织，堆顶元素之最大的元素，把最大的元素和数组最后一个位置的元素交换。然后把剩下的n-1个元素重新调整堆，再次把堆顶元素和数组倒数第二个元素交换，重复这个过程，最后堆里面只有一个元素，排序就完成了。
           
       public static void sort(int[] a, int n) {
           //数组中的元素从下标1到n
           buildHeap(a, n);
           int k = n;
           while(k > 1) {
               swap(a, k, 1);
               --k;
               heapify(a, k, 1);
           }
       }
       
   }
    ```
    初始化堆的时间复杂度是O(logn)。   
    更改堆元素之后，调整堆的时候，n-1个元素需要n-1次循环，每次都是从根节点向下查找，时间复杂度是log（n），所以堆排序的时间复杂度是O(nlogn)。    
    堆排序是原地排序，空间复杂度是O(1)    
    堆排序不是稳定的排序，因为在排序的过程中，会把堆的最后一个节点和堆顶元素互换，这个操作会导致相同元素的前后顺序发生变化。
    
    
    
    
    
另一种思路（附java代码实现和测试结果）
堆排序需要两个过程，一是建立堆，另一个是调整堆。  （代码难以理解，左程云书的354页，那个堆排序好理解一些。等待整理）   ：从最后一个右子节点

初始化堆的时间复杂度是O(n)，更改堆元素之后，建立堆，需要循环n-1次，每次是从根节点往下寻找，所以时间复杂度是O(logn)，所以整体的时间复杂度是）O(nlogn)       没有用到辅助空间，堆排序是原地排序，时间复杂度是O(1)  

```
package com.company;
import java.util.Arrays;
public class Sort {
    public static void main(String[] args) {
        int[] arr = {12, 11, 10, 2, 4, 6, 7, 1, 3};
        System.out.println("Before sort" + Arrays.toString(arr));
        //insertSort(arr);
        //mergeSort(arr, 0, arr.length - 1);
        //quickSort(arr, 0, arr.length - 1);
        heapSort(arr);
        System.out.println("After sort" + Arrays.toString(arr));

    }
    

    
    public static void heapSort(int[] arr) {
        int n = arr.length;
        //最后一个有子节点的元素，下标是n/2 - 1.。这些元素都是根节点，有孩子节点，所以heapify的最后一项根节点位置是根据i变化的
        for(int i = n/2 - 1; i >= 0; i--) {
            heapify(arr, n, i);
        }
        for(int i = n-1; i >= 0; i--) {
            //大顶堆的0位置元素最大，把最大的放到数组的最后
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            //调整的堆的大小是不断变化的,堆顶下标始终是0，堆调整的范围在缩小
            heapify(arr, i, 0);
        }
    }
    public static void heapify(int[] arr, int n, int i) {
        int largest = i;//把最大值的下标，初始化为i
        int l = 2*i + 1;
        int r = 2*i + 2;

        //内部不做循环，外层调用者的来控制调用heapify的次数
            if(l < n && arr[l] > arr[largest]) {
                largest = l;
            }
            if(r < n && arr[r] > arr[largest]) {
                largest = r;
            }
            if(largest != i) {
                int temp = arr[i];
                arr[i] = arr[largest];
                arr[largest] = temp;

                heapify(arr, n, largest);
            }

    }
}

```
运行结果
```
Before sort[12, 11, 10, 2, 4, 6, 7, 1, 3]
After sort[1, 2, 3, 4, 6, 7, 10, 11, 12]
```    
