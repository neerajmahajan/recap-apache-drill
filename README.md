### apache-drill

#### Introduction
* Apache Drill is used to query and analyse distributed data sources with SQL.
* Apache Drill is a low-latency distributed query engine for large-scale datasets, including structured and semi-structured/nested data.It is capable of querying nested data in formats like JSON and Parquet and performing dynamic schema discovery.
* Apache  Drill  uses  standard  ANSI-SQL to query a variety of structured,semi-structured and unstructured data types.
* Drill makes querying semi-structured data extremely easy. 
* Query Hadoop, relational databases, MongoDB, and Kafka with standard SQL
* Drill can query multiple sources and data formates on the fly.Eg
  * JSON data 
  * Text files (cvs, psv,etc)
  * Parquet files.
  * HBase table.
  * Hive
  
#### Parsing Text Files
* extractHeader property is false by default, which means you get all data from csv file as an array. which can extracted by columns[index]
* while enabling extractHeader property, set skipFirstLine = true.
* use .csvh format for reading cvs files if you want to include first line as header names.
* While querying text files, convert the columnn data type to integer if using numeric functions like AVG,SUM etc. otherwise drill will gives wiered error.
* If using keywords for column name, use back ticks. eg `year`, otherwise drill will give errors.
* Drill will infer data type from relational databases/ json files, but for text files everything is string.
* To convert string into numeric types use cast function
 * eg CAST (columns[0] as float)
 * See To_Number
* To convert string into dates use
 * To_date
 * To_Timestamp
 
 #### Parsing JSON Files
 
```
select blog[2] as updated_by ,blog[3] as `month` ,blog[4] as `day`,
CASE WHEN LOCATE(':',blog[5]) > 0 THEN '2018' ELSE blog[5] END as `year`,
REGEXP_REPLACE(blog[6],'/','')
as branch_name from (select SPLIT(REGEXP_REPLACE(columns[0],'\s+','|'),'|') as blog from dfs.lfs.`siab_branches.csv`)
```
