<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name:Cholimgapuram Sai Likitha      </h3>
<h3>Register Number :  212224230046         </h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>

<h3>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</h3>
<h3>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</h3>
<h1>IMPLEMENTATION</h1>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h1>The Minimax algorithm</h1>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h1>Alpha-Beta pruning</h1>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance
<hr>
<h2>Sample Input and Output:</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8d5e329a-9aff-41a6-bcf0-46efa10e1b92)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/438b242d-54ba-443e-b040-a936e6ae3b55)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/99a33390-fa11-4ade-a19f-e93bcd7aaec9)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/440797bd-53cb-49c1-b18d-89776864c3e7)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/81575a16-26b2-46f1-a8ac-27c9ed0a0fe5)

<h2> Program : </h2>
import math

# Constants for players
HUMAN = 'O'
AI = 'X'
EMPTY = ' '

# Initialize the board
def create_board():
    return [[EMPTY for _ in range(3)] for _ in range(3)]

# Print the board
def print_board(board):
    for row in board:
        print('|'.join(row))
        print('-' * 5)

# Check for winner
def check_winner(board):
    # Check rows
    for row in board:
        if row[0] == row[1] == row[2] != EMPTY:
            return row[0]
    # Check columns
    for col in range(3):
        if board[0][col] == board[1][col] == board[2][col] != EMPTY:
            return board[0][col]
    # Check diagonals
    if board[0][0] == board[1][1] == board[2][2] != EMPTY:
        return board[0][0]
    if board[0][2] == board[1][1] == board[2][0] != EMPTY:
        return board[0][2]
    # No winner
    return None

# Check if board is full
def is_full(board):
    for row in board:
        if EMPTY in row:
            return False
    return True

# Evaluate board
def evaluate(board):
    winner = check_winner(board)
    if winner == AI:
        return 1
    elif winner == HUMAN:
        return -1
    else:
        return 0

# Minimax with alpha-beta pruning
def minimax(board, depth, alpha, beta, maximizingPlayer):
    score = evaluate(board)
    
    if score == 1 or score == -1 or is_full(board):
        return score

    if maximizingPlayer:
        maxEval = -math.inf
        for i in range(3):
            for j in range(3):
                if board[i][j] == EMPTY:
                    board[i][j] = AI
                    eval = minimax(board, depth + 1, alpha, beta, False)
                    board[i][j] = EMPTY
                    maxEval = max(maxEval, eval)
                    alpha = max(alpha, eval)
                    if beta <= alpha:
                        break
        return maxEval
    else:
        minEval = math.inf
        for i in range(3):
            for j in range(3):
                if board[i][j] == EMPTY:
                    board[i][j] = HUMAN
                    eval = minimax(board, depth + 1, alpha, beta, True)
                    board[i][j] = EMPTY
                    minEval = min(minEval, eval)
                    beta = min(beta, eval)
                    if beta <= alpha:
                        break
        return minEval

# AI move
def best_move(board):
    bestVal = -math.inf
    move = (-1, -1)
    for i in range(3):
        for j in range(3):
            if board[i][j] == EMPTY:
                board[i][j] = AI
                moveVal = minimax(board, 0, -math.inf, math.inf, False)
                board[i][j] = EMPTY
                if moveVal > bestVal:
                    bestVal = moveVal
                    move = (i, j)
    return move

# Main game loop
def play_game():
    board = create_board()
    print("Tic-Tac-Toe! You are 'O', AI is 'X'.")
    print_board(board)

    while True:
        # Human move
        row = int(input("Enter row (0-2): "))
        col = int(input("Enter col (0-2): "))
        if board[row][col] != EMPTY:
            print("Cell already occupied! Try again.")
            continue
        board[row][col] = HUMAN

        if check_winner(board) == HUMAN:
            print_board(board)
            print("You win!")
            break
        if is_full(board):
            print_board(board)
            print("It's a draw!")
            break

        # AI move
        ai_row, ai_col = best_move(board)
        board[ai_row][ai_col] = AI
        print("AI plays:")
        print_board(board)

        if check_winner(board) == AI:
            print("AI wins!")
            break
        if is_full(board):
            print("It's a draw!")
            break

# Run the game
if __name__ == "__main__":
    play_game()
<h2> Output :</h2>
<img width="398" height="552" alt="image" src="https://github.com/user-attachments/assets/b76f61bc-dacb-4a1d-b9ef-b689813ca44a" />
<h2>Result:</h2>
Thus the program to implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game has been executed successfully.
