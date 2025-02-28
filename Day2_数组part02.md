# Day2

## KAMA 58
![image](https://github.com/user-attachments/assets/bc6a1868-b246-4bf2-853c-0ad6d5bb9fb2)
```java
import java.util.*; 

class Main{
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int len = sc.nextInt();
        int[] nums = new int[len];
        for(int i = 0; i<len; i++){
            nums[i] = sc.nextInt();
        }
        ArrayList<int[]> list = new ArrayList<>();
        while(sc.hasNextInt()){
            int[] arr = new int[2];
            arr[0] = sc.nextInt();
            arr[1] = sc.nextInt();
            list.add(arr);
        }
        int[] res = intervalSum(nums,list);
        for(int n : res){
            System.out.println(n);
        }
    }
    
    public static int[] intervalSum(int[] nums, ArrayList<int[]> intervals){
     int[] prefixSum = new int[nums.length + 1];
     int[] res = new int[intervals.size()];
     int sum = 0;
     prefixSum[0] = sum;
     for(int i = 1; i <= nums.length; i++){
        sum += nums[i-1];
        prefixSum[i] = sum;
     }
     for(int j = 0; j<intervals.size(); j++){
         int[] arr = intervals.get(j);
         int start = arr[0];
         int end = arr[1];
         res[j] = prefixSum[end + 1] - prefixSum[start];
     }
     return res;
    }
}
```

## 重点：

- scanner 的使用：nextInt()，hasNextInt()
- 前缀和数组的界限

## LC 209
![image](https://github.com/user-attachments/assets/b77b8169-55ad-4543-9b96-adeaeae6007f)

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        Queue<Integer> queue = new LinkedList<>();
        int sum = 0;
        int res = Integer.MAX_VALUE;
        for(int num : nums){
            sum += num;
            queue.add(num);
            while(sum >= target){
                if(sum >= target)res = res >= queue.size() ? queue.size() : res;
                sum -= queue.poll();
            }
        }
        return res == Integer.MAX_VALUE ? 0 : res;
    }
}
```

## 重点：

- 想到队列的使用，排序

## LC59

![image](https://github.com/user-attachments/assets/6a69a5c9-89c0-4bf9-bc74-0474ddaad78b)

```java
class Solution {
    private static final int[][] DIRS = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}}; 
    public int[][] generateMatrix(int n) {
        int[][] ans = new int[n][n];
        int i = 0;
        int j = 0;
        int di = 0;
        for(int val = 1; val <= n * n; val++){
            ans[i][j] = val;
            int x = i + DIRS[di][0];
            int y = j + DIRS[di][1];
            if(x < 0 || x>=n || y<0 || y>=n || ans[x][y] != 0){
                di = (di+1) % 4;
            }
            i += DIRS[di][0];
            j += DIRS[di][1];
        }  
        return ans;
    }
}
```

## 重点：

- 方向数组的理解，使用di 和方向数组结合来控制更新，{{0, 1}, {1, 0}, {0, -1}, {-1, 0}} 如果di 是1，
- i,j 的下一步是 i + DIR[di][0], j+DIR[di][1] 就算i+1,j不变，就算向下
