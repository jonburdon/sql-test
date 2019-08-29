### SQL learning project

##Project aims
1. Learn sql commands


### Setup
- type **mysql --version** to check version
- use **brew install mysql** if needed
- type **mysql ctl start** to start mysql

install msssql extension
Press Ctrl+Shift+P or F1 to open the Command Palette.

Type sql to display the mssql commands, or type sqlcon, and then select MS SQL: Connect from the dropdown.


# SQL language learning project
Learning project to query a sample database, following Code Institute tutorial.


## Project Aims
* Demonstrate sql functions using a sample database

## Developer Aims
1. Learn the SQL statement syntax
2. Learn the SQL clause syntax
3. Learn the SQL aggregate function syntax
4. Document syntax covered in this project in this file.

## Approach
Sample data downloaded using wget https://raw.githubusercontent.com/Code-Institute-Org/mysql-fix/master/createuser.sh && source ./createuser.sh
Then database created using sudo mysql < Chinook_MySql_AutoIncrementPKs.SQL

### Syntax covered
**basics**
Type **use Chinook** to use the sample database.

Use **show tables;** to show the tables in Chinook

**select**

Specifies the fields we want to see in a specific table.

select Name from Artist;

select Firstname, Lastname from Customer;

select * from Track limit 15;

# **where** clause
- Used to filter and select all columns, but only the rows with a particular attribute.
- Eg select all U2 tracks using  **select * from Track where Composer = 'U2';**
- Eg select Album using **select * from Album where AlbumId = 232;**
- Eg select Employees who are IT staff using **select FirstName, LastName, Title from Employee where title = 'IT Staff';**
-
# **join** Used to select data from different tables.

 Eg select * from Track

 **select * from Track INNER JOIN Album on Track.AlbumId = Album.AlbumId limit 5;** to select Track and AlbumId.

 Join adds the data from the Album table.

 Select * from Track limit 5;

 **select Name, Title, ArtistId from Track Inner Join Album on Track.AlbumId = Album.AlbumId limit 5;** to display only three columns.

Use Alias to name data easier to understand **Select Name as Track, Title as Album, ArtistId from Track INNER JOIN Album on Track.AlbumId = Album.AlbumId limit 5;**


**select Track.Name as Track, Title as Album, Album.ArtistId, Artist.Name as Artist from Track

    -> INNER JOIN Album on Track.AlbumId = Album.AlbumId

    -> INNER JOIN Artist on Album.ArtistId = Artist.ArtistId limit 5;**




 Joins Album

 A Where clause can be used in a join command.

 eg **SELECT Track.Name as Track, Title as Album, Artist.Name as Artist FROM Track INNER JOIN Album on Track.AlbumId = Album.AlbumId INNER JOIN Artist on Album.ArtistId = Artist.ArtistId WHERE Artist.Name = "U2" limit 5;**

 Note: WHERE can have two clauses joined with AND

 Other example of joining:

 SELECT Track.Name, MediaType.Name FROM Track 

    -> INNER JOIN MediaType on Track.MediaTypeId = MediaType.MediaTypeId limit 5;


 Example selecting the Genre metal using GenreId to join:

 **SELECT Track.Name, Genre.Name FROM Track INNER JOIN Genre on Track.GenreId = Genre.GenreId WHERE Genre.Name = "Metal"limit 5;**



 Join MediaType AND Genre to Track Name:

 SELECT Track.Name, MediaType.Name, Genre.Name FROM Track

    -> INNER JOIN MediaType on Track.MediaTypeId = MediaType.MediaTypeId

    -> INNER JOIN Genre on Track.GenreId = Genre.GenreId

    -> limit 5;

 Join genre and mediatype to name and filter by genre:

SELECT Track.Name, MediaType.Name, Genre.Name FROM Track INNER JOIN MediaType on Track.MediaTypeId = MediaType.MediaTypeId INNER JOIN Genre on Track.GenreId = Genre.GenreId WHERE MediaType.Name = 'Protected AAC audio file' AND Genre.Name = 'Soundtrack';

# ORDER

**SELECT * FROM Album**

**ORDER BY Title desc;**

Or sort by ArtistId and then by title:

**SELECT * FROM Album ORDER by ArtistId, Title asc limit 5;**

Join and Order:

SELECT Track.Name, Album.Title FROM Track INNER JOIN Album on Track.AlbumId = Album.AlbumId ORDER BY Album.Title, Track.Name limit 10;

SELECT InvoiceDate, BillingCity, Total FROM Invoice

    -> ORDER By Total desc

    -> LIMIT 5;


SELECT EmployeeId, LastName, FirstName, HireDate from Employee ORDER By HireDate desc limit 3;

SELECT 

    concat(Customer.FirstName, " ", Customer.LastName) as Name,

    Invoice.InvoiceDate as Date,

    Invoice.Total

FROM Invoice

INNER JOIN Customer ON Invoice.CustomerId = Customer.CustomerId

ORDER BY Total DESC

LIMIT 10;

### COUNT functions

To count number of rows in customer table:

**SELECT COUNT(*) FROM Customer;**

Filtering can be used with WHERE clause. Eg:

**SELECT COUNT(*) FROM Customer**

**WHERE FirstName = "Frank";**

To find out how may customers Jane is the sales agent for (using JOIN):

**SELECT Employee.FirstName AS Employee, COUNT(Customer.FirstName) AS Customer FROM Employee**
**JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId**
**WHERE Employee.FirstName = "Jane";**

Reminder about JOIN syntax:
* Example: **JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId**
* Joins Customer table using the column Support Rep Id
* Joins it to Employee table using EmployeeId column
* Employee.Firstname can then be referred to in the following syntax:
* **SELECT Employee.FirstName AS Employee, COUNT(Customer.FirstName) AS Customer FROM Employee**
* NOTE: Alias is used to refer to Employee.FirstName AS Employee

Further example of COUNT:

**SELECT COUNT(*) FROM Track**
**WHERE MediaTypeId = 1;**


## MIN FUNCTION

Look at all the values in a specified column and return the minimum

EG:

**SELECT MIN(LastName) FROM Customer;**

**SELECT MIN(BirthDate) FROM Employee;**

## MAX FUNCTION

Similarly MAX finds that last (alphabetically) or largest (numerically) in a column.

Eg:

**SELECT MAX(LastName) FROM Customer;**
**SELECT MAX(HireDate) FROM Employee;**

## AVG function

Finds the Average in a column eg totals in invoice table:

**SELECT AVG(Total) FROM Invoice;**
**SELECT AVG(Milliseconds) FROM Track;**

## ROUND function

Eg.

**SELECT ROUND(AVG(Total), 2) FROM Invoice;**
**SELECT ROUND(AVG(Milliseconds), 2) FROM Track;**

## SUM Function

**SELECT TOTAL FROM Invoice WHERE InvoiceId = 2;**

Could be calculated using SUM as follows:

**SELECT SUM(UnitPrice * Quantity) FROM InvoiceLine**
**WHERE InvoiceId = 2;**

##GROUP BY clause

Allows aggregate functions ro be applied to subsets of records within a result, rather than to all records.

**SELECT COUNT(*) AlbumTracks FROM Track**
**    GROUP BY AlbumId;**

Doesn't show which album this is for so ...

**SELECT Album.Title, COUNT(*) FROM Track**
**INNER JOIN Album ON Track.AlbumId = Album.AlbumId**
**GROUP BY Track.AlbumId limit 10;**

Reminder on JOIN: Join Album table to Track Table using the AlbumId column

Select the Title Column from the Album table.
'Join with the Album table by using the Track.AlbumId column which matches the Album.AlbumId column'

GROUP Essentially collapses a group of rows in to one row.

Aggregate functions work as before.

Eg

**SELECT AlbumId, MIN(UnitPrice) FROM Track**
**GROUP BY AlbumId limit 10;**

To find total cost of each Album:

**SELECT AlbumId, ROUND(SUM(UnitPrice), 2) FROM Track**
**GROUP BY AlbumId limit 5;**

To join album title:

**SELECT Album.Title, ROUND(SUM(UnitPrice), 2) AS TotalCost FROM Track**
**INNER JOIN Album ON Track.AlbumId = Album.AlbumId**
**GROUP BY Track.AlbumId limit 5;**

Further Examples:

**SELECT COUNT(city) AS Customers_In_Berlin FROM Customer WHERE city = "Berlin";**

**SELECT SUM(InvoiceLine.UnitPrice * InvoiceLine.Quantity), Track.Name AS Track FROM InvoiceLine**
**JOIN Track ON InvoiceLine.TrackId = Track.TrackId**
**WHERE Track.Name = "The Woman King";**

**SELECT Artist.Name AS Artist, COUNT(Track.TrackId) AS Track FROM Artist**
**JOIN Album ON Artist.ArtistId = Album.ArtistId**
**JOIN Track ON Album.AlbumId = Track.AlbumId**
**GROUP BY Artist.Name**
**ORDER BY COUNT(Artist.Name)**
**DESC LIMIT 5;**

### Note: Track table has AlbumId but NOT ArtistId so we join twice, first joining Artist to Album so then we can join Album to Track.

## INSERT Statement

Used to add nee data to database.

A Statement consists of the Table we want to insert into, the columns within that table that we want to insert in to and the values for those columns.

**INSERT INTO MediaType (Name)**
**VALUES ("Test Media Type 1");**

Note: The Id is created automatically.

Note: Doing the same thing repeatedly will just create the same thing several times.

To insert a new U2 Album, knowing that their ArtistId is 150:

**INSERT INTO Album (Title, ArtistId)**
**VALUES ("Boy", 150);**

Use **select * from Album WHERE ArtistId = 150;** to check.

To insert Track Names:

INSERT INTRO Track (column1, column2, column3)
VALUES ("somedata", 150, 0.99);

INSERT INTO Track(Name, AlbumId, MediaTypeId, GenreId, Composer, Milliseconds, Bytes, UnitPrice)
VALUES();

Currently the Album Boy has no tracks, verified by **select * from Track WHERE AlbumId = 348**

Find the foreign keys by querying those tables:

SELECT AlbumId FROM Album WHERE Title = "Boy"; - result is 348

SELECT MediaTypeId FROM MediaType Where Name = "Protected AAC audio file"; - result is 2

SELECT GenreId FROM Genre WHERE Name = "Rock"; - result is 1

eg To Insert a track:

**INSERT INTO Track(Name, AlbumId, MediaTypeId, GenreId, Composer, Milliseconds, Bytes, UnitPrice)**
**VALUES("I Will Follow", 348, 2, 1, "U2", 220000, 1234, 0.99);**

Used https://en.wikipedia.org/wiki/Boy_(album) as source for data.

**INSERT INTO Track(Name, AlbumId, MediaTypeId, GenreId, Composer, Milliseconds, Bytes, UnitPrice)**
**VALUES("Bonus Track with Guest Artist Jon Burdon", 348, 2, 1, "U2", 220000, 1234, 0.99);**

