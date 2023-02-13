//Zombie--Dice
//Zombie Dice Juego en C++ 

#include <iostream>
#include <ctime>
#include <cstdlib>

using namespace std;


const int YELLOW_DICE = 3;
const int GREEN_DICE = 5;
const int RED_DICE = 4;
const int NUM_DICE = RED_DICE + YELLOW_DICE + GREEN_DICE;
const int MAX_LIVES = 3;
const int WIN_SCORE = 13;
int color = 3;

enum DiceResult {
  BRAINS = 0,
  SHOT = 1,
  FOOTPRINTS = 2
};

 int rollDice(int color) {
 int result = rand() % 6;
   if (color == 0) {
// Red dice
   if (result == 0 || result == 1) {
  return SHOT;
}  else if (result >= 2 && result <= 4) {
  return FOOTPRINTS;
}  else {
  return BRAINS;
}
}  else if (color == 1) {
// Yellow dice
if (result <= 1) {
return SHOT;
} else if (result >= 2 && result <= 3) {
return FOOTPRINTS;
} else {
return BRAINS;
}
} else {
// Green dice
if (result == 0) {
return SHOT;
} else if (result == 1) {
return FOOTPRINTS;
} else {
return BRAINS;
}
}
}

int main() {
srand(time(0));

int lives = MAX_LIVES;
int score = 0;

while (score < WIN_SCORE && lives > 0) {
int brains = 0;
int shots = 0;
for (int i = 0; i < 3; i++) {
int diceColor = rand() % 3;
int result = rollDice(diceColor);
if (result == BRAINS) {
brains++;
} else if (result == SHOT) {
shots++;
}
}
score += brains;
lives -= shots;
cout << "Brains: " << brains << endl;
cout << "Shots: " << shots << endl;
cout << "Lives: " << lives << endl;
cout << "Score: " << score << endl;
if (lives <= 0) {
cout << "You lost the game." << endl;
break;
}
if (score >= WIN_SCORE) {
cout << "You won the game." << endl;
break;
}
char choice;
cout << "Do you want to roll again? (y/n): ";
cin >> choice;
if (choice != 'y') {
break;
}
}

return 0;
}
