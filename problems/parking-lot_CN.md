# 設計停車場系統 (Parking Lot System)

## 需求
1. 停車場應有多個樓層，每個樓層有一定數量的停車位。
2. 停車場應支援不同類型的車輛，例如汽車、摩托車和卡車。
3. 每個停車位應能容納特定類型的車輛。
4. 系統應在車輛進入時分配停車位，並在車輛離開時釋放停車位。
5. 系統應追蹤停車位的可用性，並向客戶提供即時資訊。
6. 系統應處理多個出入口，並支援並發存取。

## UML 類別圖

![](../class-diagrams/parkinglot-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/parkinglot/) 
#### [Python 實作](../solutions/python/parkinglot/)
#### [C++ 實作](../solutions/cpp/parkinglot/)
#### [C# 實作](../solutions/csharp/parkinglot/)
#### [Go 實作](../solutions/golang/parkinglot/)
#### [TypeScript 實作](../solutions/typescript/src/ParkingLot/)

## 類別、介面和列舉
1. **ParkingLot** 類別遵循單例模式 (Singleton pattern)，以確保停車場只有一個實例存在。它維護樓層列表，並提供停車和取車的方法。
2. **Level** 類別代表停車場中的一個樓層，包含停車位列表。它處理該樓層內車輛的停車和取車。
3. **ParkingSpot** 類別代表單個停車位，並追蹤可用性和停放的車輛。
4. **Vehicle** 類別是不同類型車輛的抽象基礎類別。它由 Car、Motorcycle 和 Truck 類別繼承。
5. **VehicleType** 列舉定義了停車場支援的不同車輛類型。
6. 透過在關鍵區段上使用 synchronized 關鍵字來實現多執行緒，以確保執行緒安全。
7. **Main** 類別演示了停車場系統的使用。

## 使用的設計模式：
1. 單例模式 (Singleton Pattern)：確保 ParkingLot 類別只有一個實例。
2. 工廠模式 (Factory Pattern) (可選擴展)：可用於根據輸入建立車輛。
3. 觀察者模式 (Observer Pattern) (可選擴展)：可通知客戶有關可用停車位的資訊。
