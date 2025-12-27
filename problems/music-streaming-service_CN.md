# 設計像 Spotify 這樣的線上音樂串流服務

## 需求
1. 音樂串流服務應允許使用者瀏覽和搜尋歌曲、專輯和藝人。
2. 使用者應能夠建立和管理播放列表。
3. 系統應支援使用者身分驗證和授權。
4. 使用者應能夠播放、暫停、跳過和在歌曲內搜尋。
5. 系統應根據使用者偏好和收聽歷史記錄推薦歌曲和播放列表。
6. 系統應處理並發請求並確保多個使用者的流暢串流體驗。
7. 系統應具有可擴展性，並處理大量的歌曲和使用者。
8. 系統應具有可延伸性，以支援社交分享和離線播放等額外功能。

## UML 類別圖

![](../class-diagrams/musicstreamingservice-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/musicstreamingservice/) 
#### [Python 實作](../solutions/python/musicstreamingservice/)
#### [C++ 實作](../solutions/cpp/musicstreamingservice/)
#### [C# 實作](../solutions/csharp/musicstreamingservice/)
#### [Go 實作](../solutions/golang/musicstreamingservice/)

## 類別、介面和列舉
1. **Song**、**Album** 和 **Artist** 類別代表音樂串流服務中的基本實體，具有 ID、標題、藝人、專輯、持續時間以及它們之間的關係等屬性。
2. **User** 類別代表音樂串流服務的使用者，具有 ID、使用者名稱、密碼和播放列表列表等屬性。
3. **Playlist** 類別代表使用者建立的播放列表，包含歌曲列表。
4. **MusicLibrary** 類別作為儲存和管理歌曲、專輯和藝人的中央儲存庫。它遵循單例模式以確保音樂庫只有一個實例。
5. **UserManager** 類別處理使用者註冊、登入和其他使用者相關操作。它也遵循單例模式。
6. **MusicPlayer** 類別代表音樂播放功能，允許使用者播放、暫停、跳過和在歌曲內搜尋。
7. **MusicRecommender** 類別根據使用者偏好和收聽歷史記錄產生歌曲推薦。它遵循單例模式。
8. **MusicStreamingService** 類別是音樂串流服務的主要入口點。它初始化必要的組件，處理使用者請求，並管理服務的整體功能。
