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



