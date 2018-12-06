### apache-drill

#### Introduction
* Apache Drill is a low-latency distributed query engine for large-scale datasets, including structured and semi-structured/nested data.It is capable of querying nested data in formats like JSON and Parquet and performing dynamic schema discovery.
* Apache Drill is a query engine for Big Data exploration. 
* Drill performs/ supports distributed SQL query execution.
* Apache  Drill  uses  standard  ANSI-SQL to query a variety of structured,semi-structured and unstructured data types.
* Drill makes querying semi-structured data extremely easy. 
* Drill can query multiple sources and data formates on the fly.Eg
  * JSON data 
  * Text files (cvs, psv,etc)
  * Parquet files.
  * HBase table.
  * Hive
  *

```
select blog[1],blog[2],blog[3],blog[4],
CASE WHEN LOCATE(':',blog[5]) > 0 THEN '2018' ELSE blog[5] END,
blog[6] from (select SPLIT(REGEXP_REPLACE(columns[0],'\s+','|'),'|') as blog from dfs.lfs.`siab_branches.csv`)
```
