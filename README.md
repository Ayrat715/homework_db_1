# homework_db_1
Проектирование логической модели данных из 6 сущностей и ее реализация.

Я реализовал что-то отдаленно похожее на систему управления псевдо-университетом. 
Создадим таблицы для 6 сущностей: Student (студент), Course (предмет), Department (кафедра),
Professor (преподаватель), Task (задание для студентов), Classroom (учебная аудитория).

```
CREATE TABLE Student (
    StudentID   SERIAL PRIMARY KEY,
    FirstName   TEXT NOT NULL,
    LastName    TEXT NOT NULL,
    DateOfBirth DATE NOT NULL,
    Gender      TEXT CHECK (Gender IN ('Male', 'Female')),
    Email       TEXT UNIQUE NOT NULL
);

CREATE TABLE Course (
    CourseID    SERIAL PRIMARY KEY,
    CourseName  TEXT NOT NULL,
    Description TEXT
);

CREATE TABLE Department (
    DepartmentID   SERIAL PRIMARY KEY,
    DepartmentName TEXT NOT NULL,
    PhoneNumber    TEXT,
    BuildingName   TEXT
);

CREATE TABLE Professor (
    ProfessorID  SERIAL PRIMARY KEY,
    FirstName    TEXT NOT NULL,
    LastName     TEXT NOT NULL,
    DepartmentID INT  NOT NULL,
    FOREIGN KEY (DepartmentID) REFERENCES Department(DepartmentID)
        ON DELETE CASCADE
         ON UPDATE CASCADE
);

CREATE TABLE Task (
    TaskID SERIAL PRIMARY KEY,
    CourseID     INT NOT NULL,
    Title        TEXT NOT NULL,
    Description  TEXT,
    DueDate      DATE,
    FOREIGN KEY (CourseID) REFERENCES Course(CourseID)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

CREATE TABLE Classroom (
    ClassroomID  SERIAL PRIMARY KEY,
    BuildingName TEXT NOT NULL,
    RoomNumber   TEXT NOT NULL,
    Capacity     INT NOT NULL
);
```

После создания таблиц для каждой из сущностей, заполним каждую таблицу значениями.

```
INSERT INTO Student (FirstName, LastName, DateOfBirth, Gender, Email)
VALUES
    ('Ayrat', 'Fakhrutdinov', '2005-11-29', 'Male', 'fakhrutdinovajrat525@gmail.com'),
    ('Amir', 'Kurmaev', '2005-08-12', 'Male', 'kurmaev1995@inbox.ru');

INSERT INTO Course (CourseName, Description)
VALUES
    ('Basics of information systems development', 'Intro to web-development'),
    ('Linear Algebra', 'Introduction to matrices and linear transformations');

INSERT INTO Department (DepartmentName, PhoneNumber, BuildingName)
VALUES
    ('Software Engineering', '206-52-33', 'Main Building №2'),
    ('Algebra and Mathematical Logic', '233-71-60', 'Main Building №2');

INSERT INTO Professor (FirstName, LastName, DepartmentID)
VALUES
    ('Mikail', 'Abramskiy', 1),
    ('Marat', 'Arslanov', 2);

INSERT INTO Task (CourseID, Title, Description, DueDate)
VALUES
    (1, 'Semester work #1', 'Make website on Java Servlet', '2025-01-08'),
    (2, 'Project 1', 'Create a matrix calculator', '2024-02-05');

INSERT INTO Classroom (BuildingName, RoomNumber, Capacity)
VALUES
    ('Main Building №2', '1310', 60),
    ('Main Building №2', '1505', 8);
INSERT INTO Student (FirstName, LastName, DateOfBirth, Gender, Email)
VALUES
    ('Ayrat', 'Fakhrutdinov', '2005-11-29', 'Male', 'fakhrutdinovajrat525@gmail.com'),
    ('Amir', 'Kurmaev', '2005-08-12', 'Male', 'kurmaev1995@inbox.ru');

INSERT INTO Course (CourseName, Description)
VALUES
    ('Basics of information systems development', 'Intro to web-development'),
    ('Linear Algebra', 'Introduction to matrices and linear transformations');

INSERT INTO Department (DepartmentName, PhoneNumber, BuildingName)
VALUES
    ('Software Engineering', '206-52-33', 'Main Building №2'),
    ('Algebra and Mathematical Logic', '233-71-60', 'Main Building №2');

INSERT INTO Professor (FirstName, LastName, DepartmentID)
VALUES
    ('Mikail', 'Abramskiy', 1),
    ('Marat', 'Arslanov', 2);

INSERT INTO Task (CourseID, Title, Description, DueDate)
VALUES
    (1, 'Semester work #1', 'Make website on Java Servlet', '2025-01-08'),
    (2, 'Project 1', 'Create a matrix calculator', '2024-02-05');

INSERT INTO Classroom (BuildingName, RoomNumber, Capacity)
VALUES
    ('Main Building №2', '1310', 60),
    ('Main Building №2', '1505', 8);
```
Финально, таким образом, получим 6 заполненных таблиц сущностей.
