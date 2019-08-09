KSDB Readme

Kirchner Solutions Database Solution

2019 Kirchner Solutions
kirchnerbusinesssolutions.com

Robert Kirchner JR

#################################################################################

Table of Contents

    1. Introduction
        A. TablePage Technology
        B. Indexing

    2. Deployment
        A. Boot
        B. Initialization
        C. Startup Scripting

    3. Use
        A. Syntax
            a. Script Tags
        B. Results
        C. Terminal
        D. Connector

#################################################################################

1. Introduction

KSDB is the initial proof of concept for Kirchner Solutions easy-to-use,
easy-to-manage, fast, reliable, light-weight and scalable production optimizing
data solution.

#################################################################################

A. TablePage Technology

---------------------------------------------------------------------------------

Traditional databases store data, in what grows to be, very large tables.
In our search to optimize data warehousing, we developed the concept
of taking what would be a large table, and breaking it into many smaller
tables, that capitalizes on multi-threading technology, and allows each
table page to be searched and manipulated concurrently.

#################################################################################

B. Indexing

---------------------------------------------------------------------------------

Unlike traditional data solutions, our indices are an actual address to the
physical address to the data. Indices in our solutions are generated,
managed and assigned by the program internally.

In the event that you are using a very large dataset, and require faster
seek times, you can choose to index column's within a table. Indexed fields
are stored in memory, and mapped to indices with a binary search tree.
Indexing is a trade-off between CPU work and available memory.

#################################################################################

2. Deployment

KSDB is engineered to be easy to use, maintain, and deploy. KSDB gives you
absolute control of your data without the need of expensive IT staff.

#################################################################################

A. Boot

---------------------------------------------------------------------------------

KSDB comes with several .bat boot scripts for windows users. The scripts vary
in the amount memory reserved for the application. Depending on size, scale
and availability requirements, you may need to allocate more memory to our
data warehouse. It is best practice to allocate as much memory a possible,
especially if your data will be heavily indexed.

For linux and advanced users, KSDB can be called from a terminal console
using the java -jar command with xms and xmx arguments. The jar comes in
seperate Windows and linux binaries.

#################################################################################

B. Initialization

---------------------------------------------------------------------------------

By default, KSDB creates a User and Transaction table on first boot. A default
root user is created as well.

Username: root
Password: password

It is very strongly recommended that you change the root user password and
create a separate admin user.

#################################################################################

C. Startup Scripting

---------------------------------------------------------------------------------

On every boot, KSDB will look for a file named startup.dbs in the Database/scripts
directory. You can add separate commands(Covered in the syntax section) on each
line. The script will be executed on boot, deleted and KSDB will load.

#################################################################################

3. Use

KSDB is designed to much simpler and intuitive than a traditional alternative.
Using a simple query language, KSDB will be easy to to learn and use.

#################################################################################

A. Syntax

---------------------------------------------------------------------------------

KSDB uses several data types:
    1. String(Text) -s
    2. Integer      -i
    3. Decimal      -d
    4. List         -l

A dash and the first letter of the data type must be appended to the end
of each columm name(ie username-s).

Below are the currently supported release command forms:

QUERY CONTAINS FROM TABLE tablename field1:value1,fieldn:valuen
    Query data from the given data that contains value
QUERY CONTAINS FROM TABLE SORTBY fieldname tablename field1:value1,fieldn:valuen
    The same as above but sorted by field fieldname
SET INDEXES FOR tablename indexedFieldname1<br>indexedFieldnamen
    Set indices for table by the given columm names
QUERY ROW FROM TABLE tableName field1:Value1,fieldn:Value,n
    Query the last row from table that matches give arguments
QUERY ROWS FROM TABLE tableName Field:Value,Field:Value,n
    Query all rows from table that mach given arguments
QUERY ROWS FROM TABLE SORTBY fieldname tableName Field:Value,Field:Value,n
    Same as above sorted by given columm name
CREATE TABLE tableName Field1:Field2:Fieldn
    Create new table with given columms and data types
CREATE ROW IN TABLE tableName row1Field1:value1,Fieldn:valuen<>rownField1:value1,Fieldn:valuen
    Create a new row in table with given values
DELETE TABLE tableName
    Delete given table
EXPORT TABLE tableName AS CSV File//dir
    Export table as CSV to given path
DELETE ROW FROM TABLE tableName rowIndex1:rowIndexn
    Delete rows with given indices from table
EXISTS TABLE tablename
    Returns true if given table exists
GET ALL ROWS FROM TABLE tablename
    Returns all rows from given table
GET ALL ROWS FROM TABLE SORTBY fieldname tablename
    Same as above sorted by given columm name
GET EXCEPTION LOGS
    Returns all recorded exception logs

---------------------------------------------------------------------------------

a. Script tags

Startup scripts can contain the following command types along with the following
tags:
    <c>:     Wrap a value with this tag to insert current time.
    <hash>:  Wrap a value with this tag to insert the SHA-256 hash of this value.

#################################################################################

B. Results

---------------------------------------------------------------------------------

Results from a given command are returned as a single String of text
separated by the given tags:

<br>     field name break(Separates columm name from actual value)
<brl>    list break(Separates items in a list)
<brf>    row field break(Separates columms in given results)
<brrl>   row break(Separates rows in given results)

#################################################################################

C. Terminal

---------------------------------------------------------------------------------

You can log into a shell session in a running KSDB terminal window. Below are
the currently supported release terminal commands:

-h = help
-q COMMAND = run query
-l = logoff
-s = stats
-t = tables
-c = current sessions
-c -p = print current sessions
-c -bs SID= boot session by sid SID
-c -bu userName = boot session by usernamer userName
-c -bi ipAddress = boot session by ip ipAddress
-c -bp port = boot session by port port
-clean = clean all caches.
-shutdown = shutdown.
-reboot = Reboot.

#################################################################################

D. Connector

---------------------------------------------------------------------------------

KSDB can be used with any java program by importing the KSDBConnector API
jar.

The connector provides one easy to use public class:
    kirchnersolutions.database.connector.Connector

A user session is initialized with the following constructors:
    Connector(String username, String password, String KSDB ip, int KSDBport)

    Connector(String username, BigInteger password, String KSDB ip, int KSDBport)
        Where password is the BigInteger representation of the SHA-256
            password hash.

Connector has three public methods:

     public void start() throws IllegalArgumentException
        Starts KSDB session on a new thread(Must be called first).

     public String queryDB(String query) throws IllegalArgumentException
        Returns the results of a given command argument.

     public String consoleDB(String query) throws IllegalArgumentException
        Allows a remote user to run any of the supported terminal
            arguments.

#################################################################################

KSDB is a working proof of concept that is the footing for our upcomming product:

    JavaByte: Modern Database Solution

JavaByte will be a fully functional relational database engineered on the core
technologies proven in KSDB packaged as a boot jar web application.

Report bugs or request features at:
    kirchnerbusinesssolutions.com/bugs/report
or email:
    support@kirchnerbusinesssolutions.com

To support future free program development, become a Patreon
    https://www.patreon.com/kirchnersolutions