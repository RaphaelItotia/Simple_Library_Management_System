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

## Implementation:

  - Inserting Data: I inserted sample data into each table to facilitate testing and demonstration of functionalities.

```sql
    INSERT INTO Books (BookID,Title,Author,Genre,PublishedYear)
VALUES (1, 'The River and the Source', 'Margaret A. Ogolla', 'Historical Fiction',1994),
		(2, 'Dust','Yvonne Adhiambo Owuor','Literacy Fiction',2013),
		(3,'Petals of Blood','Ngugi wa Thiongo','Political Fiction',1977),
		(4,'Unbowed: A Memoir','Wangari Maathai','Autobiography',2006),
		(5,'Weep Not, Child','Ngugi wa Thiongo','Coming-of-Age Fiction',1964)

INSERT INTO Users (UserID,FullName,Email,JoinDate)
VALUES (1,'Cate Wanjiru','catewanji@gmail.com','2023-11-21'),
		(2, 'Henry Kangethe','henry1k@gmail.com','2023-12-03'),
		(3,'Hellen Mutinda','hellenmut1nda@gmail.com','2023-12-11'),
		(4,'Gladys Mutio','gladysmut1o2@gmail.com','2024-01-02'),
		(5,'Samuel Omondi','Samuel21Omo@gmail.com','2024-01-02')

INSERT INTO Loans (LoanID,BookID,UserID,LoanDate,ReturnDate)
VALUES (1,1,2,'2023-12-06','2023-12-13'),
		(2,5,1,'2023-11-24',NULL),
		(3,3,3,'2024-01-02','2024-01-12')
```

  - Data Retrieval: I created various SQL queries to meet the project objectives;
    
   1. Find All Books Currently Loaned Out:
      
```sql
      SELECT Books.Title, Users.FullName, Loans.LoanDate
FROM Loans
JOIN Books ON Loans.BookID = Books.BookID
JOIN Users ON Loans.UserID = Users.UserID
WHERE ReturnDate IS NULL;
```

  2. List All Books by a Specific Author:
     
```sql
SELECT Title
FROM Books
WHERE Author = 'Ngugi wa Thiongo';
```

  3. List of Users Who Have Borrowed a Book:

```sql
SELECT Users.FullName, Books.Title
FROM Loans
JOIN Users ON Loans.UserID = Users.UserID
JOIN Books ON Loans.BookID = Books.BookID;
```

## Results:
The SQL implementation provided a structured and efficient way to manage library data. 
Key functionalities included:

 - Tracking of currently loaned books.
 - Reporting on book availability by author.
 - Comprehensive user borrowing records.

## Conclusion:
The Library Management System demonstrates a solid understanding of SQL database design and implementation. The project effectively addresses the challenges faced by the library through organized data management. 

## Future Work

  - Implementing user authentication and role-based access control.
  - Creating a web-based interface for easier access and management.
  - Incorporating additional features for managing book reservations and fines.
