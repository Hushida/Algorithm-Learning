# 跳跃问题1
给定数组arr,arr[i]代表可以从位置i向右跳1~k个距离，比如，arr[1] = 3,表示可以从位置1跳到位置2，位置3，位置4.如果从位置0出发，最少跳几次能
到达arr最后的位置？  
**思路** 用jump表示当前跳了多少次，cur表示如果只能跳jump次能达到的最远位置，也就是当前能到达的最远位置，
next表示再多跳一步能到达的最远的位置，即为下一次能到达的最远位置。  
```
public int jump(int[] arr) {
  if(arr == null || arr.length <= 0) {
    return 0;
  }
  int jump = 0;
  int cur = 0;
  int next = 0;
  for(int i=0; i < arr.length; i++) {
    if(cur < i) {
      jump++;
      cur = next; //更新jump的同时一定要同时更新cur的值
    }
    next = Math.max(next, i + arr[i]);
  }
  return jump;
}
```
