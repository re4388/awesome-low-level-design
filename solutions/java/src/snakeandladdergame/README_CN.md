# 蛇梯棋遊戲 (LLD)

## 問題陳述

設計並實作一個蛇梯棋遊戲，允許多名玩家在有蛇和梯子的棋盤上進行遊戲，模擬擲骰子，並確定獲勝者。

---

## 需求

- **多名玩家：** 遊戲支援兩名或更多玩家。
- **棋盤：** 遊戲使用可配置大小的棋盤 (通常為 1 到 100)。
- **蛇和梯子：** 棋盤包含蛇 (使玩家向下移動) 和梯子 (使玩家向上移動)。
- **擲骰子：** 玩家擲骰子以決定他們的移動。
- **回合管理：** 玩家以輪詢方式進行回合。
- **獲勝條件：** 第一個到達最後一個格子的玩家獲勝。
- **輸入驗證：** 遊戲防止無效移動 (例如：移動超過最後一個格子)。
- **可擴展性：** 易於新增功能，例如多個骰子、道具或自訂棋盤大小。

---

## 核心實體

- **SnakeAndLadderGame：** 管理遊戲流程、玩家回合和獲勝條件的主要類別。
- **Board：** 代表遊戲棋盤，包括蛇、梯子和玩家位置。
- **Snake：** 代表具有起點和終點位置的蛇。
- **Ladder：** 代表具有起點和終點位置的梯子。
- **Player：** 代表具有姓名和當前位置的玩家。
- **Dice：** 模擬擲骰子。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/SnakeAndLadderGame-class-diagram.png)

### 1. SnakeAndLadderGame
- **欄位：** Board board, List<Player> players, Dice dice, boolean isGameOver
- **方法：** start(), playTurn(), movePlayer(Player, int steps), checkWin(Player), getCurrentPlayer()

### 2. Board
- **欄位：** int size, List<Snake> snakes, List<Ladder> ladders, Map<Player, Integer> playerPositions
- **方法：** getNextPosition(int current, int roll), addSnake(Snake), addLadder(Ladder), setPlayerPosition(Player, int position), getPlayerPosition(Player)

### 3. Snake
- **欄位：** int start, int end

### 4. Ladder
- **欄位：** int start, int end

### 5. Player
- **欄位：** String name, int position

### 6. Dice
- **方法：** roll()

---

## 範例用法

```java
List<Player> players = List.of(new Player("Alice"), new Player("Bob"));
List<Snake> snakes = List.of(new Snake(14, 7), new Snake(31, 26));
List<Ladder> ladders = List.of(new Ladder(3, 22), new Ladder(5, 8));
Board board = new Board(100, snakes, ladders, players);
Dice dice = new Dice();

SnakeAndLadderGame game = new SnakeAndLadderGame(board, players, dice);
game.start();
```

---

## 演示

請參閱 `SnakeAndLadderDemo.java` 以獲取蛇梯棋遊戲的範例用法和模擬。

---

## 擴展框架

- **新增多個骰子：** 允許每回合擲多個骰子。
- **新增道具：** 引入具有獨特效果的特殊格子。
- **新增自訂棋盤大小：** 支援大於或小於 100 個格子的棋盤。

---
