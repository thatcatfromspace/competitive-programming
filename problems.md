first few problems are random, then questions are covered topicwise from [striver's dsa course](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2), starting from [here](https://github.com/thatcatfromspace/competitive-programming/blob/main/problems.md#majority-element---leetcode).

## Binary addition - [LeetCode](https://leetcode.com/problems/add-binary)

```cpp
class Solution {
public:
    string addBinary(string a, string b) {
      int i = a.size() - 1;
        int j = b.size() - 1;
        int carry = 0;
        string res = "";
        while (i >= 0 || j >= 0) {
            int sum = carry;

            if (i >= 0) {
                sum += a[i] - '0';
                i--;
            }
            if (j >= 0) {
                sum += b[j] - '0';
                j--;
            }

            carry = sum > 1 ? 1 : 0;
            res += to_string(sum % 2);
        }
        if (carry) 
            res += to_string(carry);
        reverse(res.begin(), res.end());
        return res;
    }
};
```

Explanation [here](https://aaronice.gitbook.io/lintcode/string/add-binary)

1. initialize variables `i` and `j` as indices pointing to the least significant digits of `a` and `b` respectively, and `carry` as 0.
2. initialize an empty string `res` to store the result.
3. iterate through the strings `a` and `b` from right to left:
    - add the current digits of `a` and `b` along with the carry.
    - update carry as necessary.
    - append the sum modulo 2 to the result string.
4. if there is a carry after iterating through both strings, append it to the result string.
5. reverse the result string to get the correct binary representation of the sum.
6. return the result string.

## Length of last word - [LeetCode](https://leetcode.com/problems/length-of-last-word/)

initial thoughts:

- must keep track of penultimate and last space 

simplest approach with Python:

```python
def last_word(word):
	return len(word.strip().split(' ')[-1])
```


## Climbing stairs - [LeetCode](https://leetcode.com/problems/climbing-stairs)

initial thoughts:

- classic DP problem, requires memoization of some kind.
- turns out to be basic Fibonacci series 

Detailed explanation [here](https://leetcode.com/problems/climbing-stairs/solutions/3708750/4-method-s-beat-s-100-c-java-python-beginner-friendly/)

## Highest altitude - [LeetCode](https://leetcode.com/problems/find-the-highest-altitude)

apply the concept of [prefix sum](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) to find the maximum altitude.

tip: `*max_element(vector.begin(), vector.end());` returns the maximum number in a vector - returns an iterator hence the pointer.

tip 2: if it is not explicitly stated that you cannot modify the given array/vector, play around with it to save memory usage.


## Pivot index - [LeetCode](https://leetcode.com/problems/find-pivot-index)

find sum of all elements, then start comparing left sum and right sum from the end.

solution [here](https://leetcode.com/problems/find-pivot-index/solutions/5173369/easy-c-solution/?envType=study-plan-v2&envId=leetcode-75)


## First occurrence of a string - [LeetCode](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string)

Thought about implementing a two pointer approach, but got stuck with non-existent cases and repeated letters.

Instead, **go with finding substrings sequentially**. from `i = 0 to biggerWord.size()`.


## Majority element - [LeetCode](https://leetcode.com/problems/majority-element)

easy. sort the array, the middle element should be your answer.

alternatively, reduce time complexity to `O(n)` by using a hashmap.

## Sort colors - [LeetCode](https://leetcode.com/problems/sort-colors)

did not know how to proceed. tried to naively sort the array in place resulting in around `O(n)` complexity.

instead, use a hashmap to map the number of 0s, 1s and 2s, clear the array, and then push them back in the right order with the count from the hashmap.

## Lucky numbers in matrix - [LeetCode](https://leetcode.com/problems/lucky-numbers-in-a-matrix)

find min element in row, push it to an array, find max element in row, push it to another array. 
from both arrays, match elements from both arrays in the original matrix to find lucky numbers.

## Remove duplicate from sorted array - [LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

two pointer approach. maintain a pointer `i` from the beginning and a right pointer `ptr = 1`, move ptr when `nums[i] != nums[ptr-1]`, and return `ptr` as we need to return the number of unique elements in the array, which is just equal to `ptr`.

## Rotate array - [LeetCode](https://leetcode.com/problems/rotate-array/)

naive approach is to mod the index of every element plus `k` and place them into a new array, i.e., `newArray[(i+k) % size] = nums[i]`, and the copy them back into `nums` so it gives **the illusion** of it being an in-place algorithm.

better approach is applying reverse operation 3 times, first on the entire array, then from the beginning to the`k`th element, and then from the `k`th element to the end.

## Find missing element in range - [LeetCode](https://leetcode.com/problems/missing-number/)

lakshman is brilliant. find the sum of numbers from range `[0, nums.size()]` and then subtract it from actual sum of the given array (psst, `std::accumulate()`) and the difference is the missing numbers. absolutely genius.

## Maximum consecutive ones - [LeetCode](https://leetcode.com/problems/max-consecutive-ones/)

my approach was a bit convoluted. set `lastZero = -1` and then start looking for zeroes in the array. on the first encounter, set `highest = i` (index of the first 0) and `lastZero` to the same as well. compare subsequent differences and if the last element is 1, make sure to check if the highest condition still satisfies. 

note: edge case optimization (`nums.size() <= 1`) helped me get slightly better time.

## Single number - [LeetCode](https://leetcode.com/problems/single-number/)

XOR! xor all elements in the array with `ans = 0`, the resulting `ans` is the missing number. 🤯

note: bitwise operations always yield an INTEGER, not a BOOLEAN.
