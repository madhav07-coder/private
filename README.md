
# 📘 README: Pacman Game - Qt C++ Project

<h1 align="center">
  <br>
  <a href=""><img src="https://i.pinimg.com/originals/b4/ee/c4/b4eec4d093adbe9d8a3cbb40d024836a.png" width="450"></a>
  <br>
  <br>
</h1>

<h4 align="center">A PacMan clone written in C++ and Qt.</h4>

<p align="center">
  <a href="#motivation">Motivation</a> •
  <a href="#installation">Installation</a> •
  <a href="#how-to-play">How to Play</a> •
  <a href="#contribute">Contribute</a> •
  <a href="#credits">Credits</a> •
</p>


 
 Welcome Window             | Principal Window (PACMAN) | Game Over Window          |
 :-------------------------:|:-------------------------:|:-------------------------:|
 ![](https://res.cloudinary.com/dek4evg4t/image/upload/v1562267062/ezgif.com-video-to-gif.gif)      | ![](https://res.cloudinary.com/dek4evg4t/image/upload/v1562267184/ezgif.com-video-to-gif_1.gif)     |![](https://res.cloudinary.com/dek4evg4t/image/upload/v1562268476/ezgif.com-video-to-gif_2.gif)      |
 
# 📘 Enhanced README: Pacman Game - Qt C++ Project

## 🎮 Game Overview
This is a modern recreation of the classic 2D Pacman game using C++ and the Qt framework. It features animated characters, intelligent ghost AI, powerups, scoring, game over, and victory screens. The game uses a modular, object-oriented structure supported by Qt's event system and GUI capabilities.

---

## 🔄 Game Flow Summary

### 🕹️ Complete Movement and Flow
1. **Startup:**
   - User runs the app; `main.cpp` launches `MainWindow`.
   - `MainWindow` shows menu options: Play, High Scores, Quit.

2. **Start Game:**
   - User clicks "Play" → `on_playgame_button_clicked()` triggers.
   - `Game::gameStart()` initializes all game elements.
   - `Compass::initMap()` loads maze data.
   - `Game::loadGameEntities()` spawns Pacman, ghosts, and food.
   - A 3-second countdown via `Game::countDown()` precedes gameplay.

3. **Active Gameplay:**
   - Keyboard events via `Game::keyPressEvent()` control Pacman.
   - `Pacman::move()` updates position each tick if movement is valid (`Compass::canMove()`).
   - `Ghost::move()` is controlled by `QTimer` and uses `chase()` logic.
   - If Pacman eats dot or pellet → `itemEat()` calls `dotsAte()` or `pelletAte()` → score updates via `Dashboard::addScore()`.
   - Pellet triggers `Compass::setPowerUp()` → ghosts enter frightened mode (`Ghost::changeMode()`).

4. **Collisions:**
   - If Pacman touches ghost:
     - In normal state: `Pacman::die()` triggers life loss, calls `Game::lifesManager()`.
     - In power-up mode: `Game::ghostKill()` is triggered; ghost enters pause/respawn cycle.
   - If Pacman has no lives left → `Game::gameFail()` → `GameOver` screen.

5. **Victory Condition:**
   - After every dot/pellet, `Game::checkWinner()` checks remaining food.
   - If all food collected → `Winner` screen shown via `winner.cpp`.

6. **Ending:**
   - Game ends → High scores saved via `HighScores::addHighScoresToTable()`.
   - User can return to main menu or quit.
1. **Main Menu**: Player can start the game, view high scores, or quit.
2. **Game Start**: Initializes game entities (Pacman, ghosts, dots, pellets).
3. **Gameplay**:
   - Pacman moves with keyboard input.
   - Ghosts chase using AI movement logic (targeting based on Pacman’s direction or distance).
   - Eating dots and pellets increases score.
   - Eating pellets temporarily empowers Pacman to defeat ghosts.
4. **Victory**: Triggered when all dots are eaten.
5. **Game Over**: Triggered when Pacman loses all lives.
6. **Score Screen**: Displays high scores and allows navigation back to the main menu.

---

## 🌍 Game Map
The maze is implemented as a 2D integer array where each value represents a different object:
- `0` - Wall (blocks movement)
- `1` - Path (walkable)
- `2` - Dot (scoreable)
- `3` - Power pellet (grants ghost-eating power)

This grid-based system is used to:
- Validate movement via `Compass::canMove()`
- Position ghosts and Pacman
- Check collisions

---

## 📊 Data Structures Used
- **2D Arrays**: For static game map layout
- **Classes/Inheritances**: Abstract classes like `Character` & `Item`, inherited by `Pacman`, `Ghost`, etc.
- **QTimer**: Manages animation, movement timing, and countdowns
- **QEventLoop**: Handles asynchronous waits (e.g., for death animation)
- **File I/O**: Reads/writes high scores
- **QVectors/Lists**: Dynamic storage of active game items or ghost objects

---

## 🧠 Full Codebase Reference with Functional Descriptions

### 📄 `main.cpp`
- Starts the application using `QApplication`
- Shows the `MainWindow` which acts as the main menu

### 📄 `mainwindow.cpp/h`
- `on_playgame_button_clicked()` – Starts the main game loop
- `on_highscores_button_clicked()` – Loads the leaderboard screen
- `on_quit_button_clicked()` – Exits application

### 📄 `game.cpp/h`
**Main engine of the game**
- `loadGameEntities()` – Spawns Pacman, ghosts, and food items on map
- `keyPressEvent()` – Captures keyboard input and sets direction
- `itemEat()` – Checks for item collision and score increment
- `dotsAte()` / `pelletAte()` – Tracks score from dot or pellet
- `gameStart()` / `afterGameStart()` – Countdown then unpauses game
- `pause()` / `resume()` – Pauses or resumes ghost and Pacman timers
- `ghostKill()` – Triggered when Pacman eats a ghost in power mode
- `refreshScore()` – Updates UI element with current score
- `checkWinner()` – If no dots remain, player wins
- `gameFail()` – If Pacman runs out of lives

### 📄 `compass.cpp/h`
- `initMap()` – Creates the static grid layout of walls, dots, and pellets
- `canMove()` – Returns boolean if movement in a direction is valid
- `setLoc()` / `getPlayerLoc()` – Updates and returns Pacman’s location on map
- `setPowerUp()` – Activates ghost vulnerability

### 📄 `dashboard.cpp/h`
- Manages score, lives, and high score tracking
- `addScore()` – Adds to current game score
- `reset()` – Resets score/lives on new game
- `getScore()` / `getLifes()` / `setLifes()` – Accessors and mutators for UI

### 📄 `ghost.cpp/h` (Shared by all ghosts)
- `move()` – Regular movement timer callback
- `setDirection()` – Updates travel direction
- `chase()` – AI logic to move toward Pacman
- `die()` – Called when ghost is eaten; initiates pause, respawn
- `changeMode()` – Switches from normal to frightened mode

### 📄 `blinky.cpp`, `inky.cpp`, `pinky.cpp`, `clyde.cpp`
- Each defines unique `setTarget()` logic:
  - **Blinky** chases Pacman directly
  - **Pinky** aims a few tiles ahead
  - **Inky** uses vector math involving Blinky
  - **Clyde** alternates between scatter and chase based on distance

### 📄 `pacman.cpp/h`
- `move()` – Movement based on current direction
- `die()` – Reduces life and triggers animation
- `start()` / `pause()` / `restore()` – Lifecycle management

### 📄 `dot.cpp/h` and `pellet.cpp/h`
- `eaten()` – Marks item as consumed and triggers shine

### 📄 `animaterect.cpp/h`
- `fadeIn()` / `fadeOut()` – Handles scene transitions

### 📄 `gameover.cpp/h`, `winner.cpp/h`
- Shows modal when game ends
- `on_mainMenu_button_clicked()` – Returns to menu
- `on_exit_button_clicked()` – Closes game

### 📄 `highscores.cpp/h`
- Loads and displays leaderboard
- `addHighScoresToTable()` – Inserts score
- `cleanTable()` – Clears scoreboard entries

### 📄 `character.h`, `item.h`
- Abstract classes providing base structure for all characters (ghosts, Pacman) and game items (dots, pellets)

---

## 🧩 Game Logic Explained
- **Collision Detection**: Performed using `QGraphicsItem::collidesWithItem()` in `itemEat()` and `ghostKill()`
- **Power-Ups**: Eating a pellet calls `setPowerUp()` from `Compass`, triggering vulnerable state in all ghosts
- **Chase & Scatter AI**: Each ghost runs its `chase()` and `setTarget()` logic every tick using a timer
- **Death Animation**: Triggers `die()` in Pacman or Ghost, launches event loop, then restarts or ends game
- **Score Keeping**: Incrementally updated in `dashboard` using `addScore()`
- **Victory Check**: After every dot/pellet, `checkWinner()` runs to detect board clearance

---

## 🔧 Technologies Used
- **Language:** C++
- **Framework:** Qt (Graphics, GUI, Multimedia)
- **Tools:** Qt Creator / Visual Studio

---

## ✍️ Summary
This project is a faithful, animated recreation of the classic Pacman using C++ and Qt. It demonstrates object-oriented programming, event-driven logic, and basic game development principles including AI, graphics, state machines, and file handling.

---

For visual walkthrough, see the presentation file `project3_presentation.pdf` and source code in the provided zip.

> 🎓 Built as part of an academic investigation into open source game design.


