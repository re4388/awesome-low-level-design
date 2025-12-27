# 設計大學課程註冊系統

## 需求
1. 課程註冊系統應允許學生註冊課程並查看其已註冊的課程。
2. 每門課程應有課程代碼、名稱、講師和最大註冊人數。
3. 學生應能夠根據課程代碼或名稱搜尋課程。
4. 系統應防止學生註冊已達到最大註冊人數的課程。
5. 系統應處理來自多個學生的並發註冊請求。
6. 系統應確保資料一致性並防止競爭條件。
7. 系統應具有可擴展性，以適應未來的增強功能和新功能。

## UML 類別圖

![](../class-diagrams/courseregistrationsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/courseregistrationsystem/) 
#### [Python 實作](../solutions/python/courseregistrationsystem/)
#### [C++ 實作](../solutions/cpp/courseregistrationsystem/)
#### [C# 實作](../solutions/csharp/courseregistrationsystem/)
#### [Go 實作](../solutions/golang/courseregistrationsystem/)

## 類別、介面和列舉
1. **Student** 類別代表課程註冊系統中的學生，具有 ID、姓名、電子郵件和已註冊課程列表等屬性。
2. **Course** 類別代表系統中提供的課程，具有代碼、名稱、講師、最大容量和已註冊學生人數等屬性。
3. **Registration** 類別代表註冊記錄，將學生與課程關聯並記錄註冊時間戳記。
4. **CourseRegistrationSystem** 類別是管理課程註冊系統的主要類別。它遵循單例模式以確保系統只有一個實例存在。
5. CourseRegistrationSystem 類別提供新增課程和學生、搜尋課程、為學生註冊課程以及檢索學生已註冊課程的方法。
6. 多執行緒是使用並發資料結構 (ConcurrentHashMap 和 CopyOnWriteArrayList) 實作的，以處理對共享資料 (例如課程和註冊) 的並發存取。
7. registerCourse 方法是同步的，以確保當多個學生同時註冊課程時的執行緒安全。
8. notifyObservers 方法是用於通知觀察者 (例如 UI 組件) 有關課程註冊更新的佔位符。
9. **CourseRegistrationDemo** 類別透過建立課程和學生、搜尋課程、為學生註冊課程以及檢索學生已註冊課程來示範課程註冊系統的使用。
