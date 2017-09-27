# School performances and Poverty in California

This example implements the [California School SAT Performance and Poverty Data](http://2016.padjo.org/tutorials/sqlite-data-starterpacks/#toc-simplefolks-for-simple-sql "null") which offers information about schools in California, their SAT performance, and economic information (Free-or-Reduced-Price Meal eligibility). 

### Usual intro:

As usual, we start by querying the `sqlite_master` table to get a list of the tables in the database,

```sql
--!
SELECT name, sql FROM sqlite_master WHERE type='table'
```

Notice that this is rather large dataset, with many columns. An explanation of the feature meanings is offered for the [schools](http://www.cde.ca.gov/ds/si/ds/fspubschls.asp), [sat scores](http://www.cde.ca.gov/ds/sp/ai/glossarysat2016.asp), and the [Free-or-Reduced-Price Meal](http://www.cde.ca.gov/ds/sd/sd/fsspfrpm.asp) tables.

### Instructions

To work on this file either use the given online [url](http://open.stenci.la/?address=github://gvdr/toads/SchoolCal&peers=http://cloud.stenci.la/?ticket=kiwi) or download it (together with the database) and open it with stencila from Rstudio.

*  Try to understand what's in the database
*  Create (either with some software or with pen and paper) a diagram of the tables and their possible relationships.
*  Take a look at some row of data, to get a taste of what they contain.
*  Use R to produce some exploratory plot
*  Formulate a question about the data and try to answer using some SQL queries (and some R code, if you dare)
*  Don't hesitate to ask me or one of the TAs for help!

## It's up to you now:

Remember to use the free form text to document what you are trying to achieve with the code!

```sql
--!

```
