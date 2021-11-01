# Exam 98-364: Database Fundamentals – Skills 
## Audience Profile
Candidates for this exam are seeking to prove introductory knowledge of and skills with databases, including relational databases, such as Microsoft SQL Server. It is recommended that candidates be familiar with the concepts of and have hands-on experience with the technologies described here, either by taking relevant training courses or by working with tutorials and samples available on MSDN and in Microsoft Visual Studio. Although minimal hands-on experience with the technologies is recommended, job experience is not assumed for these exams.
## Skills Measured
NOTE: The bullets that appear below each of the skills measured are intended to illustrate how we are assessing that skill. This list is not definitive or exhaustive.
NOTE: In most cases, exams do NOT cover preview features, and some features will only be added to an exam when they are GA (General Availability).
# Understanding core database concepts (20–25%)
## Understand how data is stored in tables
- understand what a table is and how it relates to the data that will be stored in the database; columns/fields, rows/records
    - Tables store data. Columns/fields describe the data that is stored within the table. Rows/records are the pieces of data defined by the columns/fields.
## Understand relational database concepts
- understand what a relational database is, the need for relational database management systems (RDBMS), and how relations are established
    - Relational databases are a form of database where tables are connected to eachother through like fields. This is opposed to a Hierarchical datadase where tables are in a format similar to a file directory with each record being exclusive to its branch in the tree, or a flat-file like a CSV which strictly has a single set of columns and rows. 
## Understand data manipulation language (DML)
- understand what DML is and its role in databases
    - Data Manipulation Language is a computer language used for creating, reading, modifying, or deleting data. 
        - SELECT : Retrieves rows from the database and enables selection of one or more rows and columns from one or more tables
        - INSERT : Add one or more rows to a table or view
        - UPDATE : Changes existing data in a table or view
        - DELETE : Removes one or more rows from a table or view
        - MERGE : Performs INSERT, UPDATE, or DELETE on a table based on the results of a join with a source table
        - BULK INSERT : Imports a data file into a table or view 
## Understand data definition language (DDL)
- understand how T-SQL can be used to create database objects, such as tables and views
    - Data Defenition Language defines data structures. These statements are used to create and change the tables of a database
        - CREATE : Enables creating a item in SQL server. Examples include databases, tables, views, users, and indexes.
        - ALTER : Enables modifying an existing object. Examples include databases, tables, views, users, and indexes.
        - DROP : Drops an existing object, removing it.
        - Collations : Defines how the data in a object can be stored, retrieved, and compared.
        - ENABLE TRIGGER : Enables a DML, DDL, or login trigger.
            - A trigger is a event that runs when conditions are met that would activate the trigger.
            - DML triggers occur when a INSERT, UPDATE, or DELETE is attempted.
            - DDL triggers occur when a CREATE, ALTER, or DROP is attempted.
            - Login triggers occur during a logon event.
        - DISABLE TRIGGER : Disables a trigger.
        - RENAME : Renames an user created table in SQL Data Warehouse or a user-created table or database in Parallel Data Warehouse.
        - UPDATE STATISTICS : Updates query optimization statistics on a table or indexed view.
        - USE : Changes the database context to the specified database or database snapshot in SQL Server.
        - TRUNCATE : Used to remove multiple rows from a table or partition of a table without logging the individual row deletions.
# Create database objects (20–25%)
## Choose data types
- understand what data types are, why they are important, and how they affect storage requirements
    - Data Type is an attribute that states what kind of data an object can hold. There are many data types sorted into the following categories: 
        - Exact numerics
            - tinyint : 0 to 255 taking up 1 byte
            - smallint : -2^15 to 2^15 taking up 2 bytes
            - int : -2^31 to 2^32 or 4 bytes
            - bigint : -2^63 to 2^63 or 8 bytes
            - decimal, numeric : Fixed precision and scale numbers from 10^38+1 to 10^38-1.
            - bit : An integer that can be 1, 0, or _NULL_.
            - money, smallmoney : Accurate to a ten-thousandth. Use a period to seperate monetary units. Smallmoney is 4 bytes, money is 8 bytes
        - Approximate numerics
            - float : The mantissa of a number (The "pattern" instead of the exponent in scientific notation) with dictation for the precision and storage size. 
                - float[(n)] : n = 1 to 24 : 7 digits and 4 bytes
                - float[(n)] : n = 25 to 53 : 15 digits and 8 bytes
            - real : 7 digits of precision, the same as float(24) using 4 bytes.
        - Date and time
            - date : defines a date in sql server
            - datetimeoffset : datetime with time zone awareness
            - datetime2 : expanded datetime with user specified precision
            - smalldatetime : datetime without seconds or fractional seconds
            - datetime : data and time with fractional seconds
            - time : time of day without timezone awareness
        - Character strings
            - char : fixed-length character string. char [(n)] has a length of n = 1 to 8000 bytes
            - varchar : variable-length character string. Storage is the actual length of the data in bytes.
                - varchar [(n)] has a length of n = 1 to 8000 bytes
                - varchar [(max)] has a length of n = 1 to 2^31 - 1 bytes (2GB)
            - text : variable-length non-unicode character string. text has a maximum length of 2^31 - 1 bytes (2GB)
        - Unicode character strings
            - nchar : Fixed-length string data. nchar[(n)] n defines the string length in byte-pairs and n = 1 to 4,000 (n x 2 bytes)
            - nvarchar : Variable-length string data. nvarchar[(n)] defines the string length in byte-pairs and n = 1 to 4,000 (n x 2 bytes)
            - ntext : Variable-length Unicode data with n = 0 to 2^30-1 (n x 2 bytes)
        - Binary strings
            - binary : Fixed-length binary data with a length of n = 1 to 8,000 (n bytes)
            - varbinary : Variable-length binary data. Stores the length of the data + 2 bytes.
                - varbinary ([n]) has a length of n = 1 to 8,000 (n bytes)
                - varbinary [(max)] has a length of n = 1 to 2^31 -1 (2GB))
            - image : Variable-length binary data of 0 to 2^31 - 1 bytes (Up to 2GB). Can be used for documents and files other than images.
        - Other data types
            - cursor : A database object used to retrieve OUTPUT parameters from a stored procedure.
            - rowversion : A unique value that is updated every time a row is updated.
            - hierarchyid : variable length binary data that is used to represent a hierarchy of rows in a table.
            - uniqueidentifier : A 6-byte globally unique identifier (GUID) that is used to identify a row in a table.
            - sql_variant : stores values of various SQL Server supported data types.
            - xml : Data type that stores XML data.
            - Spatial Geometry and Geography Types: Implemented as a .NET common language runtime (CLR) type.
            - table : Used for temporary storage of a set of rows returned as the result of a table-valued function.
## Understand tables and how to create them
- purpose of tables
    - Tables contain all the data in a database in a row-and-column format.
    - A table can have up to 1024 columns. 30,000 columns if you are using SPARSE.
    - You can assign properties to a table, on columns, and use compression.
- create tables in a database by using proper ANSI SQL syntax
## Create views
- understand when to use views and how to create a view by using T-SQL or a graphical designer
    - A view is a virtual table that is used to access data in a table or another view.
    - A view acts like a filter on tables and can reference columns from other tables.
## Create stored procedures and functions
- select, insert, update, or delete data
# Manipulate data (25–30%)
## Select data
- utilize SELECT queries to extract data from one table, extract data by using joins, combine result sets by using UNION and INTERSECT
## Insert data
- understand how data is inserted into a database, how to use INSERT statements
## Update data
- understand how data is updated in a database and how to write the updated data to the database by using the appropriate UPDATE statements, update by using a table
## Delete data
- delete data from single or multiple tables, ensure data and referential integrity by using transactions
# Understand data storage (15–20%)
## Understand normalization
- understand the reasons for normalization, the five most common levels of normalization, how to normalize a database to third normal form
## Understand primary, foreign, and composite keys
- understand the reason for keys in a database, choose appropriate primary keys, select appropriate data type for keys, select appropriate fields for composite keys, understand the relationship between foreign and primary keys
## Understand indexes
- understand clustered and non-clustered indexes and their purpose in a database
# Administer a database (10–15%)
## Understand database security concepts
- understand the need to secure a database, what objects can be secured, what objects should be secured, user accounts,and roles
## Understand database backups and restore
- understand various backup types, such as full and incremental, importance of backups, 
how to restore a database