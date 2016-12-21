# SQLite

SQLite is a relational database management system contained in a C programming library.

In contrast to many other database management systems, SQLite is not a client–server database engine.

Rather, it is embedded into the end program.

## CLI

```
sqlite> .help
.backup ?DB? FILE      Backup DB (default "main") to FILE
.bail ON|OFF           Stop after hitting an error.  Default OFF
.databases             List names and files of attached databases
.dump ?TABLE? ...      Dump the database in an SQL text format
                         If TABLE specified, only dump tables matching
                         LIKE pattern TABLE.
.echo ON|OFF           Turn command echo on or off
.exit                  Exit this program
.explain ?ON|OFF?      Turn output mode suitable for EXPLAIN on or off.
                         With no args, it turns EXPLAIN on.
.header(s) ON|OFF      Turn display of headers on or off
.help                  Show this message
.import FILE TABLE     Import data from FILE into TABLE
.indices ?TABLE?       Show names of all indices
                         If TABLE specified, only show indices for tables
                         matching LIKE pattern TABLE.
.load FILE ?ENTRY?     Load an extension library
.log FILE|off          Turn logging on or off.  FILE can be stderr/stdout
.mode MODE ?TABLE?     Set output mode where MODE is one of:
                         csv      Comma-separated values
                         column   Left-aligned columns.  (See .width)
                         html     HTML <table> code
                         insert   SQL insert statements for TABLE
                         line     One value per line
                         list     Values delimited by .separator string
                         tabs     Tab-separated values
                         tcl      TCL list elements
.nullvalue STRING      Use STRING in place of NULL values
.open ?FILENAME?       Close existing database and reopen FILENAME
.output FILENAME       Send output to FILENAME
.output stdout         Send output to the screen
.print STRING...       Print literal STRING
.prompt MAIN CONTINUE  Replace the standard prompts
.quit                  Exit this program
.read FILENAME         Execute SQL in FILENAME
.restore ?DB? FILE     Restore content of DB (default "main") from FILE
.schema ?TABLE?        Show the CREATE statements
                         If TABLE specified, only show tables matching
                         LIKE pattern TABLE.
.separator STRING      Change separator used by output mode and .import
.show                  Show the current values for various settings
.stats ON|OFF          Turn stats on or off
.tables ?TABLE?        List names of tables
                         If TABLE specified, only list tables matching
                         LIKE pattern TABLE.
.timeout MS            Try opening locked tables for MS milliseconds
.trace FILE|off        Output each SQL statement as it is run
.vfsname ?AUX?         Print the name of the VFS stack
.width NUM1 NUM2 ...   Set column widths for "column" mode
.timer ON|OFF          Turn the CPU timer measurement on or off
```

Examples:

```
$ sqlite3 mydata.db
SQLite version 3.7.9
Enter ".help" for instructions
sqlite> create table memos(text, priority INTEGER);
sqlite> insert into memos values('deliver project description', 10);
sqlite> insert into memos values('lunch with Christine', 100);
sqlite> select * from memos;
deliver project description|10
lunch with Christine|100
sqlite>
```

---

```
sqlite> .tables
sqlite> .mode column  
sqlite> .headers on
sqlite> .exit
```

## Using SQLite In Multi-Threaded Applications

**Can multiple applications or multiple instances of the same application access a single database file at the same time?**

Multiple processes can have the same database open at the same time. Multiple processes can be doing a SELECT at the same time. But only one process can be making changes to the database at any moment in time, however.

SQLite uses reader/writer locks to control access to the database. (Under Win95/98/ME which lacks support for reader/writer locks, a probabilistic simulation is used instead.) But use caution: this locking mechanism might not work correctly if the database file is kept on an NFS filesystem. This is because fcntl() file locking is broken on many NFS implementations. You should avoid putting SQLite database files on NFS if multiple processes might try to access the file at the same time. On Windows, Microsoft's documentation says that locking may not work under FAT filesystems if you are not running the Share.exe daemon. People who have a lot of experience with Windows tell me that file locking of network files is very buggy and is not dependable. If what they say is true, sharing an SQLite database between two or more Windows machines might cause unexpected problems.

We are aware of no other embedded SQL database engine that supports as much concurrency as SQLite. SQLite allows multiple processes to have the database file open at once, and for multiple processes to read the database at once. When any process wants to write, it must lock the entire database file for the duration of its update. But that normally only takes a few milliseconds. Other processes just wait on the writer to finish then continue about their business. Other embedded SQL database engines typically only allow a single process to connect to the database at once.

However, client/server database engines (such as PostgreSQL, MySQL, or Oracle) usually support a higher level of concurrency and allow multiple processes to be writing to the same database at the same time. This is possible in a client/server database because there is always a single well-controlled server process available to coordinate access. If your application has a need for a lot of concurrency, then you should consider using a client/server database. But experience suggests that most applications need much less concurrency than their designers imagine.

When SQLite tries to access a file that is locked by another process, the default behavior is to return SQLITE_BUSY. You can adjust this behavior from C code using the `sqlite3_busy_handler()` or `sqlite3_busy_timeout()` API functions.

**Is SQLite threadsafe?**

[Threads are evil](http://www.eecs.berkeley.edu/Pubs/TechRpts/2006/EECS-2006-1.pdf). Avoid them.

SQLite is threadsafe. We make this concession since many users choose to ignore the advice given in the previous paragraph. But in order to be thread-safe, SQLite must be compiled with the SQLITE_THREADSAFE preprocessor macro set to 1. Both the Windows and Linux precompiled binaries in the distribution are compiled this way. If you are unsure if the SQLite library you are linking against is compiled to be threadsafe you can call the `sqlite3_threadsafe()` interface to find out.

SQLite is threadsafe because it uses mutexes to serialize access to common data structures. However, the work of acquiring and releasing these mutexes will slow SQLite down slightly. Hence, if you do not need SQLite to be threadsafe, you should disable the mutexes for maximum performance. See the [threading mode](https://sqlite.org/threadsafe.html) documentation for additional information.

Under Unix, you should not carry an open SQLite database across a `fork()` system call into the child process.

> https://sqlite.org/faq.html
> https://www.sqlite.org/threadsafe.html

**Discussion on StackOverflow**

- [How to use SQLite in a multi-threaded application?](http://stackoverflow.com/questions/1680249/how-to-use-sqlite-in-a-multi-threaded-application)
- [Managing sqlite database in a multithreaded environment](http://stackoverflow.com/questions/32214960/managing-sqlite-database-in-a-multithreaded-environment)

## Reference

- https://en.wikipedia.org/wiki/SQLite
- https://www.sqlite.org/cintro.html
- https://www.sqlite.org/quickstart.html
- https://www.sqlite.org/docs.html
- https://www.sqlite.org/capi3ref.html
- https://www.sqlite.org/threadsafe.html
- https://www.sqlite.org/c3ref/threadsafe.html
- https://sqlite.org/faq.html
- http://www.sqlite.org/cvstrac/wiki
- http://www.sqlite.org/cvstrac/wiki?p=MultiThreading
- http://zetcode.com/db/sqlitec/
- https://www.tutorialspoint.com/sqlite/sqlite_c_cpp.htm
- http://stackoverflow.com/questions/32214960/managing-sqlite-database-in-a-multithreaded-environment
- http://stackoverflow.com/questions/1680249/how-to-use-sqlite-in-a-multi-threaded-application

