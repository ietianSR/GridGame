#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

const int TRACK_LENGTH = 20;
const int NUM_PLAYERS = 2;

// Function to roll a dice (1 to 3)
int rollDice() {
    return rand() % 3 + 1;
}

// Function to display the race track
void displayTrack(int positions[]) {
    for (int i = 0; i < NUM_PLAYERS; i++) {
        cout << "Player " << i + 1 << ": ";
        for (int j = 0; j <= TRACK_LENGTH; j++) {
            if (j == positions[i])
                cout << "[" << i + 1 << "]";
            else if (j == TRACK_LENGTH)
                cout << "|F|";
            else
                cout << " . ";
        }
        cout << "\n";
    }
    cout << "----------------------------------------\n";
}

int main() {
    srand(time(0));
    int positions[NUM_PLAYERS] = {0};
    int turn = 1;
    bool gameOver = false;

    cout << "=== Welcome to Grid Racer ===\n";
    cout << "First to reach the finish line wins!\n";

    while (!gameOver) {
        cout << "\n--- Turn " << turn << " ---\n";

        for (int i = 0; i < NUM_PLAYERS; i++) {
            cout << "Player " << i + 1 << ", press any key then Enter to roll the dice: ";
            char temp;
            cin >> temp;

            int move = rollDice();
            positions[i] += move;
            if (positions[i] > TRACK_LENGTH)
                positions[i] = TRACK_LENGTH;

            cout << "Player " << i + 1 << " moves " << move << " steps.\n";
        }

        displayTrack(positions);

        for (int i = 0; i < NUM_PLAYERS; i++) {
            if (positions[i] >= TRACK_LENGTH) {
                cout << "\n*** Player " << i + 1 << " wins the race! ***\n";
                gameOver = true;
            }
        }

        turn++;
    }

    cout << "\nThanks for playing Grid Racer!\n";
    return 0;
}
