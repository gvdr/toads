# Getting information out of a Database

## Using SQL(ite), R and Stencila - Laboratory activity

We are now working with the a database containing Pop music albums, artists, tracks, and awards.

## Mechanics

You can run this _toad_ either from the cloud, as we have done in lecture so far, or locally through your Rstudio.

The toad living in the cloud is here: http://open.stenci.la/?address=github://gvdr/toads/Popdapops&peers=http://cloud.stenci.la/?ticket=kiwi

To host the toad locally:
-  download the toads from here: https://github.com/gvdr/toads/archive/master.zip
-  unzip `toads-master.zip`, navigate to the `Popdapops` folder, right click on README.md and "open with Rstudio"
-  follow this instructions: https://github.com/stencila/r/blob/master/getting-started.md .

Once you have done, you can save your assignment to .pdf and submit it 

## Challenge 1

Explore the database and get an idea of it: what tables are there? which fields do they contain? what connections can you establish between tables? I provide you some code as a starter:

```sql
--!
SELECT _____
FROM sqlite_master
WHERE type is "table"
```

## Challenge 2

Answer the following questions:

Step 1. How many award did each of the artist win? Fill in the following code, selecting the variable over which to group and using the aggregation function 
`count( ... )`
:

```sql
--!
SELECT artist_name, _____
FROM awards
GROUP BY _____
```

Step 2. What is the total US sale (`us_sales`) for Eminem? You may want to use the commands `WHERE`and the aggregation function
`sum( ... )`
(it works similarly to the
`count()`
function we have seen in Step 1.)

```sql
--!
SELECT artist_name, sum(_____) AS total_us_sales
FROM albums
WHERE artist_name == _____
```

Step 3.  What is the total US sale (
`us_sales`
) for each artist? You may want to use the commands 
`GROUP BY`
and the aggregation function 
`sum( ... )`
.

```sql
--!
SELECT artist_name, sum(_____) AS total_us_sales
FROM albums
GROUP BY _____
```

### Challenge 3


Step 1.  Which artist composed the longest song in the database? This is a join operation: the table 
`tracks`
contains the song lengths (you may prefer to use 
`length_second`
for that) and the album id (
`album_id`
) for the songs; the table albums contains the album id (
`id`
) and the name of the artist. Put the following lines in the right order:

```sql
--!
LIMIT 2
ORDER BY length_seconds DESC
SELECT artist_name, length_seconds
FROM albums JOIN tracks ON albums.id == tracks.album_id
```

Step 2. What is the birth date of the artist with most awards?  You will need a proper `JOIN` operation: which two table should you join? On which field?

```sql
--!
SELECT artist_name, birthdate, count( ) AS number_of_awards
FROM _____ JOIN _____ ON _____._____ == _____._____
GROUP BY artist_name
ORDER BY number_of_awards DESC
LIMIT 2
```

Step 3. How many awards did the youngest artist win? Change the sorting from the previous code (thus, copy and paste the `JOIN` operation) to get the answer.

```sql
--!
SELECT artist_name, birthdate, count( ) AS number_of_awards
FROM _____ JOIN _____ ON _____._____ == _____._____
GROUP BY artist_name
ORDER BY ______ ____
LIMIT 2
```

Step 4. Which artist won the most awards in a single year? Group wisely!

```sql
--!
SELECT artist_name, count( ) AS number_of_awards
FROM _____ JOIN _____ ON _____._____ == _____._____
GROUP BY artist_name, _____
ORDER BY ______ ____
LIMIT 2
```

Step 5. (optional) Which artist wrote the album with most songs? You'll need a double `JOIN`, some grouping, counting and ordering. Fill in the code.

```sql
--!
SELECT artist_name, albums.release_date, ____ AS number_of_songs, albums.title
FROM artists JOIN albums ON artists.____ == albums.____
             JOIN tracks ON albums.____ == tracks.____
GROUP BY albums.____
ORDER BY ____
LIMIT 4
```

Step 6. (optional) Which artist wrote the longest album? You'll need a double `JOIN`, some grouping, summing and ordering. Fill in the code.

```sql
--!
SELECT _____________, sum(tracks.length_seconds) / 60 AS album_length_minutes
FROM artists JOIN _____________ ON ____.____ == ____.____
             JOIN _____________ ON ____.____ == ____.____
GROUP BY _____________
ORDER BY _____________
LIMIT 4
```

## Challenge 4

One step. Based on the previous guided exploration, let's try to do something automously. Think about a question you'd like to ask, and how you can solve it. The question can be simple or complex. Require one or two or more joins. It's up to you!

```sql
--!
---- your code here
```

## Challenge 5

So far we dealt with SQL. There's R as well! Data is handled, wrangled, and analysed in R in a similar way to SQL. We will use the `tidyverse` package. The _tidy_ in `tidyverse` comes from the concept of **tidy data** ([here](http://vita.had.co.nz/papers/tidy-data.html) presented by Hadley Wickham). In particular, R's tidyverse likes "dataframes". A data frame is similar to our Relational Data models: it is a collection of rows (observations) and columns (features).

In Stencila (and otherwhere) SQL and R can speak. To pass some table (or view) from SQL to R we first declare the output of an SQL query (we assign it to a variable):

```sql
--! albums5 =
SELECT artist_name, release_date, title, peak_aus
FROM albums
ORDER BY release_date DESC
LIMIT 5
```

and when we use R we offer the just declared variable (_albums5_):

```r
#! (albums5)
albums5
```

In R we can use packages (collection of data and functions that extends R abilities, tidyverse is one of those) by calling `library( ... )` and writing the name of the package inplace of the dots. Tidyverse provide similar capabilities of SQL (selecting features, filtering, sorting, ...). You can concatenate operations by using `%>%` (a "pipe" operator).

```r
#! (albums5)
library(tidyverse)
albums5 %>%
filter(peak_aus == 1) %>%
select(-release_date)
```

Here is a (incomplete) table of commands in SQL and in R's tidyverse for a quick reference. `A`, `B`, and `C` are three features of a table.

| SQL | Tidyverse |
|------|----------|
| `SELECT A, B, C` | `select(A, B, C)` |
|`WHERE A == 3` | `filter(A == 3)` |
| `FROM` | no strict equivalent, we can declare the dataframe to work on |
| `GROUP BY A, B`| `group_by(A, B)` |
| `ORDER BY A`, `ORDER BY A DESC`  | `arrange(A)`, `arrange(-A)` |
| `LIMIT 5` | `sample_n(5)` |


## Outro

In preparation for the guest lecture we are going to have on Monday, try to login to bigquery.cloud.google.com. You need a google account to do so. If you have already a gmail mail box, or an account on youtube, you do have a google account. If you don't have any, sign up for one (it's free) here: https://accounts.google.com/SignUp?service=bigquery&continue=https%3A%2F%2Fbigquery.cloud.google.com%2F