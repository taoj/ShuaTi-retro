# Binary search 的几种总结

* 在 rotated sorted array 中找到最小值（即 pivotal）
```Java
int left = 0;
int right = array.length-1;

while(left < right){
 int mid = left +(right-left)/2;
 
 if(array[mid]>array[right]){
   left = mid+1;
 }else{
   right = mid;
 }
}

//left is where minimal presents.
```

* Leetcode 33. Search in Rotated Sorted Array
  * No duplicates 
```Java
class Solution {
    public int search(int[] nums, int target) {
        if(nums.length == 0){
            return -1;
        }
        
        int left = 0;
        int right = nums.length-1;
        
        while(left <= right){
            int mid = left + (right-left)/2;

            if(nums[mid] == target){
                return mid;
            }

            if(nums[mid] >= nums[left]){
                if(target >= nums[left] && target < nums[mid]){
                    right = mid-1;
                }else{
                    left = mid+1;
                }
            }else{
                if(target > nums[mid] && target <= nums[right]){
                    left = mid+1;
                }else{
                    right = mid-1;
                }
            }
        }
        return -1;
    }
}
```
* Leetcode 81. Search in Rotated Sorted Array II
  * Contains duplicates
```Java
class Solution {
    public boolean search(int[] nums, int target) {
        
        if(nums == null || nums.length == 0){
            return false;
        }
        
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            
            int mid = (left + right) / 2;
            if (target == nums[mid]) 
                return true;
            if (nums[mid] == nums[left]) 
                left++;
            else if (nums[mid] > nums[left]) {
                if (target >= nums[left] && target < nums[mid]) 
                    right = mid - 1;
                else 
                    left = mid + 1;
            } else {
                if (target > nums[mid] && target <= nums[right]) 
                    left = mid + 1;
                else 
                    right = mid - 1;
            }
        }
        return false;
    }
}
```
