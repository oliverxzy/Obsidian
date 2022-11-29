```toc style: bullet | number | inline (default: bullet) min_depth: number (default: 2) max_depth: number (default: 6) title: string (default: undefined) allow_inconsistent_headings: boolean (default: false) delimiter: string (default: |) varied_style: boolean (default: false) 
```

### Two Pointers Notes
In problems where we deal with **sorted arrays** (or **LinkedLists**) and need to find a set of elements that fulfill certain constraints, the Two Pointers approach becomes quite useful.

>Given an array of sorted numbers and a target sum, find a pair in the array whose sum is equal to the given target.

At every step, we will see if the numbers pointed by the two pointers add up to the target sum. If they do not, we will do one of two things:
1. if sum of two pointer > target_sum, then - end_pointer
2. if sum of two pointer < target_sum, then + start_pointer

### Pair with Target Sum (easy)
Given an array of sorted numbers and a target sum, find a **pair in the array whose sum is equal to the given target**.
Write a function to return the indices of the two numbers (i.e. the pair) such that they add up to the given target.
```
Input: [1, 2, 3, 4, 6], target=6
Output: [1, 3]
Explanation: The numbers at index 1 and 3 add up to 6: 2+4=6
```

**Solving Idea**
- assign two pointers, start, end = 0, len(arr) - 1
- while left < right:
	- if left + right > target, then end -= 1
	-  if left + right < target, then start += 1
- return left, right

**Solution**
```python
def pair_with_targetsum(arr, target_sum):
  left, right = 0, len(arr) - 1
  while left < right:
    if arr[left] + arr[right] == target_sum:
      return [left, right]
    if arr[left] + arr[right] > target_sum:
      right -= 1
    else:
      left += 1
  # TODO: Write your code here
  return [left, right]
```

### Remove Duplicates (easy)
Given an array of sorted numbers, remove all duplicate number instances from it in-place, such that each element appears only once. The relative order of the elements should be kept the same and you should **not use any extra space** so that that the solution have a space complexity of O(1).
Move all the unique elements at the beginning of the array and after moving return the length of the subarray that has no duplicate in it.
```
Input: [2, 3, 3, 3, 6, 9, 9]
Output: 4
Explanation: The first four elements after removing the duplicates will be [2, 3, 6, 9].
```

**Solving Idea**
Since this question is about sorted array. We will maintain two pointers:
- i is the slow pointer, when arr_i != arr_j, then move to next, and replace by arr_j
- J is fast pointer, it will iterate every time. end when j >= len(arr)

**Solution**
```python
def remove_duplicates(arr):
  i = 0
  for j in range(len(arr)):
    if arr[i] != arr[j]:
      i += 1
      arr[i] = arr[j]
  
  return i+1
```

### Squaring a Sorted Array (easy)
Given a sorted array, create a new array containing **squares of all the numbers of the input array** in the sorted order.
**Example 1:**
```
Input: [-2, -1, 0, 2, 3]Output: [0, 1, 4, 4, 9]
```

**Solving Idea**
We will assign two pointer: left, right
- left right
- empty list that same size as original one 
- max_index that will iterate from end to begain to put number from max to min

**Solution**
```python
def make_squares(arr):
  squares = []
  n = len(arr)
  highest = n - 1
  squares = [0 for x in range(n)]
  left, right = 0,len(arr)-1
  while left <= right:
    sq_left = arr[left] * arr[left]
    sq_right = arr[right] * arr[right]
    if sq_left > sq_right:
      squares[highest] = sq_left
      left += 1
    else:
      squares[highest] = sq_right
      right -= 1
    highest -= 1
  return squares

  # TODO: Write your code here
  return squares
```

### Triplet Sum to Zero (medium)
Given an array of unsorted numbers, find all **unique triplets in it that add up to zero**.
**Example 1:**
```
Input: [-3, 0, 1, 2, -1, 1, -2]
Output: [-3, 1, 2], [-2, 0, 2], [-2, 1, 1], [-1, 0, 1]
Explanation: There are four unique triplets whose sum is equal to zero.
```

**Solving Idea**
We will need a main function and sum function that calculate two sum
- main function:
	- sort array
	- iterate through array:
		- if current value > 0, break
		- if current value same as before, skip
		- call Two_sum function
- Two sum function:
	- left, right = low_bar + 1, len(arr) - 1
	- if nums_left + nums_right + nums_low_bar < 0:
		- left += 1
	- elif nums_left + nums_right + nums_low_bar > 0:
		- right -= 1
	- else:
		- result.append()
		- low_bar += 1
		- high -= 1
		- low_bar+=1 if nums_lo == nums_lo-1 and lo< high

**Solution**
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        result = []
        nums.sort()
        for i in range(len(nums)):
            if nums[i] > 0:
                break
            if i==0 or nums[i-1] != nums[i]:
                self.twoSum(nums,i,result)
        return result
    
    def twoSum(self,nums,i,result):
        lo, hi = i + 1, len(nums) - 1
        while lo < hi:
            sums = nums[i] + nums[lo] + nums[hi]
            if sums < 0:
                lo += 1
            elif sums > 0:
                hi -= 1
            else:
                result.append([nums[i], nums[lo], nums[hi]])
                lo += 1
                hi -= 1
                while lo < hi and nums[lo] == nums[lo - 1]:
                    lo += 1
```

### Triplet Sum Close to Target (medium)

^547c1b

Given an array of unsorted numbers and a target number, find a **triplet in the array whose sum is as close to the target number as possible**, return the sum of the triplet. If there are more than one such triplet, return the sum of the triplet with the smallest sum.

**Example 1:**

```
Input: [-2, 0, 1, 2], target=2
Output: 1
Explanation: The triplet [-2, 1, 2] has the closest sum to the target.
```

**Solving Idea**
Define a diff to represent absolute(3_sum - target), check min(diff,absolute(3_sum - target))
1. sort the array
2. loop with i:
	1. left, right = i+1, len(arr) - 1
	2. if absolute(3_sum - target) < diff:
		1. diff = target - 3_sum
	2. if  3_sum < target:
		1. left += 1
	2. if 3_sum > target:
		1. right -= 1
	2. else:
		1. break
2. return 3_sum - target
