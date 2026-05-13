<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>NAME : MOHAMMED SAFI F       </h3>
<h3>REGISTER NUMBER : 212224060156         </h3>
<h3>AIM</h3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h3>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h3>

Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.
Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.

<h3>IMPLEMENTATION</h3>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h3>The Minimax algorithm</h3>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h3>Alpha-Beta pruning</h3>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance
### PROGRAM
```python
import math

# Print the board in 3x3 format
def print_board(board):
    print("\n")
    for i in range(3):
        print(board[3*i], board[3*i+1], board[3*i+2])
    print("\n")

# Check winner
def check_winner(board, player):
    win_states = [
        [0,1,2], [3,4,5], [6,7,8],      # Rows
        [0,3,6], [1,4,7], [2,5,8],      # Columns
        [0,4,8], [2,4,6]                # Diagonals
    ]
    return any(all(board[pos] == player for pos in state) for state in win_states)

# Check draw
def is_draw(board):
    return all(cell != "_" for cell in board)


#   MINIMAX + ALPHA-BETA
def minimax(board, depth, alpha, beta, is_maximizing):

    # Terminal conditions
    if check_winner(board, "O"):
        return 1
    if check_winner(board, "X"):
        return -1
    if is_draw(board):
        return 0

    # Maximizing player (AI = O)
    if is_maximizing:
        best_score = -math.inf

        for i in range(9):
            if board[i] == "_":
                board[i] = "O"
                score = minimax(board, depth + 1, alpha, beta, False)
                board[i] = "_"

                best_score = max(best_score, score)
                alpha = max(alpha, score)

                if beta <= alpha:
                    break  # Beta cutoff

        return best_score

    # Minimizing player (Human = X)
    else:
        best_score = math.inf

        for i in range(9):
            if board[i] == "_":
                board[i] = "X"
                score = minimax(board, depth + 1, alpha, beta, True)
                board[i] = "_"

                best_score = min(best_score, score)
                beta = min(beta, score)

                if beta <= alpha:
                    break  # Alpha cutoff

        return best_score

# Choose best AI move
def ai_move(board):
    best_score = -math.inf
    move = -1

    for i in range(9):
        if board[i] == "_":
            board[i] = "O"
            score = minimax(board, 0, -math.inf, math.inf, False)
            board[i] = "_"

            if score > best_score:
                best_score = score
                move = i

    board[move] = "O"

#     GAME LOOP
def play_game():
    board = ["_"] * 9

    print("TIC-TAC-TOE with Alpha-Beta Pruning")
    print("You are X, Computer is O")
    print_board(board)

    while True:
        # Human turn
        try:
            user = int(input("Enter your move (0-8): "))
        except:
            print("Invalid input! Enter a number between 0 and 8.")
            continue

        if user < 0 or user > 8 or board[user] != "_":
            print("Invalid move! Try again.")
            continue

        board[user] = "X"
        print_board(board)

        if check_winner(board, "X"):
            print(" You Win!")
            break
        if is_draw(board):
            print(" It's a Draw!")
            break

        # AI turn
        print("Computer thinking...")
        ai_move(board)
        print_board(board)

        if check_winner(board, "O"):
            print(" Computer Wins!")
            break
        if is_draw(board):
            print(" It's a Draw!")
            break

# Run the game
play_game()
```
### OUTPUT

<img width="449" height="806" alt="image" src="https://github.com/user-attachments/assets/ad3d7d96-a709-41f0-b423-7c88eea2b711" />

```
TIC-TAC-TOE with Alpha-Beta Pruning
You are X, Computer is O


_ _ _
_ _ _
_ _ _


Enter your move (0-8): 5


_ _ _
_ _ X
_ _ _


Computer thinking...


_ _ O
_ _ X
_ _ _


Enter your move (0-8): 4


_ _ O
_ X X
_ _ _


Computer thinking...


_ _ O
O X X
_ _ _


Enter your move (0-8): 1


_ X O
O X X
_ _ _


Computer thinking...


_ X O
O X X
_ O _


Enter your move (0-8): 0


X X O
O X X
_ O _


Computer thinking...


X X O
O X X
_ O O


Enter your move (0-8): 6


X X O
O X X
X O O


 It's a Draw!
```

### RESULT
Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game is implemented.
