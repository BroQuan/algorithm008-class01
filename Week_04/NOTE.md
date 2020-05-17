## 学习笔记
&emsp;&emsp;平时解题思路都在各个题目当中，本周学习笔记篇就讨论讨论覃超在二分查找实战篇视频尾部提出的一个问题吧。
### 问题描述
&emsp;&emsp;使用二分查找，寻找一个半有序数组中间无序的下标。
### 示例
```
输入：4,5,6,7,0,1,2

输出：4
```
### 思路
二分查找
&emsp;&emsp;分三种情况：
&emsp;&emsp;1. nums[left] < nums[mid] 且 nums[mid] > nums[r]，说明 left 与 right 范围内数据无序，且拐点在 mid 右部，故 left = mid + 1；  
&emsp;&emsp;2. nums[left] > nums[mid] 且 nums[mid] < nums[r],说明 left 与 right 范围内数据无序，且拐点在 mid 左部，故 right = mid - 1；  
&emsp;&emsp;2. nums[left] < nums[mid] 且 nums[mid] < nums[r],说明 left 与 right 范围内数据有序，直接返回left下标即可。



### 参考代码
#### java
``` java
class Solution {
    private int search(int nums[]) {
        int l = 0, r = nums.length - 1, mid = 0;
        while (l <= r) {
            mid = l + (r - l) / 2;
            if (nums[mid] > nums[l] && nums[mid] > nums[r]) {
                l = mid + 1;
            } else if (nums[mid] < nums[l] && nums[mid] < nums[r]) {
                r = mid - 1;
            } else {
                return l;
            }
        }
        return -1;
    }
    public static void main(String[] args) {
        int []input = {4,5,6,7,0,1,2,3};
        Solution s = new Solution();
        System.out.println(s.search(input));
    }
}
/*
4,5,6,7,0,1,2,3
 */

/*
6,7,0,1,2,3,4,5
 */

```