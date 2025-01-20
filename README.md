# Sudoku-solver-using-Backtracking
Below is a Python implementation of a Sudoku solver using Backtracking. The algorithm systematically tries to fill in the grid by checking all possible values for each empty cell. If it reaches a point where no valid values are possible, it backtracks and tries a different combination for previous cells.
Python Code for Sudoku Solver with Backtracking:

# Sudoku Solver using Backtracking

def is_valid(board, row, col, num):
    """ Check if it's valid to place the number `num` in the board at position (row, col) """
    
    # Check if the number exists in the row
    for i in range(9):
        if board[row][i] == num:
            return False
    
    # Check if the number exists in the column
    for i in range(9):
        if board[i][col] == num:
            return False
    
    # Check if the number exists in the 3x3 grid
    start_row = (row // 3) * 3
    start_col = (col // 3) * 3
    for i in range(3):
        for j in range(3):
            if board[start_row + i][start_col + j] == num:
                return False
    
    return True

def solve_sudoku(board):
    """ Solve Sudoku using Backtracking """
    
    # Find an empty cell (represented by 0)
    for row in range(9):
        for col in range(9):
            if board[row][col] == 0:
                # Try possible numbers 1 through 9
                for num in range(1, 10):
                    if is_valid(board, row, col, num):
                        board[row][col] = num
                        
                        # Recursively try to solve the rest of the board
                        if solve_sudoku(board):
                            return True
                        
                        # Backtrack if placing num didn't work
                        board[row][col] = 0
                
                # If no number can fit, return False (backtrack)
                return False
    
    # If no empty cell is left, the board is solved
    return True

def print_board(board):
    """ Print the Sudoku board """
    for row in board:
        print(" ".join(str(num) if num != 0 else '.' for num in row))

# Example Sudoku puzzle (0's represent empty cells)
board = [
    [5, 3, 0, 0, 7, 0, 0, 0, 0],
    [6, 0, 0, 1, 9, 5, 0, 0, 0],
    [0, 9, 8, 0, 0, 0, 0, 6, 0],
    [8, 0, 0, 0, 6, 0, 0, 0, 3],
    [4, 0, 0, 8, 0, 3, 0, 0, 1],
    [7, 0, 0, 0, 2, 0, 0, 0, 6],
    [0, 6, 0, 0, 0, 0, 2, 8, 0],
    [0, 0, 0, 4, 1, 9, 0, 0, 5],
    [0, 0, 0, 0, 8, 0, 0, 7, 9]
]

# Solve the Sudoku puzzle
if solve_sudoku(board):
    print("Sudoku solved successfully!")
    print_board(board)
else:
    print("No solution exists for the given Sudoku.")

Explanation:

    is_valid(board, row, col, num):
        Checks whether placing num at board[row][col] is valid based on Sudoku rules.
        It verifies if num is not already present in the current row, column, or 3x3 subgrid.

    solve_sudoku(board):
        This function uses backtracking to try placing numbers in empty cells.
        It recursively tries numbers 1 through 9 for each empty cell and backtracks if it encounters an invalid configuration.

    print_board(board):
        Prints the Sudoku grid in a readable format.

    The Sudoku Puzzle (board):
        The board is represented as a 9x9 matrix, where each element is an integer.
        0 represents an empty cell.

Example:

Input Sudoku Puzzle:

5 3 0 0 7 0 0 0 0
6 0 0 1 9 5 0 0 0
0 9 8 0 0 0 0 6 0
8 0 0 0 6 0 0 0 3
4 0 0 8 0 3 0 0 1
7 0 0 0 2 0 0 0 6
0 6 0 0 0 0 2 8 0
0 0 0 4 1 9 0 0 5
0 0 0 0 8 0 0 7 9

Output (after solving):

Sudoku solved successfully!
5 3 4 6 7 8 9 1 2
6 7 2 1 9 5 3 4 8
1 9 8 3 4 2 5 6 7
8 5 9 7 6 1 4 2 3
4 2 6 8 5 3 7 9 1
7 1 3 9 2 4 8 5 6
9 6 1 5 3 7 2 8 4
2 8 7 4 1 9 6 3 5
3 4 5 2 8 6 1 7 9

Key Concepts:

    Backtracking: This is a general algorithm for finding all (or some) solutions to a problem by incrementally building a solution and abandoning partial solutions when they can no longer lead to a valid solution (i.e., when a conflict occurs).
    Recursion: We use recursion to solve the puzzle step-by-step. If we reach a situation where no valid value can be placed in a cell, the algorithm backtracks and tries a different path.

This algorithm is quite efficient for standard Sudoku puzzles and can be easily adapted to more complex variants.
