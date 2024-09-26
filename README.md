# Library Management System Using SQL 

## Introduction:
I recently visited a local library where I was greeted by shelves of books and a librarian armed with a pen and checkout ledger. Curiosity got me, so I asked, “How’s managing all these books going?”

With a sigh, she told me about the struggles; tracking overdue books felt like a detective work and every time a book was borrowed, she’d pray the borrower would return it on time. As she continued, I realized that this was the perfect problem for an SQL project! If she was going to keep those books in order, she needed a system that wouldn’t crumble. And so, the Library Management System was born.

## Problem statement:
The library is struggling to efficiently manage its book inventory, track user borrowings, and monitor loan returns. The manual system currently used is time-consuming, prone to human errors, and lacks real-data retrieval for managing users, books, and loans records.

## Objective:
To design and implement a relational database that will efficiently store and manage user and book data, help in tracking book borrowings, return dates, and provide real-time data on available books and overdue loans.

## Database Design:
The database for the Library Management System consists of three main tables:

1. Books Table

  - Attributes:
      - BookID (INT, Primary Key)
      - Title (VARCHAR)
      - Author (VARCHAR)
      - Genre (VARCHAR)
      - PublishedYear (INT)

```sql
CREATE TABLE Books (
    BookID INT PRIMARY KEY,
    Title VARCHAR(100),
    Author VARCHAR(100),
    Genre VARCHAR(50),
    PublishedYear INT
);
```

2. Users Table

  - Attributes:
      - UserID (INT, Primary Key)
      - FullName (VARCHAR)
      - Email (VARCHAR)
      - JoinDate (DATE)

```sql
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Email VARCHAR(100),
    JoinDate DATE
);
```

3. Loans Table

  - Attributes:
      - LoanID (INT, Primary Key)
      - BookID (INT, Foreign Key)
      - UserID (INT, Foreign Key)
      - LoanDate (DATE)
      - ReturnDate (DATE)

```sql
CREATE TABLE Loans (
    LoanID INT PRIMARY KEY,
    BookID INT,
    UserID INT,
    LoanDate DATE,
    ReturnDate DATE,
    FOREIGN KEY (BookID) REFERENCES Books(BookID),
    FOREIGN KEY (UserID) REFERENCES Users(UserID)
);
```
