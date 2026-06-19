DROP TABLE IF EXISTS Enrollments;
DROP TABLE IF EXISTS Courses;
DROP TABLE IF EXISTS Students;
CREATE TABLE Students (
    StudentID INTEGER PRIMARY KEY,
    Name TEXT,
    Gender TEXT,
    Age INTEGER
);
CREATE TABLE Courses (
    CourseID INTEGER PRIMARY KEY,
    CourseName TEXT
);
CREATE TABLE Enrollments (
    StudentID INTEGER,
    CourseID INTEGER,
    Grade INTEGER
);
INSERT INTO Students VALUES
(1,'Aarav','Male',18),
(2,'Diya','Female',19),
(3,'Rohan','Male',18),
(4,'Sneha','Female',20),
(5,'Vikram','Male',19),
(6,'Ananya','Female',18),
(7,'Kiran','Male',20),
(8,'Priya','Female',19),
(9,'Rahul','Male',18),
(10,'Meera','Female',20);
INSERT INTO Courses VALUES
(1,'Mathematics'),
(2,'Science'),
(3,'English');
INSERT INTO Enrollments VALUES
(1,1,85),(1,2,78),(1,3,90),
(2,1,92),(2,2,88),(2,3,95),
(3,1,65),(3,2,70),(3,3,68),
(4,1,55),(4,2,60),(4,3,58),
(5,1,40),(5,2,45),(5,3,50),
(6,1,98),(6,2,96),(6,3,94),
(7,1,35),(7,2,30),(7,3,38),
(8,1,80),(8,2,82),(8,3,79),
(9,1,72),(9,2,75),(9,3,70),
(10,1,88),(10,2,90),(10,3,85);
SELECT c.CourseName, s.StudentID, s.Name, e.Grade
FROM Enrollments e
JOIN Students s ON e.StudentID = s.StudentID
JOIN Courses c ON e.CourseID = c.CourseID
ORDER BY c.CourseName, s.Name;
SELECT c.CourseName,
ROUND(AVG(e.Grade),2) AS Average_Grade
FROM Enrollments e
JOIN Courses c ON e.CourseID = c.CourseID
GROUP BY c.CourseName;
SELECT s.StudentID, s.Name,
ROUND(AVG(e.Grade),2) AS Average_Grade
FROM Students s
JOIN Enrollments e ON s.StudentID = e.StudentID
GROUP BY s.StudentID, s.Name
ORDER BY Average_Grade DESC
LIMIT 3;
SELECT COUNT(DISTINCT StudentID) AS Failed_Students
FROM Enrollments
WHERE Grade < 40;
