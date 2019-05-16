思路： 
代码（java）
```
public static void quickSort(int[] a, int start, int end) {
    if(a == null || start >= end) {
        return;
    }
    int pivotIndex = partition(a, start, end);
    quickSort(a, start, partition - 1);
    quickSort(a, partition + 1, end);
}
public static int partition(int[] a, int start, int end) {
    int pivotIndex = end;
    while(start < end) {
        if(start < end && a[start] < a[pivotIndex]) {
            start++;
        }
        if(start < end) {
            int temp 
        }
    }
    pivotIndex = end;
    return pivotIndex;
}
```
