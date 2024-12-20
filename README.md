
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

Our model represents the structure of a library media management system. The core entity is the Member entity, representing individuals who can borrow media items like books, movies, and music. Each member has a Card associated with them, and this card allows them to borrow items. Since a member can have multiple cards, as some members might have expired cards attached to them, we’ve set up a one-to-many relationship between Member and Card.

Members borrow items from the library, which is tracked in the Loan table. Each Loan records details like when the media item was borrowed, when it is due, and when it was returned. Because members can borrow many media items, we established a one-to-many relationship between the Member and Loan tables. Similarly, each media item can be borrowed multiple times, so there is a one-to-many relationship between MediaItem and Loan.

The MediaItem table represents all the different items available in the library, such as books, movies, and CDs. Each media item has attributes like its title, genre, release year, and language. Media items are also organized into Sections within the library, such as Science Fiction or Romance. Each section is comprised of multiple employees, but each employee is stationed at only one section, making a one to many relationship.  For every section though, there is an employee that is the boss of that section, so we also added a one to one relationship for this dynamic.  

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

## Queries
| Feature                     | Query 1 | Query 2 | Query 3 | Query 4 | Query 5 | Query 6 | Query 7 | Query 8 | Query 9 | Query 10 |
|-----------------------------|---------|---------|---------|---------|---------|---------|---------|---------|---------|----------|
| multiple table join          |    X    |         |    X    |    X    |   X     |    X    |    X    |    X    |    X    |    X      |
| subquery                     |         |    X    |         |         |     X   |         |         |     X   |         |          |
| GROUP BY                     |    X    |         |         |    X    |     X   |    X    |     X   |         |    X    |     X     |
| GROUP BY with HAVING         |         |         |         |    X    |         |         |     X   |         |    X    |          |
| multi-condition WHERE        |         |    X    |     X    |         |         |         |         |    X    |         |     X     |
| built-in functions (AVG, COUNT) |    X    |         |         |    X    |   X    |    X    |    X     |         |    X    |   X     |
| REGEXP                       |         |         |         |         |         |         |         |         |         |     X     |
| NOT IN                       |         |    X    |         |         |         |         |         |         |         |          |

1. Query 1 lists the name, email, and number of items loaned of the member who has checked out the most media items. 
<img width="583" alt="Screenshot 2024-10-13 at 11 28 47 PM" src="https://github.com/user-attachments/assets/3fb099b2-812e-43c0-9340-184fbb2f4925">

Query 1 allows the library to see its most active members. With this information, the library can recognize these members with rewards or incentives such as priority borrowing privileges to create member loyalty and encourage activity.

2. Query 2 lists the names and emails of members who have never written a review, listed alphabetically.
<img width="512" alt="Screenshot 2024-10-13 at 11 28 59 PM" src="https://github.com/user-attachments/assets/6dbc9f91-62c4-4c43-ab93-b40a9d6094cd">

Query 2 is useful as it highlights potential opportunities for feedback improvement. By identifying passive members who haven't written a review the library can offer incentives and reminders to encourage their contribution. Improved feedback will allow the library to make more informed decisions about matters such as inventory.

3. Query 3 lists the names, expiration dates and emails of members who have cards expiring between the specified periods.
<img width="985" alt="Screenshot 2024-10-13 at 11 47 14 PM" src="https://github.com/user-attachments/assets/4bae9968-b4c5-4ccc-bf60-312096e86ed2">

Query 3 is useful as it allows the library to improve member retention. Using the information provided by the query, the library can proactively reach out to members and encourage renewals. This will reduce the risk of losing members and also improve member satisfaction as they feel more valued. Additionally, by knowing when large numbers of cards expire, the library can better forecast its financial situation, allowing for more effective budget planning.

4. Query 4 lists the average rating by genre for media that has more than four reviews.
<img width="482" alt="Screenshot 2024-10-13 at 11 29 42 PM" src="https://github.com/user-attachments/assets/5a44ea86-131e-48f6-916c-8051ecc64616">

Query 4 is useful as it can identify popular genres in the library while limiting the report to genres with substantial reviews, limiting bias. This information will allow for better resource allocation as the library can see poorly rated genres that need updated offerings and add to highly performing genres. Following these actions will improve member satisfaction and ensure a high-quality media collection throughout all genres in the library.

5.  Query 5 lists the creators who have contributed to media items in more than one genre along with how many contributions they have made.
<img width="585" alt="Screenshot 2024-10-13 at 11 29 56 PM" src="https://github.com/user-attachments/assets/981317e0-c1d7-4464-b091-a551f3791852">

Query 5 is useful as it can improve resource optimization. Identifying creators who contribute to multiple genres could be used to improve marketing efforts by promoting offerings from creators with a larger audience spread across different genres. Furthermore, the library could also seek to develop partnerships with these vital creators, giving themselves a competitive advantage over other libraries in the area.

6.  Query 6 lists the most borrowed genres by month and their respective total borrows.
<img width="528" alt="Screenshot 2024-10-13 at 11 30 10 PM" src="https://github.com/user-attachments/assets/cbd73879-a3a9-4b0f-b45b-c62236de7ba5">

Query 6 is useful in that it helps to identify borrowing trends over time. Using this information, the library can make informed decisions on what genres to promote and acquire for different periods of the year. For example, media falling under the horror genre should be prioritized during October.

7.  Query 7 lists the employees that manage more than one section and how many sections they manage in total.
<img width="569" alt="Screenshot 2024-10-13 at 11 30 21 PM" src="https://github.com/user-attachments/assets/11911ba0-03e3-4c05-90a9-0db44a6eade3">

Query 7 allows for more efficient workload distribution by highlighting employees who manage multiple sections. If section performance is at a low this could indicate that an employee is overburdened. On the other hand, if an employee is managing numerous sections and each section is performing at a high level it could indicate that this employee should be considered for a promotion.

8.  Query 8 lists the name, salary and section of employees who have a salary higher than the average salary in their section.
<img width="582" alt="Screenshot 2024-10-13 at 11 30 33 PM" src="https://github.com/user-attachments/assets/585ac31b-5383-43af-a710-835e5631432d">

Query 8 is useful in that it can be used to make compensation adjustments. If an employee is earning significantly above the average but their performance is not up to par their salary can be reduced and vice versa. Consequently, the query can be used to ensure that high-performing employees are retained via pay rises and that low-performing employees are not overpaid.

9.  Query 9 lists the names of creators who have contributed to media items that have an average rating of 4 or higher.
<img width="558" alt="Screenshot 2024-10-13 at 11 30 45 PM" src="https://github.com/user-attachments/assets/f3dea5a0-854f-41e7-a2aa-034e2733a495">

Query 9 is useful as it can be used to ensure that the library's inventory remains at a high quality. Future content acquisitions could be guided by creators whose media consistently attains high ratings, improving customer satisfaction by aligning future offerings with members' preferences.

10. Query 10 retrieves the top two most commonly used languages in media items during the years of 2023 and 2024 and the total amount of items in which the languages were used.
<img width="966" alt="Screenshot 2024-10-13 at 11 32 49 PM" src="https://github.com/user-attachments/assets/0d9452dd-0f09-48a8-99a1-a5e777f117a4">

Query 10 helps identify language preferences among users, guiding decisions about future media acquisitions. This insight can improve inventory planning by ensuring that the most in-demand languages are well-stocked, enhancing customer satisfaction. Additionally, it aids in marketing strategies by targeting promotions towards popular language groups and catering to audience preferences.

## Database Information
Name of the database: cs_ota82991

Each query listed above is stored in the database using stored procedures using the format: CALL TP_Q1();
