# 設計社群網路 (Social Network) 類似 Facebook

## 需求
#### 使用者註冊和驗證：
- 使用者應能夠使用個人資訊 (如姓名、電子郵件和密碼) 建立帳戶。
- 使用者應能夠安全地登入和登出其帳戶。
#### 使用者個人資料：
- 每個使用者應有一個包含其資訊 (如個人資料圖片、簡介和興趣) 的個人資料。
- 使用者應能夠更新其個人資料資訊。
#### 好友連結：
- 使用者應能夠向其他使用者發送好友請求。
- 使用者應能夠接受或拒絕好友請求。
- 使用者應能夠查看其好友列表。
#### 貼文和動態消息：
- 使用者應能夠建立包含文字、圖片或影片的貼文。
- 使用者應能夠查看由其好友的貼文和自己的貼文組成的動態消息。
- 動態消息應按時間倒序排列。
#### 按讚和留言：
- 使用者應能夠對貼文按讚和留言。
- 使用者應能夠查看貼文上的按讚和留言列表。
#### 隱私和安全：
- 使用者應能夠控制其貼文和個人資料資訊的可見性。
- 系統應強制執行安全的存取控制以確保資料隱私。
#### 通知：
- 使用者應收到有關事件 (如好友請求、按讚、留言和提及) 的通知。
- 通知應即時傳遞。
#### 可擴展性和效能：
- 系統應設計為能夠處理大量並發使用者和高流量負載。
- 系統在資源利用方面應具有可擴展性和高效性。

## UML 類別圖

![](../class-diagrams/socialnetworkingservice-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/socialnetworkingservice/) 
#### [Python 實作](../solutions/python/socialnetworkingservice/)
#### [C++ 實作](../solutions/cpp/socialnetworkingservice/)
#### [C# 實作](../solutions/csharp/socialnetworkingservice/)
#### [Go 實作](../solutions/golang/socialnetworkingservice/)

## 類別、介面和列舉
1. **User** 類別代表社群網路系統中的使用者，包含 ID、姓名、電子郵件、密碼、個人資料圖片、簡介、好友列表和貼文列表等屬性。
2. **Post** 類別代表使用者建立的貼文，包含 ID、使用者 ID、內容、圖片 URL、影片 URL、時間戳記、按讚和留言等屬性。
3. **Comment** 類別代表使用者對貼文發表的留言，包含 ID、使用者 ID、貼文 ID、內容和時間戳記等屬性。
4. **Notification** 類別代表為使用者產生的通知，包含 ID、使用者 ID、通知類型、內容和時間戳記等屬性。
5. **NotificationType** 列舉定義了不同類型的通知，例如好友請求、接受好友請求、按讚、留言和提及。
6. **SocialNetworkingService** 類別是管理社群網路系統的主要類別。它遵循單例模式 (Singleton pattern)，以確保服務只有一個實例存在。
7. SocialNetworkingService 類別提供使用者註冊、登入、個人資料更新、好友請求、貼文建立、動態消息產生、按讚、留言和通知的方法。
8. 使用並發資料結構 (如 ConcurrentHashMap 和 CopyOnWriteArrayList) 實現多執行緒，以處理對共享資源的並發存取。
9. **SocialNetworkingDemo** 類別透過註冊使用者、登入、發送好友請求、建立貼文、對貼文按讚、對貼文留言以及檢索動態消息和通知來演示社群網路系統的使用。
