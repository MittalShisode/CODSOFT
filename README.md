#include <iostream>
#include <vector>
#include <string>

using namespace std;

void displayBoard(const vector<vector<char>>& board) {
    cout << "\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << board[i][j];
            if (j < 2) cout << " | ";
        }
        cout << "\n";
        if (i < 2) cout << "--|---|--\n";
    }
    cout << "\n";
}

bool checkWin(const vector<vector<char>>& board, char player) {
    for (int i = 0; i < 3; i++) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) {
            return true;
        }
    }
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
        return true;
    }
    return false;
}

bool checkDraw(const vector<vector<char>>& board) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ') {
                return false;
            }
        }
    }
    return true;
}

int main() {
    char playAgain = 'y';
    while (playAgain == 'y' || playAgain == 'Y') {
        vector<vector<char>> board(3, vector<char>(3, ' '));
        char currentPlayer = 'X';
        bool gameWon = false;
        cout << "Welcome to Tic-Tac-Toe!\n";
        displayBoard(board);
        while (true) {
            int row, col;
            cout << "Player " << currentPlayer << "'s turn. Enter row and column (1-3): ";
            cin >> row >> col;
            if (row < 1 || row > 3 || col < 1 || col > 3 || board[row - 1][col - 1] != ' ') {
                cout << "Invalid move! Try again.\n";
                continue;
            }
            board[row - 1][col - 1] = currentPlayer;
            displayBoard(board);
            if (checkWin(board, currentPlayer)) {
                cout << "Player " << currentPlayer << " wins!\n";
                gameWon = true;
                break;
            }
            if (checkDraw(board)) {
                cout << "It's a draw!\n";
                break;
            }
            currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
        }
        cout << "Do you want to play again? (y/n): ";
        cin >> playAgain;
    }
    cout << "Thank you for playing Tic-Tac-Toe!\n";
    return 0;
}
