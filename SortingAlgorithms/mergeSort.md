归并排序是分治思想的典型应用，把一个问题分解成多个子问题，然后把子问题再次分解成更小的子问题。
把等待排序的序列分成很多个子序列，每一个子序列是有序的，然后把有序的子序列合并成整体有序的序列。
时间复杂度分析。对于长度为n的数组，拆分数组的时间复杂度是logn，合并子数组的过程时间复杂度是O(n)，所以整体的时间复杂度是O(nlogn)。  

空间复杂度分析：递归过程中拆分的数组需要保存在内存中，空间复杂度是O(n)  

从排序的流程可以看出，归并排序的性能和数据的状态无关，时间复杂度始终都是O(nlogn)。
```
package com.company;
import java.util.Arrays;
public class Sort {
    public static void main(String[] args) {
        int[] arr = {12, 11, 10, 2, 4, 6, 7, 1, 3};
        System.out.println("Before sort" + Arrays.toString(arr));
        //insertSort(arr);
        mergeSort(arr, 0, arr.length - 1);
        System.out.println("After sort" + Arrays.toString(arr));

    }
    

    public static void mergeSort(int[] arr, int left, int right ) {
        int mid = left + (right - left)/2;
        if(left < right) {
            //左半边归并排序
            mergeSort(arr, left, mid);
            //右半边归并排序
            mergeSort(arr, mid+1, right);
            merge(arr, left, mid, right);
        }
    }
    public static void merge(int[] arr, int left, int mid , int right) {
        //创建临时数组
        int[] temp = new int[right - left + 1];
        int i = left;
        int j = mid + 1;
        int k = 0;

        //把比较小的数先移入数组
        while((i <= mid) && (j <= right)) {
            if (arr[i] < arr[j]) {
                temp[k++] = arr[i++];
            } else {
                temp[k++] = arr[j++];
            }
        }

            //把左边的元素移入数组
            while(i <= mid) {
                temp[k++] = arr[i++];
            }
            //把右边的元素移入数组
            while(j <= right) {
                temp[k++] = arr[j++];
            }


        for(int k2 = 0; k2 <temp.length; k2++) {
            arr[left + k2] = temp[k2];
        }

    }
}

```
运行结果是
```
Before sort[12, 11, 10, 2, 4, 6, 7, 1, 3]
After sort[1, 2, 3, 4, 6, 7, 10, 11, 12]
```
