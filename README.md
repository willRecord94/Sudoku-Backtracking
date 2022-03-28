# Sudoku-Backtracking
Coursework for CM50263 Artificial Intelligence at Unviersity of Bath.

# Projection Aim:

The aim of this project for CM50263 Artificial Intelligence was to create an algorithm that is passed a Sudoku puzzle as a 9x9 Numpy Array and returns either;

1. A Solved Sudoku as a Numpy Array
2. Or if there is no solution a Numpy Array filled with -1 in all locations (Programming.vip, 2022)
Breaking down the problem:

The problem for any given Sudoku can be recognised as a constraint satisfaction problem as there are a number of variables, each of which can take a number of values subject to a set of constraints (Ralph, 2022).

This can be specifically considered as follows;
 
**X** = { X1, X2, …, Xn } is a set of variables which in this case is the values in the grid.

**D** = { D1, D2,…, Dn } is the set of domains to specify the values each variable can take. This can be any subset of the numbers from {1, 2, 3, 4, 5, 6, 7, 8, 9}.

**C** is a set of constraints which specify the values the variables are allowed to have together. In this Sudoku problem they are;

Each ‘block’ (3x3 subset of our grid) can contain within it the number 1-9 only once i.e. without duplication.
* Each row is the same in that it can only contain the numbers 1-9 once.
* Each column also can contain the numbers 1-9 once.
* There can only be one number in each position and these cannot change from the original values provided in the passed in sudoku problem.

# Choice of Method:

In considering candidates for this problem that we have studied in the unit so far, Breadth first search has a space complexity of O(bd). This meant that it was not a suitable candidate for solving the Sudoku problem. So understanding this and given the advice in lectures (Ralph, 2022) I decided to use a depth-first search algorithm combined with the constraint propagation in order to reduce the domain. In reducing the domain and being able to disregard previously explored states the space complexity and efficiency is significantly improved.

This is known as a backtracking algorithm which is a complete algorithm because it tries all possible values, therefore meaning when it’s unable to find a solution there is no valid solution. For this type of problem which has only one solution this was important.

The resulting algorithm solved all very-easy, easy and medium difficulty examples in less than a second each but began to struggle a little with the hard examples. In testing the hard sudoku’s took up to 90.21 seconds to solve (using an M1 Macbook). In total 6 test cases took longer than the 20 second time limit (57.28, 39.41, 53.87, 20.09, 42.28 seconds).

# My solution:

The solution can be understood in terms of these steps;

1. Check that a Sudoku provided is valid (do this by checking for non-zero values, then check if the cells value exists elsewhere in the corresponding row, column, or block).
2. Find an empty position.
3. Place a value in that position.
4. Check the new sudoku is valid
5. Move to next empty cell (Recursion)
6. If a dead end is found where no input is valid the algorithm will go back and try a different value in the previous state.
7. This repeats until the sudoku is full and therefore solved or all values have been tried and the result is still at which point we can confirm no valid solution exists.

Further breakdown of the functions is included below and in the code file attached as comments.

# Function breakdown

**def sudoku_solver(sudoku):** 

Solves a Sudoku puzzle and returns its unique solution. Input is a sudoku as a 9x9 numpy array with empty cells by 0. Outputs a 9x9 numpy array of integers if there is a solution. If there is no solution, all  entries are -1.

**def entry_valid(sudoku, num, row, column):**

Function that checks a given entry is valid. Checks associated column,row and box does not contain the same value. Returns False if invalid i.e. that number entered is somewhere else and returns True if number doesn't appear.

**def next_empty_pos(sudoku):**

Function that returns the row and column of the next empty position. Returns None, None if there is no other empty positions.

**def backtracker_func(sudoku):**

This function tries to solve the given puzzle using backtracking trial/error. Returning True if successful and False if not.

**def check_row_col(sudoku):**

Checks the inputted values meet with column and row constraints. Returns True if yes and False if not.

def check_block(sudoku):

Function that returns True if the block constraint is satisfied and False if not.

# Future work and scope for improvement:

This solution could be further improved by implementing a heuristic which finds the smallest subset of values available for a given entry and prioritises trying these. This would also greatly improve efficiency by decreasing the likelihood of taking an incorrect path in the decision tree and needing to backtrack.

An additional heuristic could be implemented for the least constraining value, this could be done prior to passing in the 1-9 number set and order them by this heuristic to increase the algorithm’s efficiency (Ralph, 2022).

I tried implementing the first of these options but was unable to get it working within the timeframe allotted for the coursework. 

# References:

Ralph, B 2022, Week 4: Local Search and Constraint Satisfaction, lecture notes, Artificial intelligence CM50263, University of Bath, March 2022.

Programming.vip. 2019. Basic usage of Numpy. [Online] Available from: <https://programming.vip/docs/basic-usage-of-numpy.html> [Accessed 28 March 2022].
