#include <iostream>
using namespace std;
const int SIZE = 3;
char board[SIZE][SIZE] = {{'1', '2', '3'}, {'4', '5', '6'}, {'7', '8', '9'}};
void displayBoard() {
    for (int i = 0; i < SIZE; ++i) {
        for (int j = 0; j < SIZE; ++j) {
            cout << board[i][j] << " ";
        }
        cout << endl;
    }
}
bool isWinner(char player) {
    for (int i = 0; i < SIZE; ++i) {
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
bool isDraw() {
    for (int i = 0; i < SIZE; ++i) {
        for (int j = 0; j < SIZE; ++j) {
            if (board[i][j] != 'X' && board[i][j] != 'O') {
                return false;
            }
        }
    }
    return true;
}
void makeMove(char player) {
    int move;
    cout << "Player " << player << ", enter your move (1-9): ";
    cin >> move;
    int row = (move - 1) / SIZE;
    int col = (move - 1) % SIZE;
    if (board[row][col] != 'X' && board[row][col] != 'O') {
        board[row][col] = player;
    } else {
        cout << "Invalid move, try again." << endl;
        makeMove(player);
    }
}
int main() {
    char currentPlayer = 'X';
    bool gameWon = false;
    while(!gameWon && !isDraw()) {
        displayBoard();
        makeMove(currentPlayer);
        gameWon = isWinner(currentPlayer);
        if (gameWon) {
            displayBoard();
            cout << "Player " << currentPlayer << " wins!" << endl;
        } else if (isDraw()) {
            displayBoard();
            cout << "The game is a draw!" << endl;
        }
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }
    return 0;
}
