# 設計井字遊戲 (Tic Tac Toe Game)

## 需求
1. 井字遊戲應在 3x3 的網格上進行。
2. 兩名玩家輪流在網格上標記他們的符號 (X 或 O)。
3. 第一個將三個符號連成一線 (水平、垂直或對角線) 的玩家贏得遊戲。
4. 如果網格上的所有格子都填滿且沒有玩家獲勝，則遊戲以平局結束。
5. 遊戲應有一個使用者介面來顯示網格並允許玩家進行移動。
6. 遊戲應處理玩家的回合並驗證移動以確保它們是合法的。
7. 遊戲應在結束時偵測並宣佈獲勝者或平局。

## UML 類別圖

![](../class-diagrams/tictactoe-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/tictactoe/) 
#### [Python 實作](../solutions/python/tictactoe/)
#### [C++ 實作](../solutions/cpp/tictactoe/)
#### [C# 實作](../solutions/csharp/tictactoe/)
#### [Go 實作](../solutions/golang/tictactoe/)

## 類別、介面和列舉
1. **Player** 類別代表遊戲中的玩家，具有姓名和符號 (X 或 O)。
2. **Board** 類別代表遊戲棋盤，是一個 3x3 的網格。它提供進行移動、檢查獲勝者和檢查棋盤是否已滿的方法。
3. **Game** 類別管理遊戲流程和玩家互動。它處理玩家回合、驗證移動並確定獲勝者或平局。
4. **TicTacToe** 類別是應用程式的進入點，並建立玩家和遊戲的實例。
