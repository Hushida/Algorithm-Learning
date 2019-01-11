递归实现
```
/**
 * 
 * @Author Hushida
 * @date 2018.12.3
 * @description :递归方法实现要查找的数,返回被查找的数的位置
 */
public static int  MyBinarySerrch(int[] array, int target, int low, int high) {
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

非递归，循环实现
```
public static int  MyBinarySerrch(int[] array, int target) {
    if(array == null) {
        return -1;
    }
    int low = 0;
    int high = array.length - 1;
    
    while(low <= high) {
        int mid = low + (high - 1)/2;
        
        if(array[mid] == target) {
            return mid;
        }
        
        if(array[mid] < target) {
            low = mid +1
        }
        
        if(array[mid] > target) {
            high = mid -1;
        }
    }
    
   return -1;
}
```
