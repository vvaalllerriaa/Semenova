# Semenova Valeriia 
Мій проєкт представлений у вигляді гри "Хрестики/Нулики".

Правила гри:
У грі бере участь двоє гравців, один з яких відповідає за знак хрестика, а інший-за знак нулика. На кожному ході гравці мають ставити O чи X на ґратці розміром 3 на 3. Гравець, який першим поставив три однакових знаки в горизонтальному, вертикальному чи діагональному ряду, виграє партію.

Вказівки щодо користування зібраною програмою:
Починаючи працювати, програма робить користувачу запит на номер рядка та колонки, в яку гравець хоче поставити свій знак. Нумерація починається з нуля. Спочатку потрібно вказати рядок, потім-колонку. 

Відео з використанням гри:
https://youtu.be/B5Tu99ZNlgA

Код гри:

#include <iostream>
using namespace std;
void winner(int player) {
    if (player % 2 == 0) {
        cout << "Player 2 wins!" << endl;  // Якщо player % 2 == 0, то виграє гравець 2
    } else {
        cout << "Player 1 wins!" << endl;  // Якщо player % 2 == 1, то виграє гравець 1
    }
}
int main() {
    char mass[3][3] = { {' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '} };
    int player = 1;

    while(true){
        int a, b;
        cout << "Enter the field (row and column): ";
        cin >> a >> b;

        // Перевірка границь масива
        if (a < 0 || a >= 3 || b < 0 || b >= 3) {
            cout << "Invalid input. Please enter values between 0 and 2." << endl;
            continue;
        }

        // Перевірка, чи порле пусте
        if (mass[a][b] != ' ') {
            cout << "Field already occupied. Please choose another one." << endl;
            continue;
        }

        // Встановлення мітки гравця
        if (player % 2 == 0) {
            mass[a][b] = 'X';
        } else {
            mass[a][b] = 'O';
        }

        // Відображення поля
        for(int i = 0; i < 3; i++) {
            cout << '|';
            for(int j = 0; j < 3; j++) {
                cout << mass[i][j] << '|';
            }
            cout << endl;
        }

        // Перевиріка, чи немає перемоги
        for (int i = 0; i < 3; i++) {
            if ((mass[i][0] == mass[i][1] && mass[i][1] == mass[i][2] && mass[i][0] != ' ') ||
                (mass[0][i] == mass[1][i] && mass[1][i] == mass[2][i] && mass[0][i] != ' ')) {
                winner(player);
                return 0;
            }
        }
        if ((mass[0][0] == mass[1][1] && mass[1][1] == mass[2][2] && mass[0][0] != ' ') ||
            (mass[0][2] == mass[1][1] && mass[1][1] == mass[2][0] && mass[0][2] != ' ')) {
            winner(player);
            return 0;
        }

        // Перевірка, чи немає нічиєї
        bool draw = true;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (mass[i][j] == ' ') {
                    draw = false;
                    break;
                }
            }
        }
        if (draw) {
            cout << "Draw!" << endl;
            return 0;
        }

        // Перехід коду до наступного ігрока
        player++;
    }

    return 0;
}
