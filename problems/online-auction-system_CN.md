# 設計線上拍賣系統
在本文中，我們將深入探討使用 Java 進行線上拍賣系統的物件導向設計和實作。

該系統允許建立和管理拍賣、使用者參與投標以及處理交易。

## 需求
1. 線上拍賣系統應允許使用者註冊並登入其帳戶。
2. 使用者應能夠建立新的拍賣列表，其中包含物品名稱、描述、起標價和拍賣持續時間等詳細資訊。
3. 使用者應能夠根據各種條件 (例如物品名稱、類別、價格範圍) 瀏覽和搜尋拍賣列表。
4. 使用者應能夠對活躍的拍賣列表進行投標。
5. 系統應自動更新目前的最高出價並相應地通知投標人。
6. 當達到指定的持續時間時，拍賣應結束，並宣布出價最高者為獲勝者。
7. 系統應處理對拍賣列表的並發存取並確保資料一致性。
8. 系統應具有可延伸性，以適應未來的增強功能和新功能。

## UML 類別圖

![](../class-diagrams/onlineauctionsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/onlineauctionsystem/) 
#### [Python 實作](../solutions/python/onlineauctionsystem/)
#### [C++ 實作](../solutions/cpp/onlineauctionsystem/)
#### [C# 實作](../solutions/csharp/onlineauctionsystem/)
#### [Go 實作](../solutions/golang/onlineauctionsystem/)

## 類別、介面和列舉
1. **User** 類別代表線上拍賣系統中的使用者，具有 id、使用者名稱和電子郵件等屬性。
2. **AuctionStatus** 列舉定義了拍賣列表的可能狀態，例如活躍和已關閉。
3. **AuctionListing** 類別代表系統中的拍賣列表，具有 id、物品名稱、描述、起標價、持續時間、賣家、目前最高出價和出價列表等屬性。
4. **Bid** 類別代表使用者對拍賣列表的出價，具有 id、投標人、金額和時間戳記等屬性。
5. **AuctionSystem** 類別是線上拍賣系統的核心，並遵循單例模式以確保拍賣系統只有一個實例。
6. AuctionSystem 類別使用並發資料結構 (ConcurrentHashMap 和 CopyOnWriteArrayList) 來處理對拍賣列表的並發存取並確保執行緒安全。
7. AuctionSystem 類別提供註冊使用者、建立拍賣列表、搜尋拍賣列表和投標的方法。
8. **AuctionSystemDemo** 類別作為應用程式的入口點，並示範線上拍賣系統的使用。
