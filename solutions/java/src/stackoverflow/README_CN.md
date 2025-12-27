# StackOverflow 系統 (LLD)

## 問題陳述

設計並實作一個簡化的類似 StackOverflow 的問答平台。系統應允許使用者發布問題和回答、對其進行投票、評論、標記問題並追蹤使用者聲譽。

---

## 需求

- **使用者管理：** 使用者可以提問、回答、評論和投票。
- **問題與回答：** 使用者可以發布問題和回答。每個問題可以有多個回答，以及一個被接受的回答。
- **投票：** 使用者可以對問題和回答投贊成票或反對票。聲譽會相應更新。
- **評論：** 使用者可以對問題和回答進行評論。
- **標籤：** 問題可以被標記以進行分類。
- **聲譽：** 使用者根據投票和被接受的回答獲得或失去聲譽。
- **被接受的回答：** 問題作者可以將一個回答標記為被接受。

---

## 核心實體

- **User：** 代表使用者，追蹤聲譽和使用者詳細資訊。
- **Question：** 代表問題，包含回答、評論、標籤、投票和被接受的回答。
- **Answer：** 代表對問題的回答，包含評論、投票和被接受狀態。
- **Comment：** 代表對問題或回答的評論。
- **Tag：** 代表用於分類問題的標籤。
- **Vote：** 代表使用者對問題或回答的投票 (贊成票/反對票)。
- **VoteType：** UPVOTE 和 DOWNVOTE 的列舉。
- **Votable (介面)：** 用於可以被投票的實體。
- **Commentable (介面)：** 用於可以被評論的實體。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/stackoverflow-class-diagram.png)

### 1. User
- **欄位：** id, name, reputation 等。
- **方法：** updateReputation(int delta), getReputation() 等。

### 2. Question
- **欄位：** id, title, content, author, creationDate, answers, comments, tags, votes, acceptedAnswer
- **方法：** addAnswer(Answer), acceptAnswer(Answer), vote(User, VoteType), getVoteCount(), addComment(Comment), getComments() 等。

### 3. Answer
- **欄位：** id, content, author, question, isAccepted, creationDate, comments, votes
- **方法：** vote(User, VoteType), getVoteCount(), addComment(Comment), getComments(), markAsAccepted() 等。

### 4. Comment
- **欄位：** id, content, author, creationDate

### 5. Tag
- **欄位：** name

### 6. Vote
- **欄位：** voter, type (VoteType)
- **方法：** getVoter(), getType()

### 7. VoteType
- 列舉：UPVOTE, DOWNVOTE

### 8. Votable (介面)
- **方法：** vote(User, VoteType), getVoteCount()

### 9. Commentable (介面)
- **方法：** addComment(Comment), getComments()

---

## 使用的設計模式

- **策略模式 (Strategy Pattern)：** 透過介面用於投票和評論行為。
- **觀察者模式 (Observer Pattern)：** (概念上) 用於投票和被接受回答的聲譽更新。

---

## 範例用法

```java
User alice = new User("Alice");
Question q = new Question(alice, "What is Java?", "Explain Java basics.", Arrays.asList("java", "basics"));
User bob = new User("Bob");
Answer a = new Answer(bob, q, "Java is a programming language.");
q.addAnswer(a);
q.vote(bob, VoteType.UPVOTE);
a.vote(alice, VoteType.UPVOTE);
q.acceptAnswer(a);
```

---

## 演示

請參閱 `StackOverflowDemo.java` 以獲取 StackOverflow 系統的範例用法。

---

## 擴展框架

- **新增功能：** 例如徽章、使用者個人資料或進階搜尋。
- **新增新的投票類型：** 擴展 `VoteType` 並更新 `vote()` 方法中的邏輯。
- **新增審核：** 實作管理員/版主角色以進行內容管理。

---
