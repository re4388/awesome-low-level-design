# 設計日誌框架

## 需求
1. 日誌框架應支援不同的日誌級別，例如 DEBUG、INFO、WARNING、ERROR 和 FATAL。
2. 它應允許記錄帶有時間戳記、日誌級別和訊息內容的訊息。
3. 框架應支援多個輸出目的地，例如控制台、檔案和資料庫。
4. 它應提供配置機制來設定日誌級別和輸出目的地。
5. 日誌框架應是執行緒安全的，以處理來自多個執行緒的並發日誌記錄。
6. 它應具有可延伸性，以適應未來的新日誌級別和輸出目的地。

## UML 類別圖

![](../class-diagrams/loggingframework-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/loggingframework/) 
#### [Python 實作](../solutions/python/loggingframework/)
#### [C++ 實作](../solutions/cpp/loggingframework/)
#### [C# 實作](../solutions/csharp/loggingframework/)
#### [Go 實作](../solutions/golang/loggingframework/)
#### [TypeScript 實作](../solutions/typescript/src/LoggingFramework/)

## 類別、介面和列舉
1. **LogLevel** 列舉定義了日誌框架支援的不同日誌級別。
2. **LogMessage** 類別代表一條日誌訊息，包含時間戳記、日誌級別和訊息內容。
3. **LogAppender** 介面定義了將日誌訊息附加到不同輸出目的地的契約。
4. **ConsoleAppender**、**FileAppender** 和 **DatabaseAppender** 類別是 LogAppender 介面的具體實作，分別支援記錄到控制台、檔案和資料庫。
5. **LoggerConfig** 類別保存記錄器的配置設定，包括日誌級別和選定的日誌附加器 (appender)。
6. **Logger** 類別是一個單例，提供主要的日誌記錄功能。它允許設定配置、記錄不同級別的訊息，並為每個日誌級別提供便利方法。
7. **LoggingExample** 類別示範了日誌框架的使用，展示了不同的日誌級別、更改配置以及從多個執行緒進行日誌記錄。
