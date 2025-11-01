#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

const int MAX_PLAYERS = 2;
const int MAX_TRACK = 50;

// Function to roll a dice (1 to 3)
int rollDice() {
    return rand() % 3 + 1;
}

// Function to display the race track
void displayTrack(int positions[], int trackLength, int playerIDs[]) {
    for (int i = 0; i < MAX_PLAYERS; i++) {
        cout << "Player " << playerIDs[i] << ": ";
        for (int j = 0; j <= trackLength; j++) {
            if (j == positions[i])
                cout << "[" << playerIDs[i] << "]";
            else if (j == trackLength)
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

    int trackLength;
    int positions[MAX_PLAYERS] = {0};
    int playerIDs[MAX_PLAYERS];

    cout << "=== Welcome to Grid Racer ===\n";

    // Input: track length
    do {
        cout << "Enter track length (10 to " << MAX_TRACK << "): ";
        cin >> trackLength;
    } while (trackLength < 10 || trackLength > MAX_TRACK);

    // Input: player names (as numbers)
    for (int i = 0; i < MAX_PLAYERS; i++) {
        cout << "Enter ID number for Player " << i + 1 << ": ";
        cin >> playerIDs[i];
    }

    int turn = 1;
    bool gameOver = false;

    while (!gameOver) {
        cout << "\n--- Turn " << turn << " ---\n";

        for (int i = 0; i < MAX_PLAYERS; i++) {
            cout << "Player " << playerIDs[i] << ", press any key then Enter to roll the dice: ";
            char temp;
            cin >> temp;

            int move = rollDice();
            positions[i] += move;
            if (positions[i] > trackLength)
                positions[i] = trackLength;

            cout << "Player " << playerIDs[i] << " moves " << move << " steps.\n";
        }

        displayTrack(positions, trackLength, playerIDs);

        for (int i = 0; i < MAX_PLAYERS; i++) {
            if (positions[i] >= trackLength) {
                cout << "\n*** Player " << playerIDs[i] << " wins the race! ***\n";
                gameOver = true;
            }
        }

        turn++;
    }

    cout << "\nThanks for playing Grid Racer!\n";
    return 0;
}
