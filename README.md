
# MIST 4610 Project 1

## Team Name: 
MIS Avengers

CRN: 29704

## Team Members:

- Om Amin [@Om-Amin](https://github.com/Om-Amin)
- Rohit Sharma [@Rohits629](https://github.com/Rohits629)
- Aaron Jackson [@Aaronjackson3x](https://github.com/Aaronjackson3x)
- Kristen Wang [@kristennw](https://github.com/kristennw)
- Oliver Tripcony [@OliverTripcony](https://github.com/OliverTripcony)

## Problem Description:

Our library operates as a digital and physical space where members can borrow various media items, such as books, movies, and music CDs. Our library tracks media loans, reviews provided by members, and details about the creators of the media. Additionally, our system manages the internal structure of the library by organizing employees and media items into different sections. The goal is to ensure smooth library operations, including member engagement, media item management, staff allocation, and media categorization.

## Data Model Description:
Our model represents the structure of a library media management system. The core entity is the Member entity, representing individuals who can borrow media items like books, movies, and music. Each member has a Card associated with them, and this card allows them to borrow items. Since a member can have only one card, we’ve set up a one-to-one relationship between Member and Card.

Members borrow items from the library, which is tracked in the Loan table. Each Loan records details like when the media item was borrowed, when it is due, and when it was returned. Because members can borrow many media items, we established a one-to-many relationship between the Member and Loan tables. Similarly, each media item can be borrowed multiple times, so there is a one-to-many relationship between MediaItem and Loan.

The MediaItem table represents all the different items available in the library, such as books, movies, and CDs. Each media item has attributes like its title, genre, release year, and language. Media items are also organized into Sections within the library, such as Science Fiction or Romance. Each section is managed by an employee, so we have a one-to-many relationship between the Section and Employee tables, with each Employee managing one or more sections.

Members can also review media items. These reviews are stored in the Review table, which captures the member’s rating and comments about the media item. Each review is linked to both the member who wrote it and the media item being reviewed, so there is a many-to-one relationship between Review and both Member and MediaItem.

In addition, media items are created by various individuals, such as authors or directors, and this is captured by the Creator table. Since a media item can have multiple creators, and a creator can work on multiple media items, we set up a many-to-many relationship between MediaItem and Creator, represented by the MediaCreator table.

Lastly, the MediaType table helps categorize media items by type, such as books or movies. Each media item belongs to a specific type, and this helps the library manage its inventory more efficiently.

This data model allows the library to track member activity, media loans, reviews, and staff management, ensuring smooth day-to-day operations while providing valuable insights for improving member engagement and media inventory.

<img width="931" alt="Screenshot 2024-10-13 at 7 18 02 PM" src="https://github.com/user-attachments/assets/a81f5040-7db7-4392-877f-d780526ed34c">

## Data Dictionary:

### Table: `member`

| Column Name  | Description                              | Data Type | Size  | Key  |
|--------------|------------------------------------------|-----------|-------|-------|
| `idmember`   | PK; unique identifier for each member    | INT       | 11    | PK    |
| `memberName` | Name of the member                       | VARCHAR   | 80    |       |
| `email`      | Email of the member                      | VARCHAR   | 85    |       |
| `Address`    | Address of the member                    | VARCHAR   | 85    |       |

---

### Table: `card`

| Column Name       | Description                              | Data Type | Size  | Key  |
|-------------------|------------------------------------------|-----------|-------|-------|
| `idCard`          | PK; unique identifier for each card      | INT       | 11    | PK    |
| `issue_date`      | Date the card was issued                 | DATE      |       |       |
| `expiration_date` | Date the card expires                    | DATE      |       |       |
| `idmember`        | FK; links to member                      | INT       | 11    | FK    |
| `status`          | Status of the card (e.g., Active, Expired)| VARCHAR   | 45    |       |

---

### Table: `loan`

| Column Name       | Description                              | Data Type | Size  | Key  |
|-------------------|------------------------------------------|-----------|-------|-------|
| `idloan`          | PK; unique identifier for each loan      | INT       | 11    | PK    |
| `loanDate`        | Date the media item was borrowed         | DATE      |       |       |
| `returnedDate`    | Date the media item was returned         | DATE      |       |       |
| `expectedDueDate` | Expected return date of the media item   | DATE      |       |       |
| `idmember`        | FK; links to the member who borrowed     | INT       | 11    | FK    |
| `idmediaItem`     | FK; links to the media item borrowed     | INT       | 11    | FK    |

---

### Table: `mediaItem`

| Column Name    | Description                              | Data Type | Size  | Key  |
|----------------|------------------------------------------|-----------|-------|-------|
| `idmediaItem`  | PK; unique identifier for each media item| INT       | 11    | PK    |
| `title`        | Title of the media item                  | VARCHAR   | 45    |       |
| `release_year` | Release year of the media item           | DATE      |       |       |
| `language`     | Language of the media item               | VARCHAR   | 45    |       |
| `idsection`    | FK; section where the media item belongs | INT       | 11    | FK    |
| `idType`       | FK; type of media item (book, movie, etc.)| INT       | 11    | FK    |
| `genre`        | Genre of the media item                  | VARCHAR   | 45    |       |

---

### Table: `review`

| Column Name   | Description                              | Data Type | Size  | Key  |
|---------------|------------------------------------------|-----------|-------|-------|
| `idReview`    | PK; unique identifier for each review    | INT       | 11    | PK    |
| `rating`      | Rating given to the media item           | INT       |       |       |
| `reviewText`  | Text of the review                       | TEXT      | 200   |       |
| `idmediaItem` | FK; media item being reviewed            | INT       | 11    | FK    |
| `idmember`    | FK; member who wrote the review          | INT       | 11    | FK    |

---

### Table: `mediaType`

| Column Name  | Description                              | Data Type | Size  | Key  |
|--------------|------------------------------------------|-----------|-------|-------|
| `idType`     | PK; unique identifier for media type     | INT       | 11    | PK    |
| `Description`| Description of the media type (e.g., book, movie) | VARCHAR   | 45    |       |

---

### Table: `section`

| Column Name         | Description                              | Data Type | Size  | Key  |
|---------------------|------------------------------------------|-----------|-------|-------|
| `idsection`         | PK; unique identifier for each section   | INT       | 11    | PK    |
| `sectionName`       | Name of the section (e.g., Sci-Fi, Romance) | VARCHAR   | 45    |       |
| `employee_idemployee`| FK; employee managing the section        | INT       | 11    | FK    |

---

### Table: `employee`

| Column Name   | Description                              | Data Type | Size  | Key  |
|---------------|------------------------------------------|-----------|-------|-------|
| `idemployee`  | PK; unique identifier for each employee  | INT       | 11    | PK    |
| `employee_Name`| Name of the employee                    | VARCHAR   | 45    |       |
| `position`    | Position of the employee (e.g., Librarian, Manager)| VARCHAR   | 45    |    |
| `salary`      | Employee’s salary                        | INT       |       |       |
| `idSection`   | FK; section managed by the employee      | INT       | 11    | FK    |

---

### Table: `creator`

| Column Name   | Description                              | Data Type | Size  | Key  |
|---------------|------------------------------------------|-----------|-------|-------|
| `idCreator`   | PK; unique identifier for each creator   | INT       | 11    | PK    |
| `creator_fname`| First name of the creator               | VARCHAR   | 45    |       |
| `creator_lname`| Last name of the creator                | VARCHAR   | 45    |       |
| `typeCreator` | Type of creator (e.g., author, director) | VARCHAR   | 45    |       |

---

### Table: `mediaCreator`

| Column Name  | Description                              | Data Type | Size  | Key  |
|--------------|------------------------------------------|-----------|-------|-------|
| `idmediaItem`| FK; media item linked to the creator     | INT       | 11    | FK    |
| `idCreator`  | FK; creator linked to the media item     | INT       | 11    | FK    |
|              | PK; composite key of both `idmediaItem` and `idCreator` |          |    | PK    |

---

## Database Information on Queries
| Feature                     | Query 1 | Query 2 | Query 3 | Query 4 | Query 5 | Query 6 | Query 7 | Query 8 | Query 9 | Query 10 |
|-----------------------------|---------|---------|---------|---------|---------|---------|---------|---------|---------|----------|
| multiple table join          |    X     |         |    X    |    X    |         |    X    |    X    |         |    X    |          |
| subquery                     |         |    X    |         |         |         |         |         |         |         |          |
| GROUP BY                     |    X    |         |         |    X    |         |    X    |    X    |         |    X    |          |
| GROUP BY with HAVING         |         |         |         |    X    |         |         |    X    |         |    X    |          |
| multi-condition WHERE        |         |    X    |     X    |         |         |         |         |         |         |          |
| built-in functions (AVG, COUNT) |    X    |         |         |    X    |         |    X    |         |         |    X    |          |
| REGEXP                       |         |         |         |         |         |         |         |         |         |          |
| NOT EXISTS                   |         |        |         |         |         |         |         |         |         |          |
