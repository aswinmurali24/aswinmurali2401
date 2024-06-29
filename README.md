Simple Treasure Hunter Game

Description
This JavaScript program implements a simple game with three stages: setup, play, and end. The game is played on a 10x10 grid surrounded by an insurmountable wall and features a treasure hunter controlled by the user, who collects treasures placed on the grid.

Setup Stage
Grid Display: User sees a 10x10 grid.
Placing Objects:
Click a cell and type a number (5-8) to place a treasure with that value.
Type "o" to place an obstacle.
Type "h" to place the treasure hunter (only one allowed).
Invalid inputs show an error message.
Objects cannot be changed once placed.

End Setup: Click the button to proceed to the play stage. An error is shown if the treasure hunter is not placed.

Play Stage
Initial Display: Shows the grid with objects and status information:
Number of rounds completed.
Number of remaining treasures (by value).
User's score (initially 0).

Gameplay:
Move the treasure hunter using "a" (left), "d" (right), "w" (up), and "s" (down).
Invalid moves or commands show an error message.
If the treasure hunter moves onto a treasure, it is collected, score is updated, and an obstacle is added to a random empty cell.

End Play: Can end manually, or automatically if no moves are possible or no treasures remain.

End Stage
Performance Index: Calculated as score divided by rounds completed, rounded to two decimal places. Displayed with a message.
Game link is here : [https://student.csc.liv.ac.uk/~sgamura2/treasures.html] 
