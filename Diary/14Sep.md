---
title: Algorithm Analysis and Design (CS1.301)
subtitle: |
          | Monsoon 2021, IIIT Hyderabad
          | Daily Diary
          | 14 September, Tuesday
---

# CLRS Chapter 9: Medians and Order Statistics
## Minimum and Maximum
Clearly, the minimum or maximum can be found with $n-1$ comparisons. Further, both can be found simultaneously with $3 \left\lfloor \frac{n}{2} \right\rfloor$ (by processing elements in pairs).

## Selection in Expected Linear Time
The following procedure (modelled on quicksort) has an expected linear running time. It returns the $i^\text{th}$ smallest element in A[p..r].
```
Randomised-Select(A,p,r,i)
if p == r
    return A[p]
q = Randomised-Partition(A,p,r) //A[p..q-1] ≤ A[q] ≤ A[q+1..r]
k = q - p + 1
if i == k
    return A[q]
elseif i < k
    return Randomised-Select(A,p,q-1,i)
else
    return Randomised-Select(A,q+1,r,i-k)
```

Although this algorithm has a worst-case quadratic running time, the randomisation makes the expected time linear.
