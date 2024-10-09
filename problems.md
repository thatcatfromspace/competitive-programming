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

edit: **better approach**

maintain two variables `currSum` and `prevSum` both set to 0 initially. whenever a `1` is encountered, increment `currSum`, otherwise, set `prevSum` to `max(currentSum, prevSum)` and return the maximum of both.

## Single number - [LeetCode](https://leetcode.com/problems/single-number/)

XOR! xor all elements in the array with `ans = 0`, the resulting `ans` is the missing number. 🤯

note: bitwise operations always yield an INTEGER, not a BOOLEAN.

## Maximum subarray aka Kadane's algorithm - [LeetCode](https://leetcode.com/problems/maximum-subarray/)

Use two variables `max_ending_here = INT_MIN` and `max_so_far = 0`, in a `for` loop on all the elements in the given array, increment `max_ending_here` by the current element, and then compare `max_ending_here` and `max_so_far`, if the former is larger, set `max_so_far` to `max_ending_here`, then, if `max_ending_here < 0`, set it to 0. return `max_starting_here`.

associated g4g article [here](https://geeksforgeeks.org/largest-sum-contiguous-subarray/).

## Best time to buy and sell stock - [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

classic sliding window problem, can also be related to Kadane's algo (how?). create two variables `lowest = prices[0]` and `ans = INT_MIN`, iterate over each element `price` to see if the next price is smaller and then set `ans` to `max(ans, price - lowest)`.

## Sort the people - [LeetCode](https://leetcode.com/problems/sort-the-people)

one of the most easiest, most straightforward questions i've seen. throw the heights mapped to the names into an `unordered_map` and then sort, reverse and throw the names back into another new array in the sorted order and return the array.

## Rotate list - [LeetCode](https://leetcode.com/problems/rotate-list/)

same as rotate array but with a linked list. the mod approach did not work (too many edge case violations), instead manually cut off the list at `count - k -1` and reattach this to the beginning of the linked list. 

very intuitive solution (by me) [here](https://leetcode.com/problems/rotate-list/submissions/1330229947/)

## Reverse linked list - [LeetCode](https://leetcode.com/problems/reverse-linked-list)

use a stack to store the elements and then store it in the linked list backwards.

## Search insert position - [LeetCode](https://leetcode.com/problems/search-insert-position)

binary search your way to find the given element in the array, and then return low (this is equivalent to finding floor) for it to be the position where the number should be inserted.

## Two sum - [LeetCode](https://leetcode.com/problems/two-sum)

simplest one pass algorithm is to create a hashmap of the numbers in their array and their index. as the `for` loop iterates, return the number and its complement if it exists or store the number in the array. 

## Reverse words in a string - [LeetCode](https://leetcode.com/problems/reverse-words-in-a-string)

shamelessly use python. genius one liner crafted by me.

```py
 def reverseWords(self, s: str) -> str:
        return ' '.join(s.strip().split()[::-1])
```

## Check if LL is a palindrome - [LeetCode](https://leetcode.com/problems/palindrome-linked-list)

add the elements of the LL to an array `arr`, compare if `arr[i]` equals `arr[size-i-1]` for `i = 0 to size/2`.  

## Valid anagram - [LeetCode](https://leetcode.com/problems/valid-anagram)

approach 1: `O(n*logn)` - separate the array into characters, push it into 2 arrays, sort the arrays and compare
approach 2: `O(n)` - add the elements of first string to a hashmap, and compare the hash values of second string to first; if `hashmap[letter] == 0`, then return false. [solution](https://leetcode.com/problems/valid-anagram/submissions/1340520551/)


## Rotate string - [LeetCode](https://leetcode.com/problems/rotate-string)

iterate through the string adding the first letter of the string to the end each time, and compare the resultant **substring** to `goal`.

## Add two numbers - [LeetCode](https://leetcode.com/problems/add-two-numbers/)

straightforward approach, for every element, `sum = (l1->val + l2->val + carry) % 10` and `carry = ((l1->val + l2->val + carry) / 10`. be sure to add extra carry to the end after you're done adding.

## Minimum pushes II - [LeetCode](https://leetcode.com/problems/minimum-number-of-pushes-to-type-word-ii/)

for the longest time i kept thinking that the letter corresponding to the count matters. it doesn't.
add the count of each letter to an array, sort the array, and then itertate over each element of the array.

```cpp
totalPresses += (i / 8 + 1) * count[i]
```

## Kth distinct string in array - [LeetCode](https://leetcode.com/problems/kth-distinct-string-in-an-array/)

map every string to an array. if mapped value of string equals 1, it is distinct. then iterate over every string in the array, and for every unique encountered, reduce `k` by 1. if `k == 0`, return that string.

quite elegant submission [here](https://leetcode.com/problems/kth-distinct-string-in-an-array/submissions/1348559365).

## Minimum bit flips required - [LeetCode]()

XOR the given numbers to find the number of differing digits. then increment count everytime a `1` is encountered (by `num & 1`) and right shift the pointer num.

## Linked list cycle - [LeetCode](https://leetcode.com/problems/linked-list-cycle)

classic tortoise and hare pointer problem. while `fast && fast->next`, iterate until both pointers are equal, return true if yes, else there is no cycle in the list.

## Largest odd number in string - [LeetCode](https://leetcode.com/problems/largest-odd-number-in-string)

the point is to start counting from the **end**, not the start. if the current digit is even, change the return string to a substring of the original string from `0` to `i+1`.

## Count and say - [LeetCode](https://leetcode.com/problems/count-and-say)

immediately arrived at the logic to find the run length encoding of the given string, however, was stuck with handling the last character of the string. to handle that, the solution is embarrassingly simple. just add a whitespace to the end of the string.

my solution [here](https://leetcode.com/problems/count-and-say/submissions/1351865671/)

## Assign cookies - [LeetCode](https://leetcode.com/problems/assign-cookies)

sort both the size and greed arrays. maintain a pointer for each array `sp` and `gp` and incrmement both if `s[sp] >= g[gp]`, else just increment the size pointer.

## Power of two - [LeetCode](https://leetcode.com/problems/power-of-two)

find `n & (n - 1)`. powers of two are of the form `1000...` and one less that `n` will always be of the form `0111...`, hence the result is always `0` if `n` is a power of 2. 

## Swap two numbers - [GeeksForGeeks](https://www.geeksforgeeks.org/problems/swap-two-numbers3844/1)

there is a very simple trick to swap two numbers without using any extra memory.

```cpp
a = a ^ b;
b = a ^ b;
a = a ^ b;
```

it is guaranteed that `a` and `b` are swapped. 

for more bit manipulation techniques, see [here](https://leetcode.com/discuss/general-discussion/1073221/All-about-Bitwise-Operations-Beginner-Intermediate)

## Subsets - [LeetCode](https://leetcode.com/problems/subsets)

since i already knew that a bit manipulation approach has to be taken, i immediately found that for an array of size `k`, numbers from 0 to `2^k` can be used to mask indices of the actual array. however, the implementation was BAD, optimal approach [here](https://leetcode.com/problems/subsets/solutions/5186398/faster-less-mem-3-methods-detailed-approach-recursion-bit-mani-iterative-python-java-c/)

## Lemonade stand - [LeetCode](https://leetcode.com/problems/lemonade-change)

greedy approach is the answer. solved the problem initially without realizing that the number of $5 and $10 dollar notes need to be kept in count, so used a bunch of if-else conditions to keep that in track as well. for each transaction, manually check the number of both bills present and then provide change accordingly.

## Flood fill - [LeetCode](https://leetcode.com/problems/flood-fill)

dfs or bfs can be used here. we take the `delCol` and `delRow` approach to calculate the 4-directional neighbors of the current matrix cell. very similar to the [rotten oranges](https://leetcode.com/problems/rotten-oranges) problem.

## Ransom note - [LeetCode](https://leetcode.com/problems/ransom-note)

take an `unoreder_map` approach. for every letter in `magazine`, map it and subtract every occurence of the letter from the map when iterating through `ransomNote`. if any letter does not exist, i.e., `map[letter] < 1`, return false. felt it was very similar to [minimum presses for word](https://leetcode.com/problems/minimum-number-of-pushes-to-type-word-ii/)

## Number of 1 bits - [LeetCode](https://leetcode.com/problems/number-of-1-bits)

genius bit manipulation. for `i` in range 31 - 0, successively right shift the given number by `i` places and perform `&` with `1`. on each shift, we can determine if the last bit after the shift is `1`, thereby incrementing count everytime that `((n >> i) & 1 == 1` succeeds.

## Roman to integer - [LeetCode](https://leetcode.com/problems/roman-to-integer)

the trick is to iterate from behind the string. if the `i - 1`th bit is lesser than the `i`th bit, for example `IV`, add the resultant of their difference to the resultant integer or just add it to the integer.

## Number of islands - [LeetCode](https://leetcode.com/problems/number-of-islands)

for every cell in the matrix, perform bfs/dfs on the matrix if the current cell is `1`. if the current cell has not been visitted (vistted row, columns are kept in track using an `unordered_set`) and for each unvisitted `1`, an island is added.

key takeaway is the difference between usage of `unoreder_map` and `unordered_set`. 

## Same tree - [LeetCode](https://leetcode.com/problems/same-tree)

immediately knew it was a recursive dfs solution. but had problems defining the true/false conditions. the key is to return the logical AND: `isSameTree(p->left, q->left) && isSameTree(p->right, q->right)` as the final answer.

## Maximum points you can obtain from cards - [LeetCode](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards)

the approach is a two pointer sliding window that calculates the maximum sum by removing one element from the start and adding an element from the end. genius stuff.


![a539e5d3-3faa-43d3-bfcd-8a6549e4589b_1656213784 1710274](https://github.com/user-attachments/assets/e24ee2d1-e42c-4374-81f9-bd7e37804c07)

## Product of array except self - [LeetCode](https://leetcode.com/problems/product-of-array-except-self)

approach is to maintian a prefix and suffix product array such that `pre[i] = pre[i - 1] * nums[i - 1]` (note: product is NOT with `nums[i]`, we need everything except self) and suffix product similarly but with one element forward. then `nums[i]` simply becomes `pre[i] * suf[i]`.
