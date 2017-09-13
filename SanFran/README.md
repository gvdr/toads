# Diving into a Database

## Using SQL(ite), R and Stencila

We will be working with the [San Francisco Restaurant Health Inspections](http://2016.padjo.org/tutorials/sqlite-data-starterpacks/#more-info-san-francisco-restaurant-health-inspections "null") database.

We read from its description: "The San Francisco Dept. of Public Health’s database of eateries, inspections of those eateries, and violations found during the inspections."

Let's start by querying the `sqlite_master` (present in every sqlite database) table to get a list of the tables in the database,

```sql
--!
SELECT * FROM sqlite_master
```

What are the most common first letters for album titles? Let's count the number of albums having each first letter using SQL and then plot the result in R:

```sql
--! albums_per_letter =
SELECT substr(Title,1,1) AS Letter, count(AlbumId) AS Albums
FROM Album
GROUP BY Letter
```

```r
#! (albums_per_letter)
ggplot(albums_per_letter, aes(x=Letter, y=Albums)) + geom_bar(stat='identity')
```
