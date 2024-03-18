```#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main() {
    srand(time(0)); // инициализация генератора случайных чисел
    int capital = 100;
    int coffee = 1, pizza = 2, tea = 1, pastry = 2;
    char choice;
    
    int visitornumber = 1; // начальный номер посетителя
    int totalvisitors = 0; // общее количество посетителей
    
    while (capital > 0) {
        cout << "Твой капитал: " << capital << endl;
        cout << "Наличие ингредиентов в составе:" << endl;
        cout << "Кофе: " << coffee << endl;
        cout << "Пицца: " << pizza << endl;
        cout << "Чай: " << tea << endl;
        cout << "Пирожок: " << pastry << endl;
        
        int visitorchoice = visitornumber % 4; // выбор продукта у посетителя по порядку
        switch (visitorchoice) {
            case 1:
                cout << "Посетитель №" << visitornumber << " пришел." << endl;
                cout << "Он хочет кофе." << endl;
                cout << "Капитал: " << capital << ". Вы хотите принять заказ? (y/n)" << endl;
                cin >> choice;
                if (choice == 'y' && coffee > 0) {
                    capital += 10;
                    coffee--;
                    cout << "Вы продали кофе! +10$" << endl;
                } else if (choice == 'n') {
                    cout << "Вы отказались принять заказ." << endl;
                } else if (choice == 'y' && coffee == 0) {
                    cout << "О нет, кофе больше нету!" << endl;
                    cout << "Капитал: " << capital << ". Не желаете купить? (y/n)" << endl;
                    cin >> choice;
                    cin.ignore(); // очищаем буфер после ввода choice
                    if (choice == 'y') {
                        capital -= 5; 
                        coffee++;
                        cout << "Вы купили кофе! -5$" << endl;
                    }
                }
                break;
            case 2:
                cout << "Посетитель №" << visitornumber << " пришел." << endl;
                cout << "Он хочет пиццу." << endl;
            
                break;
            case 3:
                cout << "Посетитель №" << visitornumber << " пришел." << endl;
                cout << "Он хочет чай." << endl;
                
                break;
            case 0:
                cout << "Посетитель №" << visitornumber << " пришел." << endl;
                cout << "Он хочет пирожок." << endl;
               
                break;
        }
        
        if (rand() % 100 < 18) { // случайное появление вора с вероятностью 18%
            int theft = rand() % 100;
            if (theft < 20 && capital >= 70) {
                capital -= 70;
                cout << "О нет, вас обворовали! -70$" << endl;
            } else if (theft < 70 && capital >= 50) {
                capital -= 50;
                cout << "О нет, вас обворовали! -50$" << endl;
            } else if (capital >= 20) {
                capital -= 20;
                cout << "О нет, вас обворовали! -20$" << endl;
            } else {
                cout << "Вор не нашел ничего ценного." << endl;
            }
        }
        
        visitornumber++;
        totalvisitors++; 
        
        cout << endl; 
    }
    
    cout << "Игра окончена. Ваш капитал опустился до нуля." << endl;
    cout << "Общее количество посетителей: " << totalvisitors << endl;
    
    
}
```
