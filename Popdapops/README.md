# Getting information out of a Database

## Using SQL(ite), R and Stencila - Second Lecture

We are now working with the a database containing Pop music albums, artists, tracks, and awards.

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

1.  How many award did each of the artist win? Fill in the following code, selecting the variable over which to group and using the aggregation function 

    `count()`

    :

```sql
--!
SELECT artist_name, _____
FROM awards
GROUP BY _____
```

2.  What is the total US sale (

    `us_sales`

    ) for Eminem? You may want to use the commands 

    `WHERE`

     and the aggregation function 

    `sum( ... )`

     (it works similarly to the 

    `count()`

     function we have already seen.)

3.  What is the total US sale (

    `us_sales`

    ) for each artist? You may want to use the commands 

    `GROUP BY`

     and the aggregation function 

    `sum( ... )`

    .

### Challenge 3


1.  Which artist composed the longest song in the database? This is a join operation: the table 

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