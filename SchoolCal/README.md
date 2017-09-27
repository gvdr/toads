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

To work on this file either use the given online url () or download it (together with the database) and open it with stencila from Rstudio.