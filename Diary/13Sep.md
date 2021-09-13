---
title: Algorithm Analysis and Design (CS1.301)
subtitle: |
          | Monsoon 2021, IIIT Hyderabad
          | Daily Diary
          | 13 September, Monday
---

# CLRS Chapter 4: Divide-and-Conquer
## The Maximum-Subarray Problem
The brute-force solution is to check all $n \choose 2 = \Theta(n^2)$ pairs.  

Suppose we divide A[low..high] into two, A[low..mid] and A[mid..high]. Then, the maximum subarray can be entirely in either of these (which can be handled recursively) or crossing the middle.  
A subarray crossing the middle can be split into two, A[i..mid] and A[mid..j]. This is carried out in linear time by finding the greatest subarray of each of these forms.  

Therefore, we have
$$T(n) = \begin{split}
\Theta(1) & n = 1 \\
2T(\frac{n}{2}) + \Theta(n) & n > 1 \end{split}$$

This gives us $T(n) = \Theta(n \log n)$.
