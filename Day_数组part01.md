## LC 704 二分查找

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while(left<=right){
            int mid = left + (right - left)/2;
            if(nums[mid] == target){
                return mid;
            }
            else if(nums[mid] > target){
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }
        return -1;
    }
}
```

**重点：** 

- 求mid时，防止过界
- 注意区间定义，
    - 这里使用左闭右闭区间也就是left 可以等于right，此时mid 也是left 和right
    - 注意while的定义，left≤right
    - 更新边界时，因为检查过mid，所以边界是mid+-1

## LC 977
![image](https://github.com/user-attachments/assets/ee184ece-77e6-42e8-b958-115eb6b8bb2d)

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int i = 0; 
        int j = nums.length - 1;
        int index = nums.length - 1;
        int[] ans = new int[nums.length];
        while(i<=j){
            if(-nums[i] > nums[j]){
                ans[index] = nums[i] * nums[i];
                i++;
            }else{
                ans[index] = nums[j] * nums[j];
                j--;
            }
            index--;
        }
        return ans;
    }
}
```

重点：

- 首先因为不知道数组的正负范围，可以考虑到两种，一种是中心到两边，但是不好控制边界更新
- 采用从头尾的值检查，并且从最大值开始填充，并且比较 −*nums*[*i*] 和 *nums*[*j*] 的大小

# LC27
![image](https://github.com/user-attachments/assets/41cb3776-179a-4db5-a7e4-661cd4707a7b)

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        // fast find next val for new arr, slow shows the index 
        int slow = 0; 
        for(int fast = 0; fast<nums.length; fast++){
            if(nums[fast] != val){
                nums[slow] = nums[fast];
                slow++;
            }
        }
        return slow;
    }
}
```

双指针:

定义：快指针寻找下一个新数组的值，慢指针维护新数组的坐标，当快指针不是要移除元素时，填充到index，并且移动慢指针的坐标。
