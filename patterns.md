|DFS|BFS|
|---|---  |
|Uses stack. Performed iteratively using a stack or recursively using call stack.| Uses queue. Only iterative.|
| Backtracking, complete search, exhausting possible paths. | Check if path exists, finding hops. |
| Goes deep. | Goes wide. |

using `unordered_set<T>` 

1. **`insert()`**  
   - Adds a new element to the set. If the element already exists, the set remains unchanged.
   - Example: `unordered_set.insert(value);`

2. **`erase()`**  
   - Removes an element by value or iterator.
   - Example: `unordered_set.erase(value);` or `unordered_set.erase(iterator);`

3. **`find()`**  
   - Searches for an element in the set and returns an iterator to it, or `end()` if it is not found.
   - Example: `auto it = unordered_set.find(value);`

4. **`count()`**  
   - Returns 1 if the element is in the set and 0 otherwise (since duplicates are not allowed).
   - Example: `unordered_set.count(value);`

5. **`size()`**  
   - Returns the number of elements in the set.
   - Example: `unordered_set.size();`

6. **`empty()`**  
   - Checks if the set is empty.
   - Example: `unordered_set.empty();`

7. **`clear()`**  
   - Removes all elements from the set.
   - Example: `unordered_set.clear();`

8. **`begin()` and `end()`**  
   - Provides iterators to traverse the set.
   - Example: `for (auto it = unordered_set.begin(); it != unordered_set.end(); ++it) { /* use *it */ }`


explore std::bitset