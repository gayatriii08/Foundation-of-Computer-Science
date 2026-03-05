# Secure Data Exchange and Algorithms Assignment

## Student Information
- Name: Gayatri Pokharel
- Student ID: 250245
- Module: Foundation Of Computer Science
- Submission Date: 5th March
---
## Overview
This repository contains three main tasks:
1. **Task 1**: Encoding formats analysis (Base64, Hex, URL encoding)
2. **Task 2**: Seating arrangement problem (P vs NP, brute force, heuristics)
3. **Task 3**: Database normalization for college club management


# Task 1: Data Encoding Formats
## Base64 Encoding examples
- **Original Text:** `user:MySecret@99`
- **Base64 Encoded:** `dXNlcjpNeVNlY3JldEA5OQ==`
- **Base64 Decoded:** `user:MySecret@99`
- **HTTP Authentication Header:** `Authorization: Basic dXNlcjpNeVNlY3JldEA5OQ==`
- **Size Comparison:** Original: 15 bytes, Base64: 20 bytes +33% overhead

## Hex Encoding Examples
- **Original Text:** `Nepal`
- **Hex Encoded:** `4E 65 70 61 6C`
- **Hex Decoded:** `Nepal`
- **Size Comparison:** Original: 5 bytes Hex: 10 bytes  +100% overhead

## URL Encoding Exaples
- **Original Query:**  
  name=Ram &course=BSc IT&year=2025  

- **URL Encoded:**  
  name=Ram Shah&course=BSc IT&year=2025
- **Special Characters Encoding:**  
- Space→ %20
- &→ %26
- =→ %3D
- #→ %23
- @→ %40
- `<` → %3C  
- `>` → %3E
---
### HTTPS Data Flow with URL Encoding
```
1. User Input (username=rahul_sharma&city=mumbai)
              ↓
2. URL Encoding (username=rahul%5Fsharma&city=mumbai)
              ↓
3. HTTP Request (GET /profile?username=rahul%5Fsharma&city=mumbai)
              ↓
4. TLS Encryption (HTTPS - Secure Layer)
              ↓
5. Secure Transmission (Encrypted data over internet)
              ↓
6. TLS Decryption (Server decrypts)
              ↓
7. URL Decoding (username=rahul_sharma&city=mumbai)
              ↓
8. Server Processing (Processes original data)
```
### Email Transmission with Base64
```
1. User Attachment (document.pdf)
              ↓
2. Base64 Encoding (JVBERi0xLjQKJcOkw7zD...)
              ↓
3. SMTP Message (Email with attachment)
              ↓
4. TLS Encryption (STARTTLS)
              ↓
5. Internet (Secure transmission)
              ↓
6. TLS Decryption (Mail server decrypts)
              ↓
7. Base64 Decoding (Converts back to binary)
              ↓
8. Original File Delivered (document.pdf)
```
**Visual Diagram**

**HTTPS Flow**
```

┌────────────┐    ┌────────────┐    ┌────────────┐    ┌────────────┐
│   User     │───▶│    URL     │───▶│   HTTP     │───▶│    TLS    │
│   Input    │    │  Encoding  │    │  Request   │    │ Encryption │
└────────────┘    └────────────┘    └────────────┘    └────────────┘
                                                                  │
                                                                  ▼
┌────────────┐    ┌────────────┐    ┌────────────┐    ┌────────────┐
│  Server    │◀───│    URL     │◀───│    TLS     │◀───│  Secure   │
│ Processing │    │  Decoding  │    │ Decryption │    │Transmission│
└────────────┘    └────────────┘    └────────────┘    └────────────┘
```
---
***Email Flow***
```
┌────────────┐    ┌────────────┐    ┌────────────┐    ┌────────────┐
│   User     │───▶│   Base64   │───▶│    SMTP    │───▶│    TLS    │
│ Attachment │    │  Encoding  │    │  Message   │    │ Encryption │
└────────────┘    └────────────┘    └────────────┘    └────────────┘
                                                                  │
                                                                  ▼
┌────────────┐    ┌────────────┐    ┌────────────┐    ┌────────────┐
│  Original  │◀───│   Base64   │◀───│    TLS     │◀───│  Internet │
│    File    │    │  Decoding  │    │ Decryption │    │            │
└────────────┘    └────────────┘    └────────────┘    └────────────┘

```
---


   
# Task 2
**P vs NP Classification**
**P Problem Example (Easy to Solve):**
- **Task:** Sort 30 students alphabetically
- **Time:** Doubles when students double
- **Example:** 10 students = 1 second, 20 students = 2 seconds
- **Classification:** P Problem ✓

**NP Problem Example (Hard to Solve):**

- **Task:** Arrange 30 students so no friends or same-city students sit next to each other
- **Possible arrangements:** 30! = 2,652,528,598,121,910,586,363,084,800,000,000
- **Classification:** NP Problem ✓

### Brute Force Approach ###
Example with 5 Students
- **Students:** Asha, Bikash, Nisha, Rohan, Suman
- **Constraints:**
- **Asha & Bikash are friends** → cannot sit together
- **Bikash & Nisha are from same city** → cannot sit together

Brute Force tries every arrangement:
```
Attempt 1: Asha | Bikash | Nisha | Rohan | Suman
           ✗ Asha-Bikash are friends — REJECTED

Attempt 2: Asha | Bikash | Rohan | Nisha | Suman
           ✗ Asha-Bikash are friends — REJECTED

Attempt 3: Asha | Nisha | Bikash | Rohan | Suman
           ✓ No conflicts — ACCEPTED ✓
```
**Result: Found valid arrangement on attempt 3 out of 120 total**
           
### Heuristic Approach ###
Example
Same 5 students with conflict map:

- Asha ↔ Bikash (friends)
- Bikash ↔ Nisha (same city)
- Rohan ↔ Suman (friends)

Step 1 — Rank by most conflicts:

- Bikash — 2 conflicts (hardest to seat)
- Asha — 1 conflict
- Nisha — 1 conflict
- Rohan — 1 conflict
- Suman — 1 conflict
  
Step 2 — Seat most constrained first:
```
Seat 1: Place Bikash first → [Bikash] [ ] [ ] [ ] [ ]
Seat 2: Try Asha next to Bikash → CONFLICT ✗
Seat 2: Try Rohan next to Bikash → No conflict ✓
         → [Bikash] [Rohan] [ ] [ ] [ ]
Seat 3: Try Asha → No conflict with Rohan ✓
         → [Bikash] [Rohan] [Asha] [ ] [ ]
Seat 4: Try Nisha → No conflict with Asha ✓
         → [Bikash] [Rohan] [Asha] [Nisha] [ ]
Seat 5: Place Suman → Check conflict with Nisha ✓
         → [Bikash] [Rohan] [Asha] [Nisha] [Suman] ✓

```
**Result: Valid arrangement found in just 6 steps instead of up to 120!**

**Complexity Comparison**

| Approach     | Method                              | Steps for 30 Students | Time Estimate              |
|--------------|-------------------------------------|----------------------|----------------------------|
| Brute Force  | Try all possible arrangements       | 2.65 × 10³² arrangements | > Age of universe (4+ trillion years) |
| Heuristic    | Seat most constrained students first | ~900 placement checks | Milliseconds               |

---
# Task 3 (Normalization)
## Original table ##

| StudentID | StudentName | Email              | ClubName     | ClubRoom | ClubMentor | JoinDate  |
|-----------|-------------|--------------------|--------------|----------|------------|-----------|
| 1         | Asha        | asha@email.com     | Music Club   | R101     | Mr. Raman  | 1/10/2024 |
| 2         | Bikash      | bikash@email.com   | Sports Club  | R202     | Ms. Sita   | 1/12/2024 |
| 3         | Nisha       | nisha@email.com    | Music Club   | R101     | Mr. Raman  | 1/20/2024 |
| 4         | Rohan       | rohan@email.com    | Drama Club   | R303     | Mr. Kiran  | 1/18/2024 |
| 5         | Suman       | suman@email.com    | Music Club   | R101     | Mr. Raman  | 1/22/2024 |
| 6         | Bikash      | bikash@email.com   | Drama Club   | R303     | Mr. Kiran  | 1/25/2024 |
| 7         | Pooja       | pooja@email.com    | Sports Club  | R202     | Ms. Sita   | 1/27/2024 |
| 8         | Nisha       | nisha@email.com    | Coding Club  | Lab1     | Mr. Anil   | 1/28/2024 |
| 9         | Aman        | aman@email.com     | Coding Club  | Lab1     | Mr. Anil   | 1/30/2024 |


## Normalized Tables 

**Student Table**
| StudentID | StudentName | Email              |
|-----------|-------------|--------------------|
| 1         | Asha        | asha@email.com     |
| 2         | Bikash      | bikash@email.com   |
| 3         | Nisha       | nisha@email.com    |
| 4         | Rohan       | rohan@email.com    |
| 5         | Suman       | suman@email.com    |
| 6         | Pooja       | pooja@email.com    |
| 7         | Aman        | aman@email.com     |

**Club Table**
| ClubID | ClubName     | ClubRoom | ClubMentor |
|--------|--------------|----------|------------|
| C01    | Music Club   | R101     | Mr. Raman  |
| C02    | Sports Club  | R202     | Ms. Sita   |
| C03    | Drama Club   | R303     | Mr. Kiran  |
| C04    | Coding Club  | Lab1     | Mr. Anil   |

**Membership Table**
| StudentID | ClubID | JoinDate  |
|-----------|--------|-----------|
| 1         | C01    | 1/10/2024 |
| 2         | C02    | 1/12/2024 |
| 3         | C01    | 1/20/2024 |
| 4         | C03    | 1/18/2024 |
| 5         | C01    | 1/22/2024 |
| 2         | C03    | 1/25/2024 |
| 6         | C02    | 1/27/2024 |
| 3         | C04    | 1/28/2024 |
| 7         | C04    | 1/30/2024 |


## ER Diagram ##
```
STUDENT                  MEMBERSHIP                CLUB
+-----------+            +-------------+           +----------+
| StudentID |---(1)---<--| StudentID   |-->---(1)--| ClubName |
| StudentName|           | ClubName    |           | ClubRoom |
| Email     |            | JoinDate    |           | ClubMentor|
+-----------+            +-------------+           +----------+

Student (1) ----< Membership >---- (1) Club
         One              Many  Many          One

```

---

## SQL SCRIPT (database.sql)
```sql
CREATE database gayatricoursework_db;
use gayatricoursework_db;

Create table Student(
 StudentId INT PRIMARY KEY,
    StudentName VARCHAR(50),
    Email Varchar(255)
);

Create table Club(
ClubId INT primary key,
	ClubName Varchar(50),
    ClubRoom Varchar(10),
    ClubMentor Varchar(30)
);

CREATE TABLE Membership (
    MembershipId INT PRIMARY KEY,
    StudentId INT,
    ClubId INT,
    JoinDate DATE,
    FOREIGN KEY (StudentId) REFERENCES Student(StudentId),
    FOREIGN KEY (ClubId) REFERENCES Club(ClubId)
);

INSERT INTO Student (StudentID, StudentName, Email)
VALUES 
(1, 'Asha', 'asha@email.com'),
(2, 'Bikash', 'bikash@email.com'),
(3, 'Nisha', 'nisha@email.com'),
(4, 'Rohan', 'rohan@email.com'),
(5, 'Suman', 'suman@email.com'),
(6, 'Pooja', 'pooja@email.com'),
(7, 'Aman', 'aman@email.com');

INSERT INTO Club (ClubID, ClubName, ClubRoom, ClubMentor)
VALUES
(101, 'Music Club', 'R101', 'Mr. Raman'),
(202, 'Sports Club', 'R202', 'Ms. Sita'),
(303, 'Drama Club', 'R303', 'Mr. Kiran'),
(401, 'Coding Club', 'Lab1', 'Mr. Anil');

INSERT INTO Membership (MembershipID, StudentID, ClubID, JoinDate)
VALUES
(1, 1, 101, '2024-01-10'),
(2, 2, 202, '2024-01-12'),
(3, 1, 202, '2024-01-15'),
(4, 3, 101, '2024-01-20'),
(5, 4, 303, '2024-01-18'),
(6, 5, 101, '2024-01-22'),
(7, 2, 303, '2024-01-25'),
(8, 6, 202, '2024-01-27'),
(9, 3, 401, '2024-01-28'),
(10, 7, 401, '2024-01-30');

SELECT s.StudentName, s.Email, c.ClubName, c.ClubRoom, c.ClubMentor, m.JoinDate
FROM Membership m
JOIN Student s ON m.StudentID = s.StudentID
JOIN Club c ON m.ClubID = c.ClubID;

INSERT INTO Student (StudentID, StudentName, Email)
VALUES (8, 'Pratha', 'Pratha@email.com');

INSERT INTO Club (ClubID, ClubName, ClubRoom, ClubMentor)
VALUES (105, 'Art Club', 'R404', 'Ms. Jenisha');

SELECT * FROM Student;
SELECT * FROM Club;

SELECT s.StudentName
FROM Student s;

SELECT c.ClubName
FROM Club c;

SELECT JoinDate
FROM Membership;

SELECT *
FROM Membership m
JOIN Student s ON m.StudentID = s.StudentID
JOIN Club c ON m.ClubID = c.ClubID;
```

---
## HOW TO RUN
1. **Clone repository:**
   ```bash
   git clone  https://github.com/gayatriii08/Foundation-of-Computer-Science
   ```
2. **Run SQL script:**
   ```bash
   mysql -u username -p < database.sql
   ```
