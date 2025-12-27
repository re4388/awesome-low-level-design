# 設計西洋棋遊戲

## 需求
1. 西洋棋遊戲應遵循西洋棋的標準規則。
2. 遊戲應支援兩名玩家，每名玩家控制自己的一組棋子。
3. 棋盤應表示為 8x8 的網格，黑白方格交替。
4. 每位玩家應有 16 個棋子：1 個國王、1 個皇后、2 個城堡、2 個主教、2 個騎士和 8 個兵。
5. 遊戲應驗證每個棋子的合法移動並防止非法移動。
6. 遊戲應偵測將死 (checkmate) 和僵局 (stalemate) 情況。
7. 遊戲應處理玩家回合，並允許玩家輪流移動。
8. 遊戲應提供使用者介面供玩家與遊戲互動。

## UML 類別圖

![](../class-diagrams/chessgame-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/chessgame/) 
#### [Python 實作](../solutions/python/chessgame/)
#### [C++ 實作](../solutions/cpp/chessgame/)
#### [C# 實作](../solutions/csharp/chessgame/)
#### [Go 實作](../solutions/golang/chessgame/)

## 類別、介面和列舉
1. **Piece** 類別是代表西洋棋棋子的抽象基礎類別。它包含共同屬性，如顏色、列和行，並宣告一個抽象方法 canMove 供每個特定棋子類別實作。
2. **King**、**Queen**、**Rook**、**Bishop**、**Knight** 和 **Pawn** 類別繼承 Piece 類別，並在 canMove 方法中實作各自的移動邏輯。
3. **Board** 類別代表棋盤並管理棋子的放置。它提供取得和設定棋盤上棋子、檢查移動有效性以及判斷將死和僵局情況的方法。
4. **Player** 類別代表遊戲中的玩家，並具有在棋盤上進行移動的方法。
5. **Move** 類別代表玩家所做的移動，包含被移動的棋子和目的地座標。
6. **Game** 類別協調整個遊戲流程。它初始化棋盤、處理玩家回合並判斷遊戲結果。
7. **ChessGame** 類別是應用程式的入口點並開始遊戲。
