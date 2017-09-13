# Diving into a Database

## Using SQL(ite), R and Stencila

We will be working with the [San Francisco Restaurant Health Inspections](http://2016.padjo.org/tutorials/sqlite-data-starterpacks/#more-info-san-francisco-restaurant-health-inspections "null") database.

We read from its description: "The San Francisco Dept. of Public Health’s database of eateries, inspections of those eateries, and violations found during the inspections."

Let's start by querying the `sqlite_master` (present in every sqlite database) table to get a list of the tables in the database,

```sql
--!
SELECT * FROM sqlite_master
```

Which are the businesses committing the most violations? Let's count the number of violation for business using SQL and then plot the result in R:

```sql
--! violation_per_business =
SELECT *, count(ViolationTypeID) AS number_crimes
FROM violations
GROUP BY business_id
```

```r
#! (violations_per_business)
library(dplyr)
violations_per_business %>%
filter(number_crimes > 30) %>% 
ggplot(aes(x=reorder(business_id, -number_crimes), y=number_crimes)) +
  geom_bar(stat='identity')```
