# 設計發布-訂閱系統 (Pub-Sub System)

## 需求
1. 發布-訂閱系統應允許發布者將訊息發布到特定主題。
2. 訂閱者應能夠訂閱感興趣的主題並接收發布到這些主題的訊息。
3. 系統應支援多個發布者和訂閱者。
4. 訊息應即時傳遞給主題的所有訂閱者。
5. 系統應處理並發存取並確保執行緒安全。
6. 發布-訂閱系統在訊息傳遞方面應具有可擴展性和高效性。

## UML 類別圖

![](../class-diagrams/pubsubsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/pubsubsystem/)
#### [Python 實作](../solutions/python/pubsubsystem/)
#### [C++ 實作](../solutions/cpp/pubsubsystem/)
#### [C# 實作](../solutions/csharp/pubsubsystem/)
#### [Go 實作](../solutions/golang/pubsubsystem/)

## 類別、介面和列舉
1. **Message** 類別代表可以被發布和訂閱者接收的訊息。它包含訊息內容。
2. **Topic** 類別代表訊息可以發布到的主題。它維護一組訂閱者，並提供新增和移除訂閱者的方法，以及將訊息發布給所有訂閱者的方法。
3. **Subscriber** 介面定義了訂閱者的契約。它宣告了當訂閱者接收到訊息時被呼叫的 onMessage 方法。
4. **PrintSubscriber** 類別是 Subscriber 介面的具體實作。它接收訊息並將其列印到控制台。
5. **Publisher** 類別代表將訊息發布到特定主題的發布者。
6. **PubSubSystem** 類別是管理主題、訂閱者和訊息發布的主要類別。它使用 ConcurrentHashMap 來儲存主題，並使用 ExecutorService 來處理並發訊息發布。
7. **PubSubDemo** 類別透過建立主題、訂閱者和發布者，以及發布訊息來演示發布-訂閱系統的使用。
