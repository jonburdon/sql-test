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
