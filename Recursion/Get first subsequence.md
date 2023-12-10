## Get first subsequence

### Objective


Implement an algorithm to find the first subsequence of a given array whose elements sum to a specified value and print only one valid subsequence.

**Key Steps**

1. **Initialization**
    
    - Initialize an array, `arr`, with elements `[1, 2, 1]`.
    - Set the target sum, `sum`, to `2`.
    - Initialize an empty array, `blank_arr`, to store the subsequences.
2. **First Subsequence Sum Algorithm**
    
    - Call the `getFirstSubsequence` function, passing the array, initial index (`0`), current sum (`0`), target sum, empty array, and length of the array.
    - The objective is to find and print only the first valid subsequence whose elements sum to the target sum.
3. **Generate Subsequences**
    
    - In the `getFirstSubsequence` function, if the current index `i` reaches the length of the array, check if the current sum `s` equals the target sum.
    - If the sum is equal, print the current subsequence stored in `empty_arr` and return `true` to indicate that a valid subsequence has been found.
4. **Take Element Case**
    
    - Include the current element in the subsequence by appending it to `empty_arr`.
    - Update the current sum `s` by adding the current element.
    - Recursively call the `getFirstSubsequence` function with the next index (`i+1`).
    - If a valid subsequence is found, return `true` to stop further exploration.
5. **Backtrack**
    
    - Remove the last element from `empty_arr` to backtrack and explore other possibilities.
    - Update the current sum `s` by subtracting the removed element.
6. **Not Take Element Case**
    
    - Recursively call the `getFirstSubsequence` function without including the current element in the subsequence.
    - If a valid subsequence is found, return `true` to stop further exploration.

**Note**

- The use of the `return true` statement in the recursive calls is a technique to print only one valid subsequence. Once a valid subsequence is found, the recursion stops, and further exploration is skipped. This is a base case optimization to print only one answer.
### Code
**Go**
```go
package subseq

import (
	"fmt"
)

func SubSeqSum() {
	fmt.Println("Tutorial to get first sub sequences sum")

	var arr = []int{1, 2, 1}
	var n = len(arr)
	var sum = 2
	var blank_arr []int

	// Get the first sub sequences only
	getFirstSubsequence(0, 0, sum, arr, &blank_arr, n)
}

func getFirstSubsequence(i int, s int, sum int, arr []int, empty_arr *[]int, n int) bool {
	if i == n {
		// if condition satisfied
		if s == sum {
			fmt.Println(*empty_arr)

			// Technique to print only one answer := basecase tip
			return true
		} else {
			// Condition not satisified
			return false
		}
	}

	*empty_arr = append(*empty_arr, arr[i])

	s += arr[i]
	// take
	if getFirstSubsequence(i+1, s, sum, arr, empty_arr, n) {
		return true
	}

	*empty_arr = (*empty_arr)[:len(*empty_arr)-1]
	s -= arr[i]

	// not take
	return getFirstSubsequence(i+1, s, sum, arr, empty_arr, n)
}
```

**Output**
```
Tutorial to get first sub sequences sum
[1 1]
```

**Python**

```python

def get_first_subsequence(i, s, sum, arr, empty_arr, n):
    if i == n:
        if s == sum:
            print(empty_arr)
            return True

        else:
            return False

    empty_arr.append(arr[i])

    s += arr[i]

    if get_first_subsequence(i+1, s, sum, arr, empty_arr, n):
        return True

    empty_arr.pop()
    s -= arr[i]

    return get_first_subsequence(i+1, s, sum, arr, empty_arr, n)

arr = [1, 2, 1]
n = len(arr)
sum = 2
blank_arr = []

get_first_subsequence(0, 0, sum, arr, blank_arr, n)

```

```
[1, 1]
```
### Algorithmic Complexity Analysis
#### Time Complexity:
The time complexity of the provided code can be analyzed as follows:

- **Generating First Subsequence:**
  - The `getFirstSubsequence` function is called for each element in the array, and for each element, two recursive calls are made (take and not take).
  - The number of recursive calls is \(2^n\), where \(n\) is the length of the array. This is because, for each element, there are two choices (include or exclude).
  - Each recursive call involves constant-time operations.

Therefore, the overall time complexity is exponential, \(O(2^n)\), where \(n\) is the length of the array.

#### Space Complexity:
The space complexity is influenced by the recursive call stack and the space used for the temporary array (`empty_arr`):

- **Recursive Call Stack:**
  - The depth of the recursion is at most \(n\) (the length of the array). Each recursive call consumes a constant amount of space on the call stack.
  - Therefore, the space used by the call stack is \(O(n)\).

- **Temporary Array:**
  - The size of the temporary array (`empty_arr`) can be at most \(n\) elements (when all elements are included in a subsequence).
  - Therefore, the space used by the temporary array is \(O(n)\).

Combining both contributions, the overall space complexity is \(O(n)\).

In summary:
- **Time Complexity:** \(O(2^n)\)
- **Space Complexity:** \(O(n)\)
### Recursion Tree
![getfirstsubsequence.png](img/getfirstsubsequence.png)