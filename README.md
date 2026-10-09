# RDBMS Program 13 - Normalization up to 3NF

## Objective

Consider the following Student table:

```text
Student(
    StudentID,
    StudentName,
    CourseName,
    FacultyName,
    DepartmentName
)
```

Normalize the table up to **Third Normal Form (3NF)**.

## Original Table

The original table contains:

| StudentID | StudentName | CourseName       | FacultyName | DepartmentName   |
| --------- | ----------- | ---------------- | ----------- | ---------------- |
| 1001      | Arun        | Database Systems | Dr. Ravi    | Computer Science |
| 1001      | Arun        | Data Structures  | Dr. Ravi    | Computer Science |
| 1002      | Priya       | Mathematics      | Dr. Meena   | Mathematics      |
| 1003      | Kumar       | Database Systems | Dr. Ravi    | Computer Science |

## Step 1 - First Normal Form (1NF)

A relation is in **1NF** when:

* Each column contains atomic values.
* There are no repeating groups.
* Each row is uniquely identifiable.

The Student table contains atomic values, so it can be converted into 1NF.

## Step 2 - Second Normal Form (2NF)

A relation is in **2NF** when:

1. It is already in 1NF.
2. There is no partial dependency on part of a composite key.

Separate the data into appropriate tables:

```text
Student(StudentID, StudentName)

Course(CourseID, CourseName, FacultyID)

Faculty(FacultyID, FacultyName, DepartmentID)

Department(DepartmentID, DepartmentName)

StudentCourse(StudentID, CourseID)
```

## Step 3 - Third Normal Form (3NF)

A relation is in **3NF** when:

1. It is already in 2NF.
2. There is no transitive dependency.

The final 3NF structure is:

### Student

```text
StudentID (PK)
StudentName
```

### Department

```text
DepartmentID (PK)
DepartmentName
```

### Faculty

```text
FacultyID (PK)
FacultyName
DepartmentID (FK)
```

### Course

```text
CourseID (PK)
CourseName
FacultyID (FK)
```

### StudentCourse

```text
StudentID (PK, FK)
CourseID (PK, FK)
```

## Functional Dependencies

```text
StudentID → StudentName

DepartmentID → DepartmentName

FacultyID → FacultyName, DepartmentID

CourseID → CourseName, FacultyID

StudentID + CourseID → StudentCourse
```

## Final Normalized Structure

```text
                 DEPARTMENT
                 ┌──────────────────┐
                 │ DepartmentID PK  │
                 │ DepartmentName   │
                 └────────┬─────────┘
                          │
                          │ 1:N
                          │
                 ┌────────▼─────────┐
                 │     FACULTY      │
                 │──────────────────│
                 │ FacultyID PK     │
                 │ FacultyName      │
                 │ DepartmentID FK  │
                 └────────┬─────────┘
                          │
                          │ 1:N
                          │
                 ┌────────▼─────────┐
                 │      COURSE      │
                 │──────────────────│
                 │ CourseID PK      │
                 │ CourseName       │
                 │ FacultyID FK     │
                 └────────┬─────────┘
                          │
                          │
                          │
                 ┌────────▼─────────┐
                 │  STUDENTCOURSE   │
                 │──────────────────│
                 │ StudentID PK,FK  │
                 │ CourseID PK,FK   │
                 └────────┬─────────┘
                          │
                          │ N:1
                          │
                 ┌────────▼─────────┐
                 │     STUDENT      │
                 │──────────────────│
                 │ StudentID PK     │
                 │ StudentName      │
                 └──────────────────┘
```

## Why Normalization is Required

Normalization helps to:

* Reduce data redundancy.
* Avoid duplicate data.
* Prevent update anomalies.
* Improve data integrity.
* Make database design more efficient.

## Student Task

Students must:

1. Create the `CollegeDB` database.
2. Analyze the given unnormalized Student table.
3. Convert the table into 1NF.
4. Convert the table into 2NF.
5. Convert the table into 3NF.
6. Create the normalized tables.
7. Identify Primary Keys.
8. Identify Foreign Keys.
9. Insert suitable sample records.
10. Display the normalized data using JOIN operations.

## Submission Instructions

1. Complete `student_solution.sql`.
2. Save the file.
3. Commit the changes.
4. Push the changes to GitHub.
5. Open the **Actions** tab.
6. Check the autograding result.

## Important

* Do not modify `test.sh`.
* Do not modify `.github/workflows/autograding.yml`.
* Only modify `student_solution.sql`.
* Use the table names exactly as specified.
* Primary Keys and Foreign Keys must be defined correctly.

## Total Marks

**10 Marks**
