# 設計電梯系統

## 需求
1. 電梯系統應由多部服務多個樓層的電梯組成。
2. 每部電梯應有容量限制且不得超過。
3. 使用者應能夠從任何樓層請求電梯並選擇目的地樓層。
4. 電梯系統應有效地處理使用者請求並優化電梯的移動以最小化等待時間。
5. 系統應根據行進方向和電梯與請求樓層的接近程度來優先處理請求。
6. 電梯應能夠並發處理多個請求並以最佳順序處理它們。
7. 當多個執行緒與電梯互動時，系統應確保執行緒安全並防止競爭條件。

## UML 類別圖

![](../class-diagrams/elevatorsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/elevatorsystem/) 
#### [Python 實作](../solutions/python/elevatorsystem/)
#### [C++ 實作](../solutions/cpp/elevatorsystem/)
#### [C# 實作](../solutions/csharp/elevatorsystem/)
#### [Go 實作](../solutions/golang/elevatorsystem/)

## 類別、介面和列舉
1. **Direction** 列舉代表電梯移動的可能方向 (UP 或 DOWN)。
2. **Request** 類別代表使用者對電梯的請求，包含來源樓層和目的地樓層。
3. **Elevator** 類別代表系統中的單個電梯。它有容量限制並維護請求列表。電梯並發處理請求並根據請求在樓層之間移動。
4. **ElevatorController** 類別管理多部電梯並處理使用者請求。它根據電梯與請求樓層的接近程度找到最佳電梯來服務請求。
5. **ElevatorSystem** 類別是應用程式的入口點，並示範電梯系統的使用。
