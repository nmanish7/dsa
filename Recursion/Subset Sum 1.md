### Given a list (Arr) of N integers, print sums of all subset in it. Output should be printed in increasing order of sums.

**Example**
```
Input:
N = 2
Arr = [2,3]

Output:
0 2 3 5

Explanation:
When no elements is taken then Sum = 0.
When only 2 is taken then Sum = 2.
When only 3 is taken then Sum = 3.
When element 2 and 3 are taken then Sum = 2 + 3 = 5.

```

**Go Code**
```go
package subseq

import (
	"fmt"
)

func SubSetSum1() {
	fmt.Println("Tutorial for SubSetSum 1")
	var arr = []int{3, 1, 2}
	var length int = len(arr)
	var sumArr []int

	// Calling function
	doSubSetSum1(0, 0, &arr, length, &sumArr)

	fmt.Println("Input Array : ", arr)
	fmt.Println("Sum Sub Set Array : ", sumArr)

	DoQuickSort(&sumArr, 0, len(sumArr)-1)

	fmt.Println("After Sorting : ", sumArr)
}

func doSubSetSum1(ind int, sum int, arr *[]int, n int, sumArr *[]int) {
	if ind == n {
		(*sumArr) = append((*sumArr), sum)
		return
	}

	// pick the element
	doSubSetSum1(ind+1, sum+(*arr)[ind], arr, n, sumArr)

	// Do-not pick the element
	doSubSetSum1(ind+1, sum, arr, n, sumArr)

}
```

**Output:**
```
Tutorial for SubSetSum 1
Input Array :  [3 1 2]
Sum Sub Set Array :  [6 4 5 3 3 1 2 0]
After Sorting :  [0 1 2 3 3 4 5 6]
```

**Python Code**
```Python
def do_subset_sum1(ind, sum, arr, n, sumArr ):
    if ind == n:
        sumArr.append(sum)
        return
    
    do_subset_sum1(ind+1, sum+arr[ind], arr, n, sumArr)
    do_subset_sum1(ind+1, sum, arr, n, sumArr)



arr = [3,1,2]
sumArr = []
do_subset_sum1(0,0,arr,len(arr), sumArr)
print(sumArr)
```

**Output:**
```
[6, 4, 5, 3, 3, 1, 2, 0]
```

**Recursion Tree**

![subsetsum1recursiontree.png](subsetsum1recursiontree.PNG)
