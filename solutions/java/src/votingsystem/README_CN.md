# 投票系統 (LLD)

## 問題陳述

設計並實作一個投票系統，允許選民為候選人投票，確保每個選民只能投票一次，並提供計票和顯示結果的功能。

---

## 需求

- **選民註冊：** 系統管理合格選民的列表。
- **候選人註冊：** 系統管理候選人列表。
- **投票：** 每個選民可以為一名候選人投票，但只能投一次。
- **投票記錄：** 系統記錄每一票並防止重複投票。
- **結果統計：** 系統可以統計每位候選人的票數並顯示結果。
- **可擴展性：** 易於新增功能，例如多個選舉、投票輪次或不同的投票方式。

---

## 核心實體

- **VotingSystem：** 管理選民、候選人、投票和結果統計的主要類別。
- **Voter：** 代表具有唯一 ID 和姓名的選民。
- **Candidate：** 代表具有唯一 ID 和姓名的候選人。
- **VoteRecord：** 代表選民為候選人投下的投票記錄。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/votingsystem-class-diagram.png)

### 1. VotingSystem

- **欄位：** Map<Integer, Voter> voters, Map<Integer, Candidate> candidates, Map<Integer, VoteRecord> voteRecords
- **方法：** registerVoter(Voter), registerCandidate(Candidate), castVote(int voterId, int candidateId), tallyResults(), displayResults(), hasVoted(int voterId)

### 2. Voter

- **欄位：** int id, String name

### 3. Candidate

- **欄位：** int id, String name

### 4. VoteRecord

- **欄位：** int voterId, int candidateId

---

## 範例用法

```java
VotingSystem votingSystem = new VotingSystem();
votingSystem.registerVoter(new Voter(1, "Alice"));
votingSystem.registerVoter(new Voter(2, "Bob"));
votingSystem.registerCandidate(new Candidate(1, "John"));
votingSystem.registerCandidate(new Candidate(2, "Jane"));

votingSystem.castVote(1, 1); // Alice 投給 John
votingSystem.castVote(2, 2); // Bob 投給 Jane

votingSystem.displayResults();
```

---

## 演示

請參閱 `VotingSystemDemo.java` 以獲取投票系統的範例用法和模擬。

---

## 擴展設計

- **新增多個選舉：** 支援不同的選舉或投票輪次。
- **新增投票方式：** 實作排序選擇、加權投票等。
- **新增功能：** 例如選民驗證、審計日誌或結果匯出。

---
