每次都把当前元素插入到左边已经排好序的数组当中，保证插入之后，左边的数组仍然有序。    
插入元素和数组的初始顺序有关，如果数组已经部分有序了，需要交换的元素少。  
最好情况下，数组已经有序，只需要N-1次比较，0次交换。  
最坏情况下，数组是逆序的，需要n*(n-1)/2次交换，是N^2级别额交换次数。   
平均时间复杂度是O(n^2)     
稳定性分析：如果插入元素和前面的元素相同，会把插入元素放到相同元素的后面，相等元素的先后顺序没有发生改变，所以是插入排序是稳定的排序。  

插入排序的算法步骤：   
1、从第一个元素开始，认为这个元素已经被排序了
2、取出1下一个元素，在已经排序的元素里，从后往前扫描
3、在已经排序的数组中，如果这个元素大于新元素，就把这个元素移动到下一个位置。  
4、一直往前找，如果找到一个元素小于等于新元素，就停止。  
5、把新元素插入到这个位置。然后重复以上操作。

```
package com.company;
import java.util.Arrays;
public class Sort {
    public static void main(String[] args) {
        int[] arr = {2, 4, 6, 7, 1, 3};
        System.out.println("Before sort" + Arrays.toString(arr));
        insertSort(arr);
        System.out.println("After sort" + Arrays.toString(arr));

    }
    public static void insertSort(int[] arr) {
        for(int i = 1; i < arr.length; i++) {
            //取出下一个元素，已经排序的序列中从后前移动
            int temp = arr[i];
            for(int j = i; i >= 0; j--) {
                if((j > 0) && (arr[j - 1] > temp)) {
                    arr[j] = arr[j - 1];//把元素移动到后面的元素
                    System.out.println("Temping" + Arrays.toString(arr));
                } else {
                    //把新元素插入到这个位置之后
                    arr[j] = temp;
                    System.out.println("sorting" + Arrays.toString(arr) );
                    break;//停止这次循环
                }
            }
        }
    }
}

```
运行结果如下
```
Before sort[2, 4, 6, 7, 1, 3]
sorting[2, 4, 6, 7, 1, 3]
sorting[2, 4, 6, 7, 1, 3]
sorting[2, 4, 6, 7, 1, 3]
Temping[2, 4, 6, 7, 7, 3]
Temping[2, 4, 6, 6, 7, 3]
Temping[2, 4, 4, 6, 7, 3]
Temping[2, 2, 4, 6, 7, 3]
sorting[1, 2, 4, 6, 7, 3]
Temping[1, 2, 4, 6, 7, 7]
Temping[1, 2, 4, 6, 6, 7]
Temping[1, 2, 4, 4, 6, 7]
sorting[1, 2, 3, 4, 6, 7]
After sort[1, 2, 3, 4, 6, 7]
```
