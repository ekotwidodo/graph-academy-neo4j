## Chapter 04: Importing CSV Data into Neo4j

When importing data into Neo4j, we have typically a set of source files that were obtained from: RDBMS, Web APIs, Public data directories, BI tools, and Excel. 
The file types are in CSV, JSON, XML, etc.

Some preparations for importing data:
1. Understand the data in the CSV files
2. Inspect and clean (if necessary) the data in the source data files
3. Create or understand the graph data model we will be implementing during the import

### Understand the data in the CSV files, then inspect and clean it

To import CSV data into Neo4J, there are some inspections that we should do:
- **Step 1: Acquire or download the CSV**

  If the CSV file is a URL, we can simply download it in a Web browser and save it locally.
  
- **Step 2: Determine the delimiter**

  We should view the contents (at least the beginning rows) of the file to determine the delimiter.

  Here are the examples for `movies.csv` and `ratings.csv` that have delimiter `COMMA`.
  
  ![Example of the CSV file `movies.csv`](https://raw.githubusercontent.com/neo4j-graphacademy/importing-data/main/modules/1-preparing/lessons/3-inspect-clean-data/images/file-in-editor.png)

- **Step 3: Determine if headers match fields**

  Depending on the length of each row, it may be hard to determine if the values for fields look consistent.
  With a CSV file, we can open it in a spreadsheet to understand the data a little better.
  
  **Important:** By default all of these fields in each row will be read as string types.
  
- **Step 4: Determine if all data is readable**

  We have to make sure that all records can be read from the CSV file without error.
  
  Here is the Cypher code that will read all data in a CSV file that contains headers and is specified as a URL:
  
  ```cypher
  LOAD CSV WITH HEADERS
  FROM 'https://data.neo4j.com/importing/ratings.csv'
  AS row
  RETURN count(row)
  ```
  
- **Step 5: Is the data clean?**

  Here are some additional things that you will check before you begin working with the data, depending on the data:
  * Are quotes used correctly?
  * If an element has no value will an empty string be used?
  * Are UTF-8 prefixes used (for example \uc)?
  * Do some fields have trailing spaces?
  * Do the fields contain binary zeros?
  * Understand how lists are formed (default is to use colon(:) as the separator.
  * Any obvious typos?

### Understanding the data model

In the last course (third course: Graph data modeling fundamentals), we learned that the stakeholders of our application must agree upon the important use cases for the application
and design the graph data model to optimize the key queries of the application.

Here is the graph data model that we will use:

![The Graph data model that we will use in this course](https://raw.githubusercontent.com/neo4j-graphacademy/importing-data/main/modules/1-preparing/lessons/5-data-model/images/movie-data-model-import-csv.png)

In the following module, we are going to load data into an empty graph from the CSV files to conform to the graph data model.


**Sources:**
[Importing CSV Data into Neo4j](https://graphacademy.neo4j.com/courses/importing-data)
