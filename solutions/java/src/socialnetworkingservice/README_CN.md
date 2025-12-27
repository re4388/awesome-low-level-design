外觀模式 (Facade Pattern)：SocialNetworkFacade 是客戶端的主要進入點。它為服務和儲存庫的複雜子系統提供了一個簡單、統一的介面 (createPost, addFriend, getNewsFeed)。

觀察者模式 (Observer Pattern)：PostService 充當主體 (Subject)。當使用者建立貼文時，它會通知所有已註冊的觀察者 (Observers) (如 NewsFeedNotifier)。這將發布動作與更新動態消息的後果解耦。

策略模式 (Strategy Pattern)：NewsFeedService 使用 NewsFeedGenerationStrategy 來產生使用者的動態消息。預設為 ChronologicalStrategy (按時間順序)，但這可以輕鬆替換為更複雜的演算法。

組合模式 (Composite Pattern)：為了對評論和回覆進行建模，使用了 Commentable 介面。Post 和 Comment 都實作了此介面，允許它們被統一對待。評論可以新增到貼文或其他評論中，形成樹狀結構。

單例模式 (Singleton Pattern)：Repository 類別被實作為單例，以為此模擬提供全域的記憶體內資料儲存。

儲存庫模式 (Repository Pattern)：此模式用於抽象資料存取層。服務與 UserRepository 和 PostRepository 介面互動，將它們與底層資料儲存機制 (在此情況下為 ConcurrentHashMap) 完全解耦。
