### Introduction
This pattern describes an efficient technique to deal with overlapping intervals. In a lot of problems involving intervals, we either need to find overlapping intervals or merge intervals if they overlap.
Given two intervals (‘a’ and ‘b’), there will be six different ways the two intervals can relate to each other:
![[Screen Shot 2022-11-13 at 11.55.50 AM.png]] ^ew91p1

### Merge Intervals (medium)
Given a list of intervals, **merge all the overlapping intervals** to produce a list that has only mutually exclusive intervals.
**Example 1:**
```
Intervals: [[1,4], [2,5], [7,9]]
Output: [[1,5], [7,9]]
Explanation: Since the first two intervals [1,4] and [2,5] overlap, we merged them into one [1,5].
```

**Solving Idea**
Based on [[Merge Intervals#^ew91p1]] cases, when overlapping, we will have case 2, 3, 4.
![[Screen Shot 2022-11-13 at 12.11.36 PM.png]]
1. then sort array by start, to make sure a.start <= b.start
2. when b.start <= a.end, then overlapp
	- c.start = a.start, c.end = max(a.end, b.end)

**Solution**
```python
def merge(intervals):
  if len(intervals) < 2:
    return intervals

  # sort the intervals on the start time
  intervals.sort(key=lambda x: x.start)

  mergedIntervals = []
  start = intervals[0].start
  end = intervals[0].end
  for i in range(1, len(intervals)):
    interval = intervals[i]
    if interval.start <= end:  # overlapping intervals, adjust the 'end'
      end = max(interval.end, end)
    else:  # non-overlapping interval, add the previous internval and reset
      mergedIntervals.append(Interval(start, end))
      start = interval.start
      end = interval.end

  # add the last interval
  mergedIntervals.append(Interval(start, end))
  return mergedIntervals
```

