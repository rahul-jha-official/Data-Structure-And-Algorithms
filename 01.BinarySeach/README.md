# Binary Search Problems
## Coding Problems
- [Search Insert Position](#search-insert-position)
- [Search in Rotated Sorted Array](#search-in-rotated-sorted-array)

## [Search Insert Position](search-insert-position)
<a href="https://leetcode.com/problems/search-insert-position/description/">Problem Statement</a>
```cs
public class Solution 
{
    public int SearchInsert(int[] nums, int target) 
    {
        int start = 0, end = nums.Length - 1;
        while (start < end)
        {
            int mid = (end - start)  / 2 + start;
            if (nums[mid] < target)
            {
                start = start + 1;
            }
            else if (nums[mid] > target)
            {
                end = end - 1;
            }
            else
            {
                break;
            }
        }

        for (int i = start; i < end + 1 && i < nums.Length; i++)
        {
            if (nums[i] >= target) return i;
        }

        return nums.Length;
    }
}
```

## [Search in Rotated Sorted Array](#search-in-rotated-sorted-array)
<a href="https://leetcode.com/problems/search-in-rotated-sorted-array/description/">Problem Statement</a>

```cs
public class Solution {
    public int Search(int[] nums, int target)
    {
        int low = 0, high = nums.Length - 1;
        while (low <= high)
        {
            int mid = (low + high) / 2;
            if (nums[mid] == target) return mid;
            if (nums[low] <= nums[mid])
            {
                if (target >= nums[low] && target <= nums[mid]) high = mid - 1;
                else low = mid + 1;
            }
            else
            {
                if (target >= nums[mid] && target <= nums[high]) low = mid + 1;
                else high = mid - 1;
            }
        }
        return -1;
    }
}
```
