# 設計交通號誌控制系統 (Traffic Signal Control System)

## 需求
1. 交通號誌系統應控制多條道路交叉口的交通流量。
2. 系統應支援不同類型的號誌，例如紅燈、黃燈和綠燈。
3. 每個號誌的持續時間應可配置，並可根據交通狀況進行調整。
4. 系統應平滑處理號誌之間的轉換，確保安全高效的交通流量。
5. 系統應能夠偵測並處理緊急情況，例如救護車或消防車接近交叉口。
6. 系統應具有可擴展性和可延伸性，以支援額外的特性和功能。

## UML 類別圖

![](../class-diagrams/trafficsignalsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/trafficsignalcontrolsystem/)
#### [Python 實作](../solutions/python/trafficsignalsystem/)
#### [C++ 實作](../solutions/cpp/trafficsignalsystem/)
#### [C# 實作](../solutions/csharp/trafficsignalsystem/)
#### [Go 實作](../solutions/golang/trafficsignalsystem/)
#### [TypeScript 實作](../solutions/typescript/src/TrafficSignalSystem/) 

## 類別、介面和列舉
1. **Signal** 列舉代表交通號誌的不同狀態：紅燈、黃燈和綠燈。
2. **Road** 類別代表交通號誌系統中的道路，具有 ID、名稱和關聯的交通號誌等屬性。
3. **TrafficLight** 類別代表交通號誌，具有 ID、當前號誌和每個號誌狀態的持續時間等屬性。它提供更改號誌和通知觀察者 (例如道路) 有關號誌變更的方法。
4. **TrafficController** 類別作為交通號誌系統的中央控制器。它遵循單例模式 (Singleton pattern) 以確保控制器只有一個實例。它管理道路及其關聯的交通號誌，啟動交通控制流程，並處理緊急情況。
5. **TrafficSignalSystemDemo** 類別是應用程式的主要進入點。它透過建立道路、交通號誌、將交通號誌分配給道路以及啟動交通控制流程來演示交通號誌系統的使用。
