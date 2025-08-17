# Tic-Tac-Toe-AI
Unbeatable Tic-Tac-Toe game using Minimax algorithm in Python.


Tic-Tac-Toe AI
🎯 Objective:

Develop a Python-based Tic-Tac-Toe game with an unbeatable AI opponent using the Minimax algorithm. Optional: Use Alpha-Beta Pruning to optimize performance.

📋 Features

Two players:

Human: Plays with X or O via terminal input

AI: Plays optimally using Minimax

Input validation

Display board after each move

Detect:

Win

Draw

Optional: Add simple GUI (Tkinter / Web)

🧠 Technologies & Concepts

Python

Game Theory

Minimax Algorithm

Alpha-Beta Pruning (optional)

Terminal or GUI for interface

🧪 Sample: Minimax-based Tic-Tac-Toe AI in Python (CLI)
import math

# Constants
HUMAN = 'X'
AI = 'O'
EMPTY = ' '

# Create empty board
board = [EMPTY] * 9

# Display board
def print_board():
    for i in range(0, 9, 3):
        print(f"{board[i]} | {board[i+1]} | {board[i+2]}")
        if i < 6:
            print("---------")

# Check winner
def check_winner(b):
    wins = [(0,1,2), (3,4,5), (6,7,8), 
            (0,3,6), (1,4,7), (2,5,8), 
            (0,4,8), (2,4,6)]
    for a, b_, c in wins:
        if board[a] == board[b_] == board[c] != EMPTY:
            return board[a]
    if EMPTY not in board:
        return "Draw"
    return None

# Minimax function
def minimax(is_maximizing):
    winner = check_winner(board)
    if winner == AI:
        return 1
    elif winner == HUMAN:
        return -1
    elif winner == "Draw":
        return 0

    if is_maximizing:
        best_score = -math.inf
        for i in range(9):
            if board[i] == EMPTY:
                board[i] = AI
                score = minimax(False)
                board[i] = EMPTY
                best_score = max(score, best_score)
        return best_score
    else:
        best_score = math.inf
        for i in range(9):
            if board[i] == EMPTY:
                board[i] = HUMAN
                score = minimax(True)
                board[i] = EMPTY
                best_score = min(score, best_score)
        return best_score

# AI move
def best_move():
    best_score = -math.inf
    move = None
    for i in range(9):
        if board[i] == EMPTY:
            board[i] = AI
            score = minimax(False)
            board[i] = EMPTY
            if score > best_score:
                best_score = score
                move = i
    board[move] = AI

# Main game loop
def play():
    print("Welcome to Tic-Tac-Toe!")
    print_board()

    while True:
        try:
            human_move = int(input("Enter your move (1-9): ")) - 1
            if board[human_move] != EMPTY:
                print("Cell already taken!")
                continue
            board[human_move] = HUMAN
        except (ValueError, IndexError):
            print("Invalid input. Choose 1-9.")
            continue

        print_board()
        result = check_winner(board)
        if result:
            print(f"Game Over! Result: {result}")
            break

        print("AI is thinking...")
        best_move()
        print_board()

        result = check_winner(board)
        if result:
            print(f"Game Over! Result: {result}")
            break

if __name__ == "__main__":
    play()

📁 Recommended Project Structure
tic_tac_toe_ai/
├── main.py
├── README.md
├── .gitignore
└── LICENSE (MIT or your choice)

📝 README Example
# Tic-Tac-Toe AI

An unbeatable AI agent for the classic Tic-Tac-Toe game using the Minimax algorithm.

## Features

- Human vs AI gameplay
- AI uses Minimax for optimal strategy
- CLI-based interface
- Win/Draw detection

## How to Play

1. Run the game:


python main.py


2. Enter moves by typing a number from 1 to 9:

1 | 2 | 3
4 | 5 | 6
7 | 8 | 9

Thankyou
