#include <iostream>

using namespace std;

// Функция для вывода  поля на экран
void PrintBoard(char** board, int size) {
    for (int i = 0; i < size; ++i) {
        for (int j = 0; j < size; ++j) {
            cout << board[i][j] << " ";
        }
        cout << endl;
    }
}

// Функция для проверки выигрышнвй комбинации
bool CheckWin(char** board, int size, char symbol) {
    for (int i = 0; i < size; ++i) {
        bool rowWin = true;
        bool colWin = true;
        for (int j = 0; j < size; ++j) {
            if (board[i][j] != symbol)
                rowWin = false;
            if (board[j][i] != symbol)
                colWin = false;
        }
        if (rowWin || colWin)
            return true;
    }

    // Проверка диагонлц
    bool diag1Win = true;
    bool diag2Win = true;
    for (int i = 0; i < size; ++i) {
        if (board[i][i] != symbol)
            diag1Win = false;
        if (board[i][size - i - 1] != symbol)
            diag2Win = false;
    }
    if (diag1Win || diag2Win)
        return true;

    return false;
}

// Функция для хода бота
void BotMove(char** board, int size, char symbol) {
    //  бот выбирает первое доступное пустое поле
    for (int i = 0; i < size; ++i) {
        for (int j = 0; j < size; ++j) {
            if (board[i][j] == '-') {
                board[i][j] = symbol;
                return;
            }
        }
    }
}

int main() {
    int size;
    cout << "Enter the size of the board: ";
    cin >> size;

    // Инициализация поля
    char** board = new char* [size];
    for (int i = 0; i < size; ++i) {
        board[i] = new char[size];
        for (int j = 0; j < size; ++j) {
            board[i][j] = '-';
        }
    }

    // Игровой цикл
    char currentPlayer = 'X';
    bool gameOver = false;
    while (!gameOver) {
        // Вывод  состояния поля
        cout << "Current board:" << endl;
        PrintBoard(board, size);

        if (currentPlayer == 'X') {
            // Ход игрока
            int row, col;
            cout << "Player " << currentPlayer << ", enter your move (row and column): ";
            cin >> row >> col;

            if (row < 0 || row >= size || col < 0 || col >= size || board[row][col] != '-') {
                cout << "Error: Field doesn't exist or already taken. Please try again." << endl;
                continue;
            }

            board[row][col] = currentPlayer;

            // Проверка на победу
            if (CheckWin(board, size, currentPlayer)) {
                cout << "Player " << currentPlayer << " wins!" << endl;
                gameOver = true;
                break;
            }
        }
        else {
            // Ход бота
            cout << "Bot's turn..." << endl;
            BotMove(board, size, currentPlayer);

            // Проверка на победу
            if (CheckWin(board, size, currentPlayer)) {
                cout << "Bot wins!" << endl;
                gameOver = true;
                break;
            }
        }

        // Проверка на ничью
        bool isFull = true;
        for (int i = 0; i < size; ++i) {
            for (int j = 0; j < size; ++j) {
                if (board[i][j] == '-') {
                    isFull = false;
                    break;
                }
            }
            if (!isFull) break;
        }
        if (isFull) {
            cout << "It's a draw!" << endl;
            gameOver = true;
            break;
        }

        // Смена игрока
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    // Освобождение памяти
    for (int i = 0; i < size; ++i) {
        delete[] board[i];
    }
    delete[] board;



}
