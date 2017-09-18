# Getting information out of a Database

## Using SQL(ite), R and Stencila - Second Lecture

We are still working with the [San Francisco Restaurant Health Inspections](http://2016.padjo.org/tutorials/sqlite-data-starterpacks/#more-info-san-francisco-restaurant-health-inspections "null") database.

Refer to the previous lecture or its website for more context about it.

Let's start by querying the `sqlite_master` (present in every sqlite database) table to get a list of the tables in the database:

```sql
--!
SELECT name
FROM sqlite_master
WHERE type is "table"
```

The information is stored in three tables, we can get a name of their features looking at the sql column.

```sql
--!
SELECT name, sql
FROM sqlite_master
WHERE type == "table"
```

We'd like to know which Postal Codes correspond to a higher number of violations. The question is not so simple, as we have to consider a number of things that may bias the result. Let's start with a quick and dirty answer. And let's build it bit by bit.

The table _businesses_ is where the postal code are. Let's take a look at the first 10 rows (remember: order is pretty much random):

```sql
--!
SELECT postal_code
FROM businesses
LIMIT 10
```

The violations are in the _violations_ table, categorized by _ViolationsTypeID_. Complete the following code to obtain them

```sql
--!
SELECT _________
FROM violations
LIMIT 10
```

Always from the _violations_ table, we can count the number of violation per business. To do it you need to use the count() aggregation function and to group the observations adequately:

```sql
--!
SELECT ________ AS number_violations, Business_ID
FROM violations
GROUP BY ________
LIMIT 10
```

Notice how we used the sql command &amp;quot;AS&amp;quot; to give a name to the feature we just computed. To obtain the number of violation per postal code, we may want to proceed in a similar way (grouping and counting). However, the informationation is not all in one table.

Therefore, the following _can not_ work because _postal_code_ is not in _violations_.

```sql
--!
SELECT postal_code, count() as number_violations
FROM violations
GROUP BY postal_code
LIMIT 10
```

What we need is _JOIN_ operation: we need to connect the two table. This the first _set operation_ we encounter, and it's where stuff becomes interesting! We JOIN the tables _violations_ and _businesses_. In order to do so, we need to specify which feature we use to link the tables. We can do it with _USING_

```sql
--!
SELECT postal_code, count() as number_violations
FROM violations JOIN businesses USING (______)
GROUP BY postal_code
LIMIT 10
```

Now, let's git to it a good look, removing wrong postal codes (either null or &amp;quot;00000&amp;quot;) and sorting the observation in descending order of number of violations.

The following code is scrambled, put the lines in order so to obtain a working code.

```sql
--!
LIMIT 10
WHERE postal_code IS NOT NULL AND postal_code IS NOT "00000"
FROM violations AS v JOIN businesses as b USING (business_id)
GROUP BY postal_code
SELECT postal_code, count() as number_violations
ORDER BY number_violations DESC
```

For the curious, that's here: [https://goo.gl/maps/28p8YF9uB6M2](https://goo.gl/maps/28p8YF9uB6M2 "null")

For the next part, we'll focus on the interaction between R and SQL (through stencila).

```r
#!
library(dplyr);
```