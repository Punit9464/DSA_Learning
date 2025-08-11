# Largest Element in an Array
#### Brute Force:
- Sort the given array
- last element of the array will be the largest element

#### Optimal:
- Set a variable ```maxi = INT_MIN```;
- Iterate the array, for i = 0 -> n-1:
    1. If `arr[i] > maxi`: update `maxi = arr[i]`; 

<br><br>

# Second Largest Element in the Array
#### Brute Force:
- In case of no duplicates, Sort the array -> Second last element is the second Largest.

#### Better:
- First find the Largest element in the array.
- Iterate through the given array again:
    1. update `secondLargest`, if `secondLargest < arr[i] && arr[i] < largest`

#### Optimal:
- Iterate through the array only once:
```cpp
int largest = -1, secondLargest = -1;

for(int i = 0; i < n; i++) {
    if(largest < arr[i]) {
        secondLargest = arr[i];
        largest = arr[i];
    } else if(arr[i] > secondLargest && arr[i] != largest) {
        secondLargest = arr[i];
    }
}

return secondLargest;
```
<br><br>

# Check if Array is sorted
#### Approach:
- Start Iteration from 1 to n-1:
-> check:
    ```cpp
    if(arr[i-1] > arr[i])
    ```
    if the current element is smaller than its previous, then array is not sorted.


# Check if Array is Rotated and Sorted
#### Brute Force:
- If the array is rotated, first reverse its rotation.
```cpp
    for i = 1 to n-1:
        if(arr[i-1] > arr[i]): // that means here the array is rotated
            reverse(arr);

    // Now the array must be in its original form
    // Now we can apply the "Check if Array is Sorted Approach".
```

#### Better:
- Just find the first index position where `(arr[i] < arr[i-1]);`. if no such index exists then arr is sorted, return true.
- Otherwise **remainder of the array from this position shall be in ascending order. Also last element should not be greater than first element -> as array is rotated.**. i.e, `arr[0] >= arr[n-1]`
```cpp
int idx = -1;
for(int i = 1; i < n; i++) {
    if(arr[i-1] > arr[i]) {
        idx = i;
        break;
    }
}
if(idx == -1) return true;

for(int i = idx+1; i < n; i++) {
    if(arr[i-1] > arr[i]) return false; // ahead elements must be in ascending order, if not return false
}
return true;
```

#### Optimal:
- If an array has been rotated, and its possible It can be sorted. => There must be only one index where `arr[i-1] > arr[i]`.
- Why so ? => because imagine a array `1 2 3 4 5`. 
    - Rotate it one times, it becomes -> `5 1 2 3 4`
    - Rotate it again, it becomes -> `4 5 1 2 3`
    - Rotate again, -> `3 4 5 1 2`
    and so on....
    <br>
- Therefore, doesn't matters how many times we rotate it, there is only one index where => `arr[i-1] > arr[i]`.
- Also if array is rotated this condition must also be satisfied, `arr[n-1] <= arr[0]`. eg, `3 4 5 1 2` -> `2 <= 3`.
- Hence, if condition `arr[i-1] > arr[i]` exists more than once anywhere, The array is not sorted.
```cpp
int cnt = 0;
for(int i = 1; i < n; i++) {
    if(arr[i-1] > arr[i]) cnt++;
}

if(arr[n-1] > arr[0]) cnt++;
return cnt <= 1;
```

<br><br>

# Remove Duplicates from the Array
#### Brute Force:
- Store the data of the array in a set, storing each element once.
- store them back to the array.

#### Optimal (Two Pointers):
- Initialize two pointers -> j = 0, i = 1;
- Iterate from i = 1 to i = n-1:
    - wherever, `arr[i] != arr[j]` stop, place `arr[j+1] = arr[i]` and increment j;
    - atlast return `j+1` => number of unique elements in the array.

### Intuition:
Why does this works?
- We are making to pointers -> front(i), back(j).
- back (j) points to the unique elements only and back keeps on iterating whole array.
- Whenever we find any elements which are unique that is -> `arr[i] != arr[j]`, we are making lie `arr[i]` just at `arr[j+1]`, as `j` is pointing to unique element already, so wish to bring the next unique element at `j+1`th position.
- Then we increment `j`, as `j` must keep pointing to unique elements
- Atlast we return `j+1` as number of elements = `index + ` (0 -based indexing).
- code:
```cpp
int i = 1, j = 0;

for(; i < n; i++) {
    if(arr[i] != arr[j]) {
        arr[j+1] = arr[i];
        j++;
    }
}

return j+1;
```

