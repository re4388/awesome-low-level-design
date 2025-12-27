# 板球資訊系統 (LLD)

## 問題陳述

設計並實作一個類似 CricInfo 的板球資訊系統，提供有關板球比賽、球隊、球員和即時比分的綜合資訊。該系統應處理即時更新、比賽統計數據和使用者互動。

---

## 需求

1. **比賽資訊管理：**
   - 儲存和管理板球比賽詳細資訊
   - 追蹤比賽時間表和結果
   - 支援即時比分更新
   - 處理比賽狀態轉換

2. **球隊和球員管理：**
   - 維護球隊名單和球員資訊
   - 追蹤球員角色和統計數據
   - 支援球隊組成變更

3. **記分卡管理：**
   - 記錄詳細的比賽統計數據
   - 追蹤局數 (innings)、回合 (overs) 和逐球 (ball-by-ball) 資訊
   - 維護打擊和投球統計數據

4. **搜尋和檢索：**
   - 搜尋比賽、球隊和球員
   - 查看詳細的比賽資訊
   - 存取歷史數據和統計數據

5. **系統需求：**
   - 處理並發存取
   - 確保資料一致性
   - 支援可擴展性
   - 允許未來的擴展

---

## 核心實體

### 1. Match
- **欄位：** String id, String title, String venue, Date startTime, Team team1, Team team2, MatchStatus status, Scorecard scorecard
- **方法：** updateStatus(), getScorecard(), getMatchDetails()

### 2. Team
- **欄位：** String id, String name, List<Player> players
- **方法：** addPlayer(), removePlayer(), getTeamStats()

### 3. Player
- **欄位：** String id, String name, String role
- **方法：** getPlayerStats(), updateRole()

### 4. Scorecard
- **欄位：** Match match, List<Innings> innings
- **方法：** addInnings(), updateScore(), getMatchSummary()

### 5. Innings
- **欄位：** String id, Team battingTeam, Team bowlingTeam, List<Over> overs
- **方法：** addOver(), getInningsSummary()

### 6. Over
- **欄位：** int overNumber, List<Ball> balls
- **方法：** addBall(), getOverSummary()

### 7. Ball
- **欄位：** int ballNumber, Player bowler, Player batsman, String result
- **方法：** recordResult(), getBallDetails()

### 8. MatchStatus (列舉)
- **值：** SCHEDULED, IN_PROGRESS, COMPLETED, ABANDONED

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/cricinfo-class-diagram.png)

---

## 服務

### 1. MatchService (Singleton)
- **方法：** 
  - addMatch(Match match)
  - getMatch(String id)
  - updateMatchStatus(String id, MatchStatus status)
  - searchMatches(String query)

### 2. ScorecardService (Singleton)
- **方法：**
  - createScorecard(Match match)
  - updateScorecard(String matchId, Scorecard scorecard)
  - getScorecard(String matchId)
  - addInnings(String matchId, Innings innings)

### 3. CricinfoSystem
- **方法：**
  - getMatchDetails(String matchId)
  - getTeamDetails(String teamId)
  - getPlayerDetails(String playerId)
  - search(String query)

---

## 範例用法

```java
CricinfoSystem system = CricinfoSystem.getInstance();

// 建立一場新比賽
Match match = system.createMatch("IND vs AUS", "Melbourne Cricket Ground", new Date());

// 更新比賽狀態
system.updateMatchStatus(match.getId(), MatchStatus.IN_PROGRESS);

// 記錄一球
system.recordBall(match.getId(), 1, 1, "FOUR");

// 獲取比賽詳細資訊
MatchDetails details = system.getMatchDetails(match.getId());
```

---

## 演示

請參閱演示類別以獲取板球資訊系統的範例用法和模擬。

---

## 擴展框架

- **新增使用者驗證：** 支援使用者帳戶和偏好設定
- **新增評論系統：** 即時比賽評論
- **新增統計引擎：** 進階球員和球隊統計數據
- **新增通知系統：** 比賽更新和提醒
- **新增社群功能：** 使用者評論和討論

---

## 使用的設計模式

- **單例模式 (Singleton Pattern)：** 用於服務類別 (MatchService, ScorecardService)
- **工廠模式 (Factory Pattern)：** 用於建立比賽和記分卡
- **觀察者模式 (Observer Pattern)：** 用於即時更新和通知
- **策略模式 (Strategy Pattern)：** 用於不同類型的比賽格式

---
