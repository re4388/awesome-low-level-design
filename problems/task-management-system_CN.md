# 設計任務管理系統 (Task Management System)

## 需求
1. 任務管理系統應允許使用者建立、更新和刪除任務。
2. 每個任務應有標題、描述、截止日期、優先順序和狀態 (例如：待處理、進行中、已完成)。
3. 使用者應能夠將任務指派給其他使用者並設定任務提醒。
4. 系統應支援根據各種條件 (例如：優先順序、截止日期、指派的使用者) 搜尋和過濾任務。
5. 使用者應能夠將任務標記為已完成並查看其任務歷史記錄。
6. 系統應處理對任務的並發存取並確保資料一致性。
7. 系統應具有可擴展性，以適應未來的增強功能和新功能。

## UML 類別圖

![](../class-diagrams/taskmanagementsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/taskmanagementsystem/) 
#### [Python 實作](../solutions/python/taskmanagementsystem/)
#### [C++ 實作](../solutions/cpp/taskmanagementsystem/)
#### [C# 實作](../solutions/csharp/taskmanagementsystem/)
#### [Go 實作](../solutions/golang/taskmanagementsystem/)
#### [TypeScript 實作](../solutions/typescript/src/TaskManagement/)

## 類別、介面和列舉
1. **User** 類別代表任務管理系統中的使用者，具有 id、姓名和電子郵件等屬性。
2. **TaskStatus** 列舉定義了任務的可能狀態，例如待處理、進行中和已完成。
3. **Task** 類別代表系統中的任務，具有 id、標題、描述、截止日期、優先順序、狀態和指派的使用者等屬性。
4. **TaskManager** 類別是任務管理系統的核心，並遵循單例模式 (Singleton pattern) 以確保任務管理器只有一個實例。
5. TaskManager 類別使用並發資料結構 (ConcurrentHashMap 和 CopyOnWriteArrayList) 來處理對任務的並發存取並確保執行緒安全。
6. TaskManager 類別提供建立、更新、刪除、搜尋和過濾任務的方法，以及將任務標記為已完成和檢索使用者任務歷史記錄的方法。
7. **TaskManagementSystem** 類別作為應用程式的進入點，並演示任務管理系統的使用。
