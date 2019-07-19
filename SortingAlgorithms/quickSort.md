java版本
```
package com.company;
import java.util.Arrays;
public class Sort {
    public static void main(String[] args) {
        int[] arr = {12, 11, 10, 2, 4, 6, 7, 1, 3};
        System.out.println("Before sort" + Arrays.toString(arr));
        //insertSort(arr);
        //mergeSort(arr, 0, arr.length - 1);
        quickSort(arr, 0, arr.length - 1);
        System.out.println("After sort" + Arrays.toString(arr));

    }
    


    public static void quickSort(int[] arr, int start, int end) {

        if(arr == null || start >= end) {
            return ;
        }

        int partitionIndex = divide(arr, start, end);
        quickSort(arr, start, partitionIndex - 1);
        quickSort(arr, partitionIndex + 1, end);

    }
    public static int divide(int[] arr, int start, int end) {
        //选择基准元素
        int base = arr[end];
        //两个指针不相遇，就判断
        while(start < end) {
            while(start < end && arr[start] <= base) {
                start++;
            }
            if(start < end) {
                int temp = arr[start];
                arr[start] = arr[end];
                arr[end] = temp;
                end--;
            }
            while(start < end && arr[end] >= base) {
                end--;
            }
            if(start < end) {
                int temp = arr[start];
                arr[start] = arr[end];
                arr[end] = temp;
                start++;
            }

        }
        //相遇就返回
        return end ;
    }
}

```
代码运行结果 
```
Before sort[12, 11, 10, 2, 4, 6, 7, 1, 3]
After sort[1, 2, 3, 4, 6, 7, 10, 11, 12]
```
