## N-Queens

The **n-queens** puzzle is the problem of placing `n` queens on `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return all distinct solutions to the **n-queens puzzle**.

Each solution contains a distinct bard configuration of the n-queens' placement, where `Q` and `.` both indicate a queen and an empty space, respectively.

**Example**

![nqueensexample1.png](img/nqueensexample1.png)
- If n = 4, that means place 4 Queens in 4 x 4 chess board, following rules.

**Rules**
- Every row have single queen.
- Every column have single queen.
- None of the Queen attack each others.

**Queen Attack**
- Queen can attack in eight direction.  
	1. Horizontal to the right (rank).
	2. Horizontal to the left (rank).
	3. Vertical upward (file).
	4. Vertical downward (file).
	5. Diagonal to the upper right.
	6. Diagonal to the upper left.
	7. Diagonal to the lower right.
	8. Diagonal to the lower left.
### Objective

The objective of the N-Queens problem is to find all possible configurations of placing \(n\) queens on an \(n \times n\) chessboard, such that no two queens threaten each other. A queen can attack horizontally, vertically, and diagonally.

**Key Steps**
1. **Initialize the Chess Board**
   - Create an \(n \times n\) chessboard represented by a 2D string array.
   - Initialize each cell with "." to represent an empty cell.

2. **Solve the N-Queens Problem**
   - Use a recursive function (`solve`) to explore possible queen placements column by column.
   - For each column, try placing a queen in each row.
   - Check if the placement is safe using the `isSafe1` function, considering horizontal and diagonal conflicts.
   - If a safe position is found, update the board, move to the next column, and recursively continue the exploration.
   - If a complete solution is found (all queens placed), copy the board configuration and add it to the solutions.

3. **Check Safety (`isSafe1` function)**
   - The `isSafe1` function checks for conflicts in three directions:
     - Diagonal upper left
     - Horizontal left
     - Diagonal lower left
   - These checks are performed for the current position (row, col) to ensure that placing a queen is safe.

4. **Visual Output**
   - After finding all solutions, print the final board and the N-Queens configurations.
   - Print a visual representation of each solution.

### Code

**Go**
```go
package subseq

import (
	"fmt"
)

// NQueenProblem solves the N-Queens problem and prints the board configuration.
func NQueenProblem() {
	fmt.Println("Tutorial n-queens problem")
	var n int = 4
	rows, cols := n, n
	var ans [][][]string

	// Create N x N string slice (chess board)
	var board [][]string = make([][]string, rows)
	for i := range board {
		board[i] = make([]string, cols)
	}

	// Initialize each element with "."
	for i := 0; i < rows; i++ {
		for j := 0; j < cols; j++ {
			board[i][j] = "."
		}
	}

	// Solve the N-Queens problem
	solve(0, &board, &ans, n)

	// Print the final board and the N-Queens configurations
	fmt.Println("Board : ", board)
	fmt.Println("N-Queens Output : ", ans)

	// Print a visual representation of each solution
	fmt.Println("Visual Output")
	for i := range ans {
		for k := 0; k < rows; k++ {
			fmt.Println(ans[i][k])
		}
		fmt.Println()
	}

}

// solve is a recursive function to find solutions to the N-Queens problem.
func solve(col int, board *[][]string, ans *[][][]string, n int) {

	// Base Case: All queens are placed successfully
	if col == n {
		// Creating a copy of the board and appending it to the solutions (ans)
		copyBoard := make([][]string, len((*board)))
		for i := range *board {
			copyBoard[i] = make([]string, len((*board)[i]))
			copy(copyBoard[i], (*board)[i])
		}

		*ans = append(*ans, copyBoard)
		return
	}

	// Try placing a queen in each row of the current column
	for row := 0; row < n; row++ {
		if isSafe1(row, col, *board, n) {
			(*board)[row][col] = "Q"    // Place queen
			solve(col+1, board, ans, n) // Recur to place queens in subsequent columns
			(*board)[row][col] = "."    // Backtrack: remove queen for other possibilities
		}
	}
}

// isSafe1 checks if it's safe to place a queen at a given position on the board.
func isSafe1(row int, col int, board [][]string, n int) bool {

	// Check for conflicts in three directions:
	// 1. Diagonal upper left
	// 2. Horizontal left
	// 3. Diagonal lower left
	// because other sides do not matter

	duprow := row
	dupcol := col

	// Check Diagonal upper left
	for row >= 0 && col >= 0 {
		if board[row][col] == "Q" {
			return false
		}
		row--
		col--
	}

	// Reset row and col to original values
	row = duprow
	col = dupcol

	// Check Horizontal left
	for col >= 0 {
		if board[row][col] == "Q" {
			return false
		}
		col--
	}

	// Reset row and col to original values
	row = duprow
	col = dupcol

	// Check Diagonal lower left
	for row < n && col >= 0 {
		if board[row][col] == "Q" {
			return false
		}
		row++
		col--
	}

	// If no conflicts were found, it's safe to place a queen at the given position
	return true

}
```

**Output**
```go
Tutorial n-queens problem
Board :  [[. . . .] [. . . .] [. . . .] [. . . .]]
N-Queens Output :  [[[. . Q .] [Q . . .] [. . . Q] [. Q . .]] [[. Q . .] [. . . Q] [Q . . .] [. . Q .]]]
Visual Output
[. . Q .]
[Q . . .]
[. . . Q]
[. Q . .]

[. Q . .]
[. . . Q]
[Q . . .]
[. . Q .]

```

**Why to check conflicts in three directions?**

Certainly! In the context of the N-Queens problem, when checking for the safety of placing a queen in a particular position, we only need to consider the conflicts that can arise in three directions: diagonal upper left, horizontal left, and diagonal lower left. The reason other directions are not considered is based on the nature of the problem and the rules of chess.

Here's a breakdown of the considerations:

1. **Diagonal Upper Left:**
   - Queens moving in the diagonal upper-left direction will be on the same diagonal. Placing a queen in a position (row, col) means that it can potentially attack other queens in the diagonal upper left. So, we need to check for queens in that direction to ensure safety.

2. **Horizontal Left:**
   - Queens moving horizontally to the left on the same row can potentially be attacked by a queen placed in the current position. Therefore, we check for queens in the same row to the left.

3. **Diagonal Lower Left:**
   - Similar to the diagonal upper left, placing a queen in a position can potentially attack other queens in the diagonal lower left. Therefore, we need to check for queens in that direction.

The reason other directions are not explicitly checked is that, according to the rules of chess and the N-Queens problem, these are the only directions in which a queen can directly attack or be attacked by another queen. The placement of queens in these three directions is sufficient to guarantee that no two queens attack each other on the chessboard.

Considering other directions (e.g., right, upward diagonals, downward diagonals) is unnecessary because queens moving in those directions would be in different rows or columns, and therefore, their paths wouldn't intersect. The rules of chess and the constraints of the N-Queens problem simplify the checks to these three specific directions for efficiency and correctness.


**Python**
```python
def solve(col, board, ans, n):
    # Base case: All queens are placed successfully
    if col == n:
        # ans.append(board.copy())

        # Append a deep copy of the current board to the solutions
        ans.append([row.copy() for row in board])
        return

    # Try placing a queen in each row of the current column
    for row in range(n):
        if is_safe1(row, col, board, n):
            # Place queen
            board[row][col] = "Q"
            # Recur to place queens in subsequent columns
            solve(col+1, board, ans, n)
            # Backtrack: remove queen for other possibilities
            board[row][col] = "."


def is_safe1(row, col, board, n):
    duprow = row
    dupcol = col

    # Check Diagonal upper left
    while row >= 0 and col >= 0:
        if board[row][col] == "Q":
            return False

        row -= 1
        col -= 1

    row = duprow
    col = dupcol

    # Check Horizontal left
    while col >= 0:
        if board[row][col] == "Q":
            return False

        col -= 1

    row = duprow
    col = dupcol

    # Check Diagonal lower left
    while row < n and col >= 0:
        if board[row][col] == "Q":
            return False

        row += 1
        col -= 1

    return True


n = 4
ans = []
# board = [["."] * n] * n # Problem : creates a list containing n references to the same list, resulting in a shared reference for each row.

# Use a list comprehension to create independent rows
board = [["."] * n for _ in range(n)]


solve(0, board, ans, n)

print(ans)
print()


# Print each solution in a visually understandable format
for board in ans:
    for row in board:
        print(row)
    print()
```

**Output**
```python
[[['.', '.', 'Q', '.'], ['Q', '.', '.', '.'], ['.', '.', '.', 'Q'], ['.', 'Q', '.', '.']], [['.', 'Q', '.', '.'], ['.', '.', '.', 'Q'], ['Q', '.', '.', '.'], ['.', '.', 'Q', '.']]]

['.', '.', 'Q', '.']
['Q', '.', '.', '.']
['.', '.', '.', 'Q']
['.', 'Q', '.', '.']

['.', 'Q', '.', '.']
['.', '.', '.', 'Q']
['Q', '.', '.', '.']
['.', '.', 'Q', '.']

```
### Algorithmic Complexity Analysis

#### Time Complexity
- The time complexity of the N-Queens problem is typically \(O(n!)\), where \(n\) is the size of the chessboard.
- The number of recursive calls is \(n^n\) in the worst case.
- The \(n!\) term arises from the fact that in each column, we have \(n\) choices for queen placement, resulting in n x (n - 1) x (n - 2) x ... x 1 = n! possibilities.

#### Space Complexity
- The space complexity mainly depends on the storage of the chessboard configurations and the recursive call stack.
- The space complexity is \(O(n^2)\) for storing the chessboard configurations, as it is an \(n \times n\) array.
- The recursive call stack can go up to \(O(n)\) in depth.

Note: The precise analysis of space complexity may vary depending on the specific implementation details and language-specific factors.

### Recursion Tree

![nqueens1.png](img/nqueens1.png)