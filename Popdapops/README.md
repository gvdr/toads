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

Step 2. 

## Outro

In preparation for the guest lecture we are going to have on Monday, try to login to bigquery.cloud.google.com. You need a google account to do so. If you have already a gmail mail box, or an account on youtube, you do have a google account. If you don't have any, sign up for one (it's free) here: https://accounts.google.com/SignUp?service=bigquery&continue=https%3A%2F%2Fbigquery.cloud.google.com%2F