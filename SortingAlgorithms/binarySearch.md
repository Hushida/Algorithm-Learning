递归实现
```
/**
 * 
 * @Author Hushida
 * @date 2018.12.3
 * @description :递归方法实现要查找的数,返回被查找的数的位置
 */
public static void  MyBinarySerrch(int[] array, int target, int low, int high) {
    int mid = (low + high)/2;
    if(target < array[low] || target > array[high] || array[low] > array[high] || array.length <= 0) {
        return -1;
    }
    
    if(target < array[mid]) {
        return MyBinarySearch(array, target, low, mid -1);
    } else if(target > array[mid]) {
        return MyBinarySearch(array, target, mid + 1, high);
    } else {
        return mid;
    }
}
```
