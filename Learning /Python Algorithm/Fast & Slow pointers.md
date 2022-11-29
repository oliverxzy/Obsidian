```toc style: bullet | number | inline (default: bullet) min_depth: number (default: 2) max_depth: number (default: 6) title: string (default: undefined) allow_inconsistent_headings: boolean (default: false) delimiter: string (default: |) varied_style: boolean (default: false) 
```

The **Fast & Slow** pointer approach, is a pointer algorithm that uses two pointers which move through the array (or sequence/LinkedList) at different speeds. This approach is quite useful when dealing with cyclic LinkedLists or arrays.
By moving at different speeds (say, in a cyclic LinkedList), the algorithm proves that the two pointers are bound to meet. The fast pointer should catch the slow pointer once both the pointers are in a cyclic loop. ^a3e393

### LinkedList Cycle (easy) - 141. Linked List Cycle

^f542ce

Given the head of a **Singly LinkedList**, write a function to determine if the LinkedList has a **cycle** in it or not.

**Solving Idea**
assign fast & slow pointers that:
fast move 2, slow move 1
1. If linkedlist dont have cycle, fast pointer will reach the end before slow pointer
2. If linkedlist have cycle, fast will meet with slow 

**Solution**
```python
def has_cycle(head):
  slow, fast = head, head
  while fast is not None and fast.next is not None:
    fast = fast.next.next
    slow = slow.next
    if slow == fast:
      return True  # found the cycle
  return False

```

### Start of LinkedList Cycle (medium) - 142. Linked List Cycle II

^f77b40

Given the head of a **Singly LinkedList** that contains a cycle, write a function to find the **starting node of the cycle**.

**Solving Idea**
1. set slow = slow.next, fast = fast.next.next. Find two pointer's meeting point
2. move one of them to head, slow = slow.next, fast = fast.next
	1. when they meet, the point is start of cycle

**Solution**
```python
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow, fast = head, head
        while fast is not None and fast.next is not None:
            fast = fast.next.next
            slow = slow.next
            
            if fast == slow:
                break
        
        if fast is None or fast.next is None:
            return None
        
        slow = head
        
        while slow != fast:
            fast = fast.next
            slow = slow.next
            
        return slow

```

### Happy Number (medium) - 202. Happy Number

^6d82ac

Write an algorithm to determine if a number `n` is happy.
A **happy number** is a number defined by the following process:
-   Starting with any positive integer, replace the number by the sum of the squares of its digits.
-   Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
-   Those numbers for which this process **ends in 1** are happy.
Return `true` _if_ `n` _is a happy number, and_ `false` _if not_.

**Solving Idea**
1. Define a function to calculate current square sum
2. use slow, fast pointers:
	1. slow = slow.next, fast = fast.next.next
	2. if slow == fast: no happy number

**Solution**
```python
def find_happy_number(num):
  slow, fast = num, num
  while True:
    slow = find_square_sum(slow)  # move one step
    fast = find_square_sum(find_square_sum(fast))  # move two steps
    if slow == fast:  # found the cycle
      break
  return slow == 1  # see if the cycle is stuck on the number '1'


def find_square_sum(num):
  _sum = 0
  while (num > 0):
    digit = num % 10
    _sum += digit * digit
    num //= 10
  return _sum

```

### Middle of the LinkedList (easy)
Given the head of a **Singly LinkedList**, write a method to return the **middle node** of the LinkedList.
If the total number of nodes in the LinkedList is even, return the second middle node.
**Example 1:**
```
Input: 1 -> 2 -> 3 -> 4 -> 5 -> nullOutput: 3
```

**Solving Idea**
use slow and fast pointer:
- slow = slow.next
- fast = fast.next.next
when fast reach end, slow is the middle of the linkedlist

**Solution**
```python
def find_middle_of_linked_list(head):
  slow = head
  fast = head
  while (fast is not None and fast.next is not None):
    slow = slow.next
    fast = fast.next.next
  return slow

```

### Problem Challenger 1 - Palindrome LinkedList (medium)
Given the head of a **Singly LinkedList**, write a method to check if the **LinkedList is a palindrome** or not.
Your algorithm should use **constant space** and the input LinkedList should be in the original form once the algorithm is finished. The algorithm should have O(N)O(N) time complexity where ‘N’ is the number of nodes in the LinkedList.
**Example 1:**
```
Input: 2 -> 4 -> 6 -> 4 -> 2 -> null
Output: true
```

**Solving Idea**
we use fast and slow, to find middle of linkedlist. then reverse second half, and compare with first half.
1. we define a reverse function that reverse second half
2. main function:
	1. slow and fast pointers to find middle point
	2. apply reverse function to reverse second half
	3. compare first and second:
		1. if first.current != second.current -> break
		2. first and second move to next
		3. return True
	4. return False

**Solution**
```python
def is_palindromic_linked_list(head):
  if head is None or head.next is None:
    return True

  # find middle of the LinkedList
  slow, fast = head, head
  while (fast is not None and fast.next is not None):
    slow = slow.next
    fast = fast.next.next

  head_second_half = reverse(slow)  # reverse the second half
  # store the head of reversed part to revert back later
  copy_head_second_half = head_second_half

  # compare the first and the second half
  while (head is not None and head_second_half is not None):
    if head.value != head_second_half.value:
      break  # not a palindrome

    head = head.next
    head_second_half = head_second_half.next

  reverse(copy_head_second_half)  # revert the reverse of the second half

  if head is None or head_second_half is None:  # if both halves match
    return True

  return False


def reverse(head):
  prev = None
  while (head is not None):
    next = head.next
    head.next = prev
    prev = head
    head = next
  return prev

```

>Review Reverse function definition #NeedReview