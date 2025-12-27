# 井字遊戲 (LLD)

## 問題陳述

設計並實作一個井字遊戲，允許兩名玩家在 NxN 的棋盤上進行遊戲，輪流進行，並確定獲勝者或平局。

---

## 需求

- **兩名玩家：** 遊戲在兩名玩家之間進行。
- **棋盤：** 遊戲使用 NxN 的棋盤。
- **回合：** 玩家輪流在棋盤上放置他們的符號 (X 或 O)。
- **獲勝條件：** 遊戲偵測玩家何時獲勝 (一行、一列或對角線連成一線)。
- **平局條件：** 遊戲偵測棋盤何時已滿且遊戲為平局。
- **輸入驗證：** 遊戲防止移動到已被佔用的格子。
- **可擴展性：** 易於更改棋盤大小或新增功能。

---

## 核心實體

- **Game：** 管理遊戲流程、玩家回合和遊戲狀態。
- **Board：** 代表 NxN 網格並提供更新和檢查棋盤的方法。
- **Cell：** 代表棋盤上的一個格子。
- **Player：** 代表具有姓名和符號的玩家。
- **Symbol：** X 和 O 的列舉。
- **GameStatus：** IN_PROGRESS, DRAW, WIN 的列舉。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/tictactoe-class-diagram.png)

### 1. Game
- **欄位：** Board board, Player[] players, int currentPlayerIndex, GameStatus status
- **方法：** play(), makeMove(int row, int col), checkWin(), checkDraw(), switchPlayer(), getCurrentPlayer()

### 2. Board
- **欄位：** Cell[][] grid, int size
- **方法：** isCellEmpty(int row, int col), setCell(int row, int col, Symbol), printBoard(), isFull(), checkWin(Symbol)

### 3. Cell
- **欄位：** int row, int col, Symbol symbol
- **方法：** getSymbol(), setSymbol(Symbol)

### 4. Player
- **欄位：** String name, Symbol symbol

### 5. Symbol (列舉)
- 值：X, O

### 6. GameStatus (列舉)
- 值：IN_PROGRESS, DRAW, WIN

---

## 範例用法

```java
Player p1 = new Player("Alice", Symbol.X);
Player p2 = new Player("Bob", Symbol.O);
Game game = new Game(p1, p2);
game.play();
```

---

## 演示

請參閱 `TicTacToeDemo.java` 以獲取井字遊戲的範例用法和模擬。

---

## 擴展設計

- **更改棋盤大小：** 更新 `Board` 類別以支援不同的大小。
- **新增 AI 玩家：** 為單人模式實作電腦玩家。
- **新增 GUI：** 為遊戲建立圖形介面。

---
