# 西洋棋遊戲 (LLD)

## 問題陳述

設計並實作一個西洋棋遊戲，允許兩名玩家在標準的 8x8 棋盤上對弈，強制執行西洋棋規則，驗證移動，並確定遊戲狀態 (將軍、將死、逼和)。

---

## 需求

- **兩名玩家：** 遊戲在兩名玩家 (白方和黑方) 之間進行。
- **棋盤：** 遊戲使用標準的 8x8 西洋棋盤。
- **棋子：** 所有標準西洋棋子 (國王、皇后、城堡、主教、騎士、兵) 及其移動規則。
- **移動驗證：** 遊戲根據西洋棋規則驗證移動並防止非法移動。
- **回合管理：** 玩家輪流進行回合。
- **遊戲狀態：** 遊戲偵測將軍、將死和逼和。
- **異常處理：** 系統對無效移動拋出異常。
- **可擴展性：** 易於新增功能，例如移動歷史記錄、悔棋或 AI 對手。

---

## 核心實體

- **ChessGame：** 管理遊戲流程、玩家回合和遊戲狀態的主要類別。
- **Board：** 代表 8x8 西洋棋盤並管理棋子位置。
- **Cell：** 代表棋盤上的一個格子，包含列、行和棋子。
- **Player：** 代表具有姓名和顏色的玩家。
- **Color (列舉)：** WHITE (白), BLACK (黑)。
- **Move：** 代表從一個格子到另一個格子的移動。
- **Piece (抽象，在 pieces/ 中)：** 所有西洋棋子的基礎類別。
- **King, Queen, Rook, Bishop, Knight, Pawn (在 pieces/ 中)：** 具有移動邏輯的具體棋子類別。
- **InvalidMoveException：** 對無效移動拋出的異常。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/chessgame-class-diagram.png)

### 1. ChessGame
- **欄位：** Board board, Player[] players, int currentPlayerIndex, boolean isGameOver
- **方法：** start(), makeMove(Move), switchPlayer(), isCheck(), isCheckmate(), isStalemate(), getCurrentPlayer()

### 2. Board
- **欄位：** Cell[][] grid, List<Piece> pieces
- **方法：** getCell(int row, int col), movePiece(Move), isCellOccupied(int row, int col), isCheck(Color), isCheckmate(Color), isStalemate(Color), printBoard()

### 3. Cell
- **欄位：** int row, int col, Piece piece
- **方法：** getPiece(), setPiece(Piece), isEmpty()

### 4. Player
- **欄位：** String name, Color color

### 5. Color (列舉)
- 值：WHITE, BLACK

### 6. Move
- **欄位：** Cell from, Cell to

### 7. Piece (抽象，在 pieces/ 中)
- **欄位：** Color color, Cell position
- **方法：** isValidMove(Board, Move), getPossibleMoves(Board)

### 8. InvalidMoveException
- **拋出：** 當移動不符合西洋棋規則時

---

## 範例用法

```java
Player white = new Player("Alice", Color.WHITE);
Player black = new Player("Bob", Color.BLACK);
ChessGame game = new ChessGame(white, black);
game.start();

Move move = new Move(game.getBoard().getCell(6, 4), game.getBoard().getCell(4, 4)); // e2 到 e4
game.makeMove(move);
```

---

## 演示

請參閱 `ChessGameDemo.java` 以獲取西洋棋遊戲的範例用法和模擬。

---

## 擴展框架

- **新增移動歷史記錄：** 追蹤所有移動以進行悔棋/重做或重播。
- **新增 AI 對手：** 實作電腦玩家。
- **新增 GUI：** 為遊戲建立圖形介面。

---
