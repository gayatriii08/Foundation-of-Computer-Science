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
2. **Task 2**: Database normalization for college club management
3. **Task 3**: Seating arrangement problem (P vs NP, brute force, heuristics)


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
- **Original Query:** `name=Gayatri Pokharel&course=BSc IT&year=2024`
- **URL Encoded:** `name=Gayatri%20Pokharel&course=BSc%20IT&year=2024`
- **Special Characters Encoding:**
- Space→ `%20`
- < → `%3C`
- > → `%3E`
- " → `%22`
- @ → `%40`
- % → `%25`


---

# Task 2

# Task 3 (Normalization)
**Original table**

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


### Normalized Tables 

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


### ER Diagram
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


