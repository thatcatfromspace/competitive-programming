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

# Approach

1. Initialize variables `i` and `j` as indices pointing to the least significant digits of `a` and `b` respectively, and `carry` as 0.
2. Initialize an empty string `res` to store the result.
3. Iterate through the strings `a` and `b` from right to left:
    - Add the current digits of `a` and `b` along with the carry.
    - Update carry as necessary.
    - Append the sum modulo 2 to the result string.
4. If there is a carry after iterating through both strings, append it to the result string.
5. Reverse the result string to get the correct binary representation of the sum.
6. Return the result string.

## Length of last word - [LeetCode](https://leetcode.com/problems/length-of-last-word/)

initial thoughts:

- must keep track of penultimate and last space 

Simplest approach with Python:

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

Find sum of all elements, then start comparing left sum and right sum from the end.

Solution [here](https://leetcode.com/problems/find-pivot-index/solutions/5173369/easy-c-solution/?envType=study-plan-v2&envId=leetcode-75)


## First occurrence of a string - [LeetCode](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string)

Thought about implementing a two pointer approach, but got stuck with non-existent cases and repeated letters.

Instead, **go with finding substrings sequentially**. from `i = 0 to biggerWord.size()`.


## Majority element - [LeetCode](https://leetcode.com/problems/majority-element)


easy. sort the array, the middle element should be your answer.

alternatively, reduce time complexity to `O(n)` by using a hashmap.

