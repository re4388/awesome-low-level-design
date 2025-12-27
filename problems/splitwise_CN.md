# 設計 Splitwise

## 需求
1. 系統應允許使用者建立帳戶並管理其個人資料資訊。
2. 使用者應能夠建立群組並將其他使用者新增至群組。
3. 使用者應能夠在群組內新增費用，指定金額、描述和參與者。
4. 系統應根據參與者的份額自動在參與者之間分攤費用。
5. 使用者應能夠查看他們與其他使用者的個人餘額並結清餘額。
6. 系統應支援不同的分攤方式，例如均分、百分比分攤和精確金額。
7. 使用者應能夠查看其交易記錄和群組費用。
8. 系統應處理並發交易並確保資料一致性。

## UML 類別圖

![](../class-diagrams/splitwise-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/splitwise/)
#### [Python 實作](../solutions/python/splitwise/)
#### [C++ 實作](../solutions/cpp/splitwise/)
#### [C# 實作](../solutions/csharp/splitwise/)
#### [Go 實作](../solutions/golang/splitwise/)

## 類別、介面和列舉
1. **User** 類別代表 Splitwise 系統中的使用者，具有 ID、姓名、電子郵件以及用於儲存與其他使用者餘額的 map 等屬性。
2. **Group** 類別代表 Splitwise 中的群組，包含成員使用者列表和費用列表。
3. **Expense** 類別代表群組內的費用，具有 ID、金額、描述、付款使用者和分攤列表等屬性。
4. **Split** 類別是代表費用分攤的抽象類別。它由 EqualSplit、PercentSplit 和 ExactSplit 類別繼承，以處理不同的分攤方式。
5. **Transaction** 類別代表兩個使用者之間的交易，具有 ID、發送者、接收者和金額等屬性。
6. **SplitwiseService** 類別是管理 Splitwise 系統的主要類別。它遵循單例模式 (Singleton pattern)，以確保服務只有一個實例存在。
7. SplitwiseService 類別提供新增使用者、群組和費用、分攤費用、更新餘額、結清餘額和建立交易的方法。
8. 使用並發資料結構 (如 ConcurrentHashMap 和 CopyOnWriteArrayList) 實現多執行緒，以處理對共享資源的並發存取。
9. **SplitwiseDemo** 類別透過建立使用者、群組、新增費用、結清餘額和列印使用者餘額來演示 Splitwise 系統的使用。
