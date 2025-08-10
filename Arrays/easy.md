# Largest Element in an Array
#### Brute Force:
- Sort the given array
- last element of the array will be the largest element

#### Optimal:
- Set a variable ```maxi = INT_MIN```;
- Iterate the array, for i = 0 -> n-1:
    1. If `arr[i] > maxi`: update `maxi = arr[i]`; 

