# 設計圖書館管理系統

## 需求
1. 圖書館管理系統應允許圖書館員管理書籍、會員和借閱活動。
2. 系統應支援從圖書館目錄中新增、更新和移除書籍。
3. 每本書應有詳細資訊，例如標題、作者、ISBN、出版年份和可用狀態。
4. 系統應允許會員借閱和歸還書籍。
5. 每個會員應有詳細資訊，例如姓名、會員 ID、聯絡資訊和借閱歷史記錄。
6. 系統應強制執行借閱規則，例如一次可以借閱的最大書籍數量和借閱期限。
7. 系統應處理對圖書館目錄和會員記錄的並發存取。
8. 系統應具有可延伸性，以適應未來的增強功能和新功能。

## UML 類別圖

![](../class-diagrams/librarymanagementsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/librarymanagementsystem/) 
#### [Python 實作](../solutions/python/librarymanagementsystem/)
#### [C++ 實作](../solutions/cpp/librarymanagementsystem/)
#### [C# 實作](../solutions/csharp/librarymanagementsystem/)
#### [Go 實作](../solutions/golang/librarymanagementsystem/)

## 類別、介面和列舉
1. **Book** 類別代表圖書館目錄中的書籍，具有 ISBN、標題、作者、出版年份和可用狀態等屬性。
2. **Member** 類別代表圖書館會員，具有會員 ID、姓名、聯絡資訊和已借閱書籍列表等屬性。
3. **LibraryManager** 類別是圖書館管理系統的核心，並遵循單例模式以確保圖書館管理員只有一個實例。
4. LibraryManager 類別使用並發資料結構 (ConcurrentHashMap) 來處理對圖書館目錄和會員記錄的並發存取。
5. LibraryManager 類別提供新增和移除書籍、註冊和取消註冊會員、借閱和歸還書籍以及根據關鍵字搜尋書籍的方法。
6. **LibraryManagementSystemDemo** 類別作為應用程式的入口點，並示範圖書館管理系統的使用。
