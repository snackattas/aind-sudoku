# Artificial Intelligence Nanodegree
## Introductory Project: Diagonal Sudoku Solver

# Question 1 (Naked Twins)
Q: How do we use constraint propagation to solve the naked twins problem?  
A: Constraint propagation is a technique that helps reduce the domain of a decision variable, in this case, our values dict variable.  The values dict is considered to be reduced if there are less digits present in its values after some work done.  This factors into the naked twins problem in the sense that, in addition to eliminate and only choice, naked twins is an additional technique to reduce the digits present in the value dict's values.  

Here's how naked twins works:
* First it finds the boxes that:
  * Are in the same unit
    * A unit is a set of 9 boxes that need to be unique and have all 1-9 digits present, like [A1, A2, A3, A4, A5, A6, A7, A8, A9]
  * Have >1 digit
  * The values in the boxes are identical to each other
  * The number of digits in the value equals the number of identical boxes' values. Ex:
    * {A1: 12, A4: 12}
    * {A1: 123, A2: 123, A4: 123}
* We can extrapolate that for the naked twin boxes, the final values are ensured to be one of the values present.  
* Because of this, we can remove identical naked twins values from the non-naked twins boxes' values in the unit:
  * Before naked twins: {A1: 123, A2: 123, A3: 123, A4: 134}
  * After naked twins: {A1: 123, A2: 123, A3: 123, A4: 4}

# Question 2 (Diagonal Sudoku)
Q: How do we use constraint propagation to solve the diagonal sudoku problem?  
A: Constraint propagation is a technique that helps reduce the domain of a decision variable, in this case, our values dict variable.  The values dict is considered to be reduced if there are less digits present in its values after some work done.  

A useful way to think about solving sudoku puzzles is to divide the boxes into units, or sets of 9 boxes that need to be unique and have all 1-9 digits present, like [A1, A2, A3, A4, A5, A6, A7, A8, A9].  The thing about units in sudoku is that boxes overlap in different units (that's the nature of the sudoku puzzle).  For example, the unit [A1, A2, A3, B1, B2, B3, C1, C2, C3] has boxes that overlap with the earlier example. So if you're able to reduce the possible values for one box, that will aid the completion of the units that the box belongs too.  Let's say A1 is first thought to be either '12356', but through various techniques, we're able to reduce its possibilities to '12'.  That reduction in possible values will make it easier to solve *both* of the units mentioned.  

Taking that logic one step further, the more units that are present, the more boxes that overlap in different units.  This means that a reduction in possibilities for a box will have more repercussions, and enable the puzzle to be solved faster.  That's what's happening with diagonal sudoku.  The two units [A1, B2, C3, D4, E5, F6, G7, H8, I9] and [A9, B8, C7, D6, E5, F4, G3, H2, I1] are added to the set of domains. Therefore, the puzzle has more constraints and can be solved faster!

### Install

This project requires **Python 3**.

We recommend students install [Anaconda](https://www.continuum.io/downloads), a pre-packaged Python distribution that contains all of the necessary libraries and software for this project.
Please try using the environment we provided in the Anaconda lesson of the Nanodegree.

##### Optional: Pygame

Optionally, you can also install pygame if you want to see your visualization. If you've followed our instructions for setting up our conda environment, you should be all set.

If not, please see how to download pygame [here](http://www.pygame.org/download.shtml).

### Code

* `solution.py` - Fill in the required functions in this file to complete the project.
* `test_solution.py` - You can test your solution by running `python -m unittest`.
* `PySudoku.py` - This is code for visualizing your solution.
* `visualize.py` - This is code for visualizing your solution.

### Visualizing

To visualize your solution, please only assign values to the values_dict using the `assign_value` function provided in solution.py

### Submission
Before submitting your solution to a reviewer, you are required to submit your project to Udacity's Project Assistant, which will provide some initial feedback.  

The setup is simple.  If you have not installed the client tool already, then you may do so with the command `pip install udacity-pa`.  

To submit your code to the project assistant, run `udacity submit` from within the top-level directory of this project.  You will be prompted for a username and password.  If you login using google or facebook, visit [this link](https://project-assistant.udacity.com/auth_tokens/jwt_login) for alternate login instructions.

This process will create a zipfile in your top-level directory named sudoku-<id>.zip.  This is the file that you should submit to the Udacity reviews system.
