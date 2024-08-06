# Sudoku_Solver


Overview
This project contains a Java implementation of a Sudoku solver using the backtracking algorithm. The solution is implemented within the `Solution` class, which provides methods to check if a number can be placed in a specific cell (`isSafe`), a recursive helper function to solve the Sudoku (`helper`), and a public method to start the solving process (`solveSudoku`).



How It Works

1. `isSafe` Method

The `isSafe` method checks if a given number can be placed in a specified cell of the Sudoku board without violating the Sudoku rules. The method performs three checks:

* Column Check: Ensures the number does not already exist in the column.
* Row Check: Ensures the number does not already exist in the row.
* Grid Check: Ensures the number does not already exist in the 3x3 sub-grid.


public boolean isSafe(char[][] board, int row, int col, int number) {
    // Column check
    for(int i = 0; i < board.length; i++) {
        if(board[i][col] == (char)(number + '0')) {
            return false;
        }
    }
    // Row check
    for(int j = 0; j < board.length; j++) {
        if(board[row][j] == (char)(number + '0')) {
            return false;
        }
    }
    // Grid check
    int sr = 3 * (row / 3);
    int sc = 3 * (col / 3);
    for(int i = sr; i < sr + 3; i++) {
        for(int j = sc; j < sc + 3; j++) {
            if(board[i][j] == (char)(number + '0')) {
                return false;
            }
        }
    }
    return true;
}

2. `helper` Method
The `helper` method is a recursive function that attempts to solve the Sudoku board by trying to place numbers from 1 to 9 in each cell. If a cell is already filled, it moves to the next cell. If placing a number violates the Sudoku rules, it backtracks and tries the next number.



public boolean helper(char[][] board, int row, int col) {
    if(row == board.length) {
        return true;
    }
    int nrow = 0;
    int ncol = 0;
    if(col == board.length - 1) {
        nrow = row + 1;
        ncol = 0;
    } else {
        nrow = row;
        ncol = col + 1;
    }
    if(board[row][col] != '.') {
        if(helper(board, nrow, ncol)) {
            return true;
        }
    } else {
        for(int i = 1; i <= 9; i++) {
            if(isSafe(board, row, col, i)) {
                board[row][col] = (char)(i + '0');
                if(helper(board, nrow, ncol))
                    return true;
                else
                    board[row][col] = '.';
            }
        }
    }
    return false;
}

3. `solveSudoku` Method

The `solveSudoku` method is the entry point to start solving the Sudoku. It calls the helper method with the initial parameters.



public void solveSudoku(char[][] board) {
    helper(board, 0, 0);
}



Usage


Create an instance of the `Solution` class.
Call the `solveSudoku` method with the Sudoku board as an argument.



public static void main(String[] args) {
    char[][] board = {
        {'5', '3', '.', '.', '7', '.', '.', '.', '.'},
        {'6', '.', '.', '1', '9', '5', '.', '.', '.'},
        {'.', '9', '8', '.', '.', '.', '.', '6', '.'},
        {'8', '.', '.', '.', '6', '.', '.', '.', '3'},
        {'4', '.', '.', '8', '.', '3', '.', '.', '1'},
        {'7', '.', '.', '.', '2', '.', '.', '.', '6'},
        {'.', '6', '.', '.', '.', '.', '2', '8', '.'},
        {'.', '.', '.', '4', '1', '9', '.', '.', '5'},
        {'.', '.', '.', '.', '8', '.', '.', '7', '9'}
    };
    Solution solution = new Solution();
    solution.solveSudoku(board);
}


Conclusion

This project demonstrates a simple and effective way to solve Sudoku puzzles using the backtracking algorithm. The implementation is straightforward and can be easily extended or modified for more complex variations of the Sudoku puzzle.
