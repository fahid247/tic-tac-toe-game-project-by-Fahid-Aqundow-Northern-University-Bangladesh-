#include <stdio.h>

char board[3][3];

void initializeBoard() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            board[i][j] = ' ';
        }
    }
}

void printBoard() {
    printf(" %c | %c | %c\n", board[0][0], board[0][1], board[0][2]);
    printf("---+---+---\n");
    printf(" %c | %c | %c\n", board[1][0], board[1][1], board[1][2]);
    printf("---+---+---\n");
    printf(" %c | %c | %c\n", board[2][0], board[2][1], board[2][2]);
}

int checkWin(char player) {

    for (int i = 0; i < 3; i++) {
        if (board[i][0] == player && board[i][1] == player && board[i][2] == player)
            return 1;
        if (board[0][i] == player && board[1][i] == player && board[2][i] == player)
            return 1;
    }
    if (board[0][0] == player && board[1][1] == player && board[2][2] == player)
        return 1;
    if (board[0][2] == player && board[1][1] == player && board[2][0] == player)
        return 1;
    return 0;
}

int main() {
    char currentPlayer = 'X';
    int row, col;

    initializeBoard();

    printf("Welcome to fahid's cross zero game \n");

    for (int turn = 0; turn < 9; turn++) {
        printf("\nCurrent board:\n");
        printBoard();

        printf("Player %c's turn. Enter row (0-2) and column (0-2): ", currentPlayer);
        scanf("%d %d", &row, &col);

        if (row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] != ' ') {
            printf("Invalid move! Try again.\n");
            turn--;
            continue;
        }

        board[row][col] = currentPlayer;

        if (checkWin(currentPlayer)) {
            printf("\nPlayer %c wins!\n", currentPlayer);
            printBoard();
            break;
        }

        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    if (!checkWin('X') && !checkWin('O')) {
        printf("\nIt's a draw!\n");
        printBoard();
    }

    return 0;
}
