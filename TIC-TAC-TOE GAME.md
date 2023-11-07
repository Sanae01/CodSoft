```python
import random
```


```python
# Initialize the Tic-Tac-Toe board
board = [' ' for _ in range(9)]
```


```python
# Define winning combinations
winning_combinations = [(0, 1, 2), (3, 4, 5), (6, 7, 8), (0, 3, 6), (1, 4, 7), (2, 5, 8), (0, 4, 8), (2, 4, 6)]
```


```python
# Function to print the board
def print_board(board):
    for i in range(0, 9, 3):
        print(board[i], '|', board[i+1], '|', board[i+2])
        if i < 6:
            print('---------')
```


```python
# Function to check for a win
def check_win(board, player):
    for combo in winning_combinations:
        if all(board[i] == player for i in combo):
            return True
    return False
```


```python
# Function to check for a tie
def check_tie(board):
    return ' ' not in board
```


```python
# Minimax algorithm with alpha-beta pruning
def minimax(board, depth, maximizing_player):
    if check_win(board, 'O'):
        return 1
    if check_win(board, 'X'):
        return -1
    if check_tie(board):
        return 0

    if maximizing_player:
        max_eval = -float('inf')
        for i in range(9):
            if board[i] == ' ':
                board[i] = 'O'
                eval = minimax(board, depth + 1, False)
                board[i] = ' '
                max_eval = max(max_eval, eval)
        return max_eval
    else:
        min_eval = float('inf')
        for i in range(9):
            if board[i] == ' ':
                board[i] = 'X'
                eval = minimax(board, depth + 1, True)
                board[i] = ' '
                min_eval = min(min_eval, eval)
        return min_eval
```


```python
# AI's move
def ai_move(board):
    best_move = -1
    best_eval = -float('inf')
    for i in range(9):
        if board[i] == ' ':
            board[i] = 'O'
            eval = minimax(board, 0, False)
            board[i] = ' '
            if eval > best_eval:
                best_eval = eval
                best_move = i
    return best_move
```


```python
# Main game loop
while True:
    print_board(board)
    player_move = int(input("Enter your move (0-8): " ))
    
    if board[player_move] == ' ':
        board[player_move] = 'X'
        if check_win(board, 'X'):
            print_board(board)
            print("You win!")
            break
        elif check_tie(board):
            print_board(board)
            print("It's a tie!")
            break
        
        ai_best_move = ai_move(board)
        board[ai_best_move] = 'O'
        if check_win(board, 'O'):
            print_board(board)
            print("AI wins!")
            break
        elif check_tie(board):
            print_board(board)
            print("It's a tie!")
            break
    else:
        print("Invalid move. Try again.")

```

    O | X | O
    ---------
    X | X | O
    ---------
    X | O | X
    


```python

```
