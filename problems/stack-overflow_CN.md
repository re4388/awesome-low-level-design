# 設計 Stack Overflow

## 需求
1. 使用者可以發布問題、回答問題，並對問題和回答發表評論。
2. 使用者可以對問題和回答進行投票。
3. 問題應有關聯的標籤。
4. 使用者可以根據關鍵字、標籤或使用者個人資料搜尋問題。
5. 系統應根據使用者的活動和貢獻品質為使用者分配聲譽分數。
6. 系統應處理並發存取並確保資料一致性。

## UML 類別圖

![](../class-diagrams/stackoverflow-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/stackoverflow/) 
#### [Python 實作](../solutions/python/stackoverflow/)
#### [C++ 實作](../solutions/cpp/stackoverflow/)
#### [C# 實作](../solutions/csharp/stackoverflow/)
#### [Go 實作](../solutions/golang/stackoverflow/)
#### [TypeScript 實作](../solutions/typescript/src/StackOverflow/)

## 類別、介面和列舉
1. **User** 類別代表 Stack Overflow 系統的使用者，具有 id、使用者名稱、電子郵件和聲譽等屬性。
2. **Question** 類別代表使用者發布的問題，具有 id、標題、內容、作者、回答、評論、標籤、投票和建立日期等屬性。
3. **Answer** 類別代表對問題的回答，具有 id、內容、作者、關聯問題、評論、投票和建立日期等屬性。
4. **Comment** 類別代表對問題或回答的評論，具有 id、內容、作者和建立日期等屬性。
5. **Tag** 類別代表與問題關聯的標籤，具有 id 和名稱等屬性。
6. **Vote** 類別代表與問題/回答關聯的投票。
7. **StackOverflow** 類別是管理 Stack Overflow 系統的主要類別。它提供建立使用者、發布問題、回答和評論、對問題和回答投票、搜尋問題以及按標籤和使用者檢索問題的方法。
8. **StackOverflowDemo** 類別透過建立使用者、發布問題和回答、投票、搜尋問題以及按標籤和使用者檢索問題來演示 Stack Overflow 系統的使用。
