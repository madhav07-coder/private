
# 📘 Enhanced README: Pacman Game - Qt C++ Project

## 🎮 Game Overview
This is a modern recreation of the classic 2D Pacman game using C++ and the Qt framework. It features animated characters, intelligent ghost AI, powerups, scoring, game over, and victory screens. The game uses a modular, object-oriented structure supported by Qt's event system and GUI capabilities.

---

## 🔄 Game Flow Summary
1. **Main Menu**: Player can start the game, view high scores, or quit.
2. **Game Start**: Initializes game entities (Pacman, ghosts, dots, pellets).
3. **Gameplay**:
   - Pacman moves with keyboard input.
   - Ghosts chase using AI movement logic.
   - Eating dots and pellets increases score.
   - Eating pellets temporarily powers up Pacman to eat ghosts.
4. **Victory**: Triggered when all dots are eaten.
5. **Game Over**: Triggered when Pacman loses all lives.
6. **Score Screen**: Displays high scores and allows navigation back to the main menu.

---

## 📂 Code Structure & Function Summaries

### ▶️ `main.cpp`
- Starts the Qt application.
- Creates and shows the `MainWindow`.

### 🏠 `mainwindow.cpp/h`
**Purpose:** Main menu interface.
- `loadUI()`: Initializes UI elements.
- `on_playgame_button_clicked()`: Starts the game.
- `on_highscores_button_clicked()`: Shows high score screen.
- `on_quit_button_clicked()`: Closes the application.

### 🎮 `game.cpp/h`
**Purpose:** Core gameplay engine.
- `loadGameEntities()`: Initializes all game elements (Pacman, ghosts, dots, etc).
- `keyPressEvent()`: Captures movement keys.
- `pause()` / `resume()`: Pauses and resumes gameplay.
- `gameStart()` / `afterGameStart()`: Handles countdown and game initialization.
- `itemEat()`, `dotsAte()`, `pelletAte()`: Logic when Pacman eats.
- `ghostKill()`: Handles logic when ghost is eaten.
- `refreshScore()`: Updates score display.
- `gameFail()` / `checkWinner()`: Handles game end conditions.

### 👻 Ghosts: `blinky.cpp`, `pinky.cpp`, `inky.cpp`, `clyde.cpp`, `ghost.cpp/h`
- Each ghost has:
  - `setTarget()`: AI logic for chasing Pacman.
  - `sendOut()`: Starts ghost movement.
  - `restore()`: Resets ghost after being eaten.
  - Shared behaviors like `chase()`, `die()`, `pause()`, `move()` etc in `ghost.cpp`.

### 🧭 `compass.cpp/h`
**Purpose:** Manages map navigation and movement logic.
- `canMove()`: Validates if a move is possible.
- `initMap()`: Loads maze structure.
- `setLoc()` / `getPlayerPos()`: Tracks player and ghost positions.

### 👤 `pacman.cpp/h`
**Purpose:** Manages Pacman’s behavior.
- `move()`: Handles directional movement.
- `die()`: Called when Pacman is caught.
- `start()`, `pause()`, `restore()`: Lifecycle methods.

### 🟡 `dot.cpp/h` and `pellet.cpp/h`
- `eaten()`: Triggered when Pacman eats item.
- `shine()`: Animates the item.

### 📈 `dashboard.cpp/h`
**Purpose:** Manages score, lives, and high score display.
- `addScore()`, `getScore()`: Score logic.
- `getLifes()` / `setLifes()`: Tracks Pacman’s lives.

### 🎆 `animaterect.cpp/h`
- `fadeIn()` / `fadeOut()`: Handles visual transitions.

### 🏁 `gameover.cpp/h` & `winner.cpp/h`
- `loadUI()`: Loads respective game end screens.
- Button methods to navigate back to menu or exit.

### 🏅 `highscores.cpp/h`
- `addHighScoresToTable()`: Displays saved scores.
- `cleanTable()`: Clears entries.

### 📦 `item.h`, `character.h`
- Abstract classes for items and characters.
- Inherited by Pacman, ghosts, dots, etc.

---

## 🔧 Technologies Used
- **Language:** C++
- **Framework:** Qt (Graphics, GUI, Multimedia)
- **Tools:** Qt Creator / Visual Studio

---

## ✍️ Summary of Function & Class Usage
Every class and method has been built around Qt’s object model and event system. The project follows strong encapsulation:
- **UI logic:** MainWindow, GameOver, Winner
- **Game state:** Game class manages the lifecycle.
- **Entity behavior:** Pacman & Ghosts extend movement logic.
- **Interaction and collision:** Handled via QGraphicsScene and Compass.

---

## 📊 Game Design Insights
- Maze is grid-based with directional logic.
- Ghost AI uses strategies like nearest-path targeting.
- Game loop relies on timers and events for animations and input.
- Modular code separation allows easy debugging and feature addition.

---

For visual walkthrough, see the presentation file `project3_presentation.pdf` and source code in the provided zip.

> 🎓 Built as part of an academic investigation into open source game design.
