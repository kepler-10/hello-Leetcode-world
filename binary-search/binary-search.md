## 475. heaters

### 方法一：

时间复杂度为O(mn)，空间复杂度O(1)

```java
public int findRadius(int[] houses, int[] heaters) {
    Arrays.sort(houses);
    Arrays.sort(heaters);
    int maxDist = -1;
    for (int house:houses){
        int minDist = Integer.MAX_VALUE;
        for (int heater : heaters) {
            int distance = Math.abs(heater-house);
            minDist = Math.min(minDist,distance);
        }
        maxDist = Math.max(maxDist,minDist);
    }
    return maxDist;
}
```

### 方法二：

二分法求每间房屋最近的heater

```java
public int findRadius(int[] houses, int[] heaters) {
    Arrays.sort(houses);
    Arrays.sort(heaters);
    int n= heaters.length;
    int maxDist = -1;
    for (int house:houses){
        int left = 0, right = n;
        while (left < right){
            int mid = left+(right-left)/2;
            if (heaters[mid] < house){
                left = mid+1;
            }else
                right = mid;
        }
        int dist1 = (right==0)?Integer.MAX_VALUE:Math.abs(house-heaters[right-1]);
        int dist2 = (right==n)?Integer.MAX_VALUE:Math.abs(house-heaters[right]);
        maxDist = Math.max(maxDist,Math.min(dist1,dist2));
    }
    return maxDist;
}
```

