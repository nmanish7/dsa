## Reverse an Array

### Objective

The objective is to reverse an array of integers. The program prompts the user to input the length of the array and the elements of the array. After receiving the input, it reverses the elements of the array in-place and then prints the reversed array.

**Key Steps**

1. **Input Length of Array**
   - The program prompts the user to enter the length of the array.

2. **Initialize and Input Array Elements**
   - The program initializes an integer array based on the user-specified length.
   - It then uses a loop to read integer values from the user as input and populates the array.

3. **Print Array Before Reversing**
   - The program prints the array before any reversal operation.

4. **Array Reversal Function (`reverseArray`)**
   - The `reverseArray` function is a recursive function that performs the actual reversal.
   - It takes the index (`ind`), a pointer to the array (`arr`), and the length of the array (`n`) as parameters.
   - If the current index is greater than or equal to half of the array length, the function returns, indicating that the reversal is complete.
   - Otherwise, it swaps the elements at the current index and the corresponding index from the end of the array.
   - The function then calls itself recursively with an incremented index.

5. **Print Array After Reversing**
   - After the array has been reversed using the `reverseArray` function, the program prints the reversed array.

**Note**
- The array reversal is done in-place, meaning that it doesn't create a new array but modifies the original array directly.
- The recursion in the `reverseArray` function is used to traverse the array from both ends towards the center, swapping elements along the way.

### Code
**Go**
```go
package subseq

import (
	"bufio"
	"fmt"
	"os"
	"strconv"
	"strings"
)

func ReverseArray() {

	fmt.Println("Tutorial Reverse Array")
	fmt.Print("Enter length of array : ")
	reader := bufio.NewReader(os.Stdin)
	input, _ := reader.ReadString('\n')
	input = strings.TrimSpace(input)
	n, _ := strconv.Atoi(input)

	var arr = make([]int, n)
	for k := 0; k < n; k++ {
		input, _ = reader.ReadString('\n')
		inp, _ := strconv.Atoi(strings.TrimSpace(input))
		arr[k] = inp
	}

	fmt.Println("Before Reverse : ", arr)
	reverseArray(0, &arr, n)
	fmt.Println("After Reverse : ", arr)
}

func reverseArray(ind int, arr *[]int, n int) {
	if ind >= n/2 {
		return
	}

	temp := (*arr)[ind]
	(*arr)[ind] = (*arr)[n-ind-1]
	(*arr)[n-ind-1] = temp

	reverseArray(ind+1, arr, n)
}
```

**Output**
```
Tutorial Reverse Array
Enter length of array : 5
1
2
3
4
5
Before Reverse :  [1 2 3 4 5]
After Reverse :  [5 4 3 2 1]
```

**Python**
```python
def reverse_array(ind, arr, n):
    if ind >= n/2:
        return

    arr[ind], arr[n-ind-1] = arr[n-ind-1], arr[ind]
    reverse_array(ind+1, arr, n)


arr = [1, 2, 3, 4, 5]
reverse_array(0, arr, len(arr))
print(arr)
```

**Output**
```
[5, 4, 3, 2, 1]
```
### Algorithmic Complexity Analysis
#### Time Complexity
The time complexity of the provided code can be analyzed as follows:

- **User Input**
  - Reading the length of the array and array elements involves \(O(n)\) operations, where \(n\) is the length of the array.

- **Reversing the Array**
  - The `reverseArray` function uses recursion to swap elements from the beginning and end of the array until reaching the middle.
  - The number of recursive calls is proportional to half the length of the array, and each call involves constant-time operations.

Therefore, the overall time complexity is \(O(n)\), where \(n\) is the length of the array.

#### Space Complexity
The space complexity is influenced by the depth of the recursive call stack:

- **Recursive Call Stack**
  - The depth of the recursion is at most \(n/2\) (half the length of the array). Each recursive call consumes a constant amount of space on the call stack.

- **Additional Space**
  - The algorithm uses a constant amount of additional space to store temporary variables (e.g., `temp`).

Therefore, the overall space complexity is \(O(n)\), where \(n\) is the length of the array.

In summary:
- **Time Complexity:** \(O(n)\)
- **Space Complexity:** \(O(n)\)
### Recursion Tree
![reversearray.png](img/reversearray.png)