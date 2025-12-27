# 音樂串流服務 (LLD)

## 問題陳述

設計並實作一個線上音樂串流服務 (類似 Spotify)，允許使用者瀏覽、搜尋和播放歌曲，管理播放列表，追蹤藝人，並接收推薦。

---

## 需求

- **使用者管理：** 使用者可以註冊、登入並管理其個人資料。
- **瀏覽與搜尋：** 使用者可以瀏覽和搜尋歌曲、專輯和藝人。
- **播放列表：** 使用者可以建立、更新和管理播放列表。
- **播放控制：** 使用者可以播放、暫停、跳過和在歌曲內搜尋。
- **推薦：** 系統根據使用者偏好和收聽歷史記錄推薦歌曲和播放列表。
- **追蹤藝人：** 使用者可以追蹤藝人以獲取更新和推薦。
- **並發性：** 系統處理並發請求並為多個使用者提供流暢的串流。
- **可擴展性：** 系統可擴展以處理大量歌曲和使用者。
- **可擴展性：** 易於新增功能，例如社群分享、離線播放或協作播放列表。

---

## 核心實體

- **Song：** 代表一首歌曲，具有 ID、標題、藝人、專輯和時長等屬性。
- **Album：** 代表包含多首歌曲並與藝人相關聯的專輯。
- **Artist：** 代表一位音樂藝人，具有專輯和歌曲列表。
- **User：** 代表一位使用者，具有 ID、使用者名稱、密碼、播放列表和收聽歷史記錄。
- **Playlist：** 代表使用者建立的播放列表，包含歌曲列表。
- **MusicLibrary：** 用於儲存和管理歌曲、專輯和藝人的中央儲存庫 (Singleton)。
- **UserManager：** 處理使用者註冊、登入和使用者相關操作 (Singleton)。
- **MusicPlayer：** 處理音樂播放 (播放、暫停、跳過、搜尋)。
- **MusicRecommender：** 根據使用者偏好和歷史記錄產生歌曲和播放列表推薦 (Singleton)。
- **MusicStreamingService：** 主要進入點，初始化組件，處理使用者請求，並管理整體功能。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/musicstreamingservice-class-diagram.png)

### 1. Song
- **欄位：** int id, String title, Artist artist, Album album, int duration
- **方法：** getId(), getTitle(), getArtist(), getAlbum(), getDuration()

### 2. Album
- **欄位：** int id, String title, Artist artist, List<Song> songs
- **方法：** getId(), getTitle(), getArtist(), getSongs()

### 3. Artist
- **欄位：** int id, String name, List<Album> albums, List<Song> songs
- **方法：** getId(), getName(), getAlbums(), getSongs()

### 4. User
- **欄位：** int id, String username, String password, List<Playlist> playlists, List<Song> listeningHistory, List<Artist> followedArtists
- **方法：** getId(), getUsername(), getPlaylists(), followArtist(Artist) 等。

### 5. Playlist
- **欄位：** int id, String name, List<Song> songs
- **方法：** addSong(Song), removeSong(Song), getSongs()

### 6. MusicLibrary (Singleton)
- **欄位：** Map<Integer, Song> songs, Map<Integer, Album> albums, Map<Integer, Artist> artists
- **方法：** addSong(Song), addAlbum(Album), addArtist(Artist), searchSongs(String), searchAlbums(String), searchArtists(String)

### 7. UserManager (Singleton)
- **欄位：** Map<Integer, User> users
- **方法：** registerUser(...), login(...), getUser(int id)

### 8. MusicPlayer
- **欄位：** Song currentSong, int currentPosition, boolean isPlaying
- **方法：** play(Song), pause(), skip(), seek(int position)

### 9. MusicRecommender (Singleton)
- **方法：** recommendSongs(User), recommendPlaylists(User)

### 10. MusicStreamingService
- **欄位：** MusicLibrary library, UserManager userManager, MusicPlayer player, MusicRecommender recommender
- **方法：** initialize(), handleUserRequest(...) 等。

---

## 使用的設計模式

- **單例模式 (Singleton Pattern)：** 用於 `MusicLibrary`、`UserManager` 和 `MusicRecommender` 以確保單一實例。
---

## 範例用法

```java
MusicStreamingService service = new MusicStreamingService();
service.initialize();

User alice = service.getUserManager().registerUser("alice", "password");
Artist artist = new Artist(1, "The Beatles");
Album album = new Album(1, "Abbey Road", artist);
Song song = new Song(1, "Come Together", artist, album, 259);

service.getLibrary().addArtist(artist);
service.getLibrary().addAlbum(album);
service.getLibrary().addSong(song);

alice.getPlaylists().add(new Playlist(1, "Favorites"));
alice.getPlaylists().get(0).addSong(song);

service.getPlayer().play(song);
```

---

## 演示

請參閱 `MusicStreamingServiceDemo.java` 以獲取音樂串流服務的範例用法和模擬。

---

## 擴展框架

- **新增社群功能：** 允許使用者分享播放列表或互相關注。
- **新增離線播放：** 支援下載歌曲以進行離線收聽。
- **新增協作播放列表：** 允許其多個使用者編輯播放列表。

---
