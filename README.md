# C++-Basketball-Game
#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>
using namespace std;

// Base Class: Player
// ------------------------------
class Player {
protected:
    string name;
    int age;

public:
    Player(string n, int a) : name(n), age(a) {}

    // Virtual function for override
    virtual void displayInfo() const {
        cout << "Name: " << name << ", Age: " << age << endl;
    }
};


// ------------------------------
// Derived Class: BasketPlayer
// ------------------------------
class BasketPlayer : public Player {
private:
    int pointsScored;

public:
    BasketPlayer(string n, int a)
        : Player(n, a), pointsScored(0) {}

    // Score points manually
    void scorePoints(int points) {
        pointsScored += points;
        cout << name << " scored " << points 
             << " points! Total points: " << pointsScored << endl;
    }

    // Shooting using random chance
    void shootBall() {
        int chance = rand() % 100;

        if (chance < 50) {  // 50% chance to make the shot
            cout << name << " shoots... and MAKESSES the shot!" << endl;
            scorePoints(2);
        } else {
            cout << name << " shoots... and MISSES!" << endl;
        }
    }

    // Attempt pass with 20% chance the ball is stolen
    void passBall() {
        int chance = rand() % 100;

        if (chance < 20) {
            cout << name << " attempts a pass... but the opponent STEALS the ball!" << endl;
        } else {
            cout << name << " makes a successful pass." << endl;
        }
    }

    // Override display
    void displayInfo() const override {
        cout << "\n--- Basketball Player Info ---" << endl;
        Player::displayInfo();
        cout << "Points Scored: " << pointsScored << endl;
    }
};


// ------------------------------
// Derived Class: Coach
// ------------------------------
class Coach : public Player {
private:
    string coachingStyle;

public:
    Coach(string n, int a, string style)
        : Player(n, a), coachingStyle(style) {}

    // Coach gives strategy
    void giveStrategy() const {
        cout << name << " (Coach) says: 'Our strategy is " 
             << coachingStyle << "! Stay focused!'" << endl;
    }

    // Override display
    void displayInfo() const override {
        cout << "\n--- Coach Info ---" << endl;
        Player::displayInfo();
        cout << "Coaching Style: " << coachingStyle << endl;
    }
};


// Main Program
// ------------------------------
int main() {
    srand(time(0)); // Initialize randomness

    // Create player and coach
    BasketPlayer player1("Sakib", 24);
    Coach coach1("Coach Williams", 45, "Aggressive Defense");

    // Display initial info
    player1.displayInfo();
    coach1.displayInfo();

    cout << "\n--- Game Simulation ---" << endl;

    // Coach gives strategy
    coach1.giveStrategy();

    // Player actions
    player1.shootBall();
    player1.passBall();
    player1.shootBall();

    // Final info
    player1.displayInfo();

    return 0;
}
