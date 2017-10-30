# SQL Cheat Sheet

### Data Types
* INTEGER a positive or negative whole number.
* TEXT a text string.
* DATE a date formatted as YYYY-MM-DD.
* REAL a decimal value.
* VARCHAR a text of string with limit.
* NULL special value that represents missing or unknown data.

### Constraints
* AUTOINCREMENT 
* PRIMARY KEY columns can be used to uniquely identify the row.
* UNIQUE columns have a different value for every row, more than once.
* NOT NULL columns must have a value.
* DEFAULT columns take an additional argument that will be the assumed value for an inserted row if the new row does not specify a value for that column.

```
CREATE TABLE celebs (
  id INTEGER PRIMARY KEY,
  name TEXT UNIQUE,
  birth TEXT NOT NULL
  death TEXT DEFAULT 'Not Applicable'
);
```

### Wildcard Character
* \* matches all.
* _ subtitute any individual character without breaking the pattern.
* % matches zero or more missing letters in the pattern (case insensitive).

### Operators WHERE clause
* = equals.
* != not equals.
* \> greater than.
* < less than.
* \>= greater than or equal to.
* <= less than or equal to.
* LIKE compare similar values.
* BETWEEN filter result within a certain range.
* AND to combine multiple conditions.
* OR evaluates each condition separately and return if either conditions are true.
* OREDER BY sortir the result.
  * ASC sort ascending.
  * DESC sort descending.
    * LIMIT specify maximum number of result.

### Aggregate Functions of GROUP BY
* COUNT() is a function that takes the name of a column as an argument and counts the number of rows where the column is not NULL.
* SUM() return all values into a column.
* MAX() return the largest value in a column.
* MIN() return the smallest value in a column.
* AVG() return average value for a column.
* ROUND() is a function that takes a column name and an integer as an argument. It rounds the values in the column to the number of decimal places specified by the integer. 

### Statements Manipulation
`CREATE TABLE <table> (<key> <type>);`

`CREATE TABLE celebs (id INTEGER, name TEXT, age INTEGER);`
> create table/relation in database

`INSERT INTO <table> (<key>) VALUES (<type>);`

`INSERT INTO celebs (id, name, age) VALUES (1, 'Justin Bieber', 21);`
> add new row/record into table/relation

`SELECT <key / wildcard> FROM <table>;`

`SELECT * FROM celebs;`
> return all query data from table/relation

`UPDATE <table> SET <key> = <value> WHERE <key> = <value>;`

`UPDATE celebs SET age = 22 WHERE id = 1;`
> change/edit existing row/records

`ALTER TABLE <table> ADD COLUMN <key> <type>;`

`ALTER TABLE celebs ADD COLUMN twitter TEXT;`
> add new column into row/records

`DELETE FROM <table> WHERE <key> IS <type>;`

`DELETE FROM celebs WHERE twitter IS NULL;`
> delete existing row/records

### Statements Queries
`SELECT DISTINCT <key> FROM <table>;`

`SELECT DISTINCT genre FROM movies;`
> filter result to return unique values

`SELECT <key / wildcard> FROM <table> WHERE <condition1> OPERATOR <condition2>;`

`SELECT * FROM movies WHERE imdb_rating > 8;`
> filter result to return value based on condition

`SELECT <key / wildcard> FROM <table> WHERE <key> OPERATOR <condition>;`

`SELECT * FROM movies WHERE name LIKE 'Se_en';`
> filter result to return value based on patter of wildcard

`SELECT <key / wildcard> FROM <table> WHERE <key> BETWEEN <condition1> OPERATOR <condition2>;`

`SELECT * FROM movies WHERE name BETWEEN 'A' AND 'J';`
> this statement filters the result set to only include movies with names that begin with letters "A" up to but not including "J".

`SELECT * FROM movies WHERE year BETWEEN 1990 AND 2000;`
> In this statement, the BETWEEN operator is being used to filter the result set to only include movies with years between 1990 up to and including 2000.

`SELECT <key / wildcard> FROM <table> WHERE <condition1> OPERATOR <condition2> OPEARTOR <condition3> OPERATOR <condition4>`

`SELECT * FROM movies WHERE genre = 'comedy' OR year < 1980;`
> at this statement, the OR operator return movies either have a genre of comedy or were released before 1980

`SELECT * FROM movies ORDER BY imdb_rating DESC LIMIT 3;`
> return result oredered by descending and limited to three

### Statements Aggregate Functions
`SELECT COUNT(*) FROM fake_apps;`
> count returned rows/records

`SELECT SUM(downloads) FROM fake_apps;`
> sum all values into downloads column

`SELECT MAX(downloads) FROM fake_apps;`
> return largest value in downloads column

`SELECT MIN(downloads) FROM fake_apps;`
> return smallest value in downloads column

`SELECT AVG(downloads) FROM fake_apps;`
> return average downloads

`SELECT price, ROUND(AVG(downloads), 2) FROM fake_apps
GROUP BY price;`
> return average downloads rounded to 2 decimal value

### Statements Multiple Table
`SELECT albums.name, albums.year, artists.name FROM albums, artists`
> column names need to be specified

`SELECT * FROM albums JOIN artists ON albums.artist_id = artists.id;`
> inner join

`SELECT * FROM albums LEFT JOIN artists ON albums.artist_id = artists.id;`
> outer join

```
SELECT
  albums.name AS 'Album',
  albums.year,
  artists.name AS 'Artist'
FROM
  albums
JOIN artists ON
  albums.artist_id = artists.id
WHERE
  albums.year > 1980;
```
> make aliases

```
DROP TABLE IF EXISTS albums;
CREATE TABLE IF NOT EXISTS albums(
  id INTEGER PRIMARY KEY, 
  name TEXT,
  artist_id INTEGER,
  year INTEGER);
```
> drop table if exists or do nothing if not exists
> create table or do nothing if not exists

```
DROP TABLE IF EXISTS albums;
CREATE TABLE IF NOT EXISTS albums(
  id INTEGER PRIMARY KEY, 
  name TEXT,
  year INTEGER,
  artist_id INTEGER,
  FOREIGN KEY(artist_id) REFERENCES artist(id)
);
```
> foreign key constraints
