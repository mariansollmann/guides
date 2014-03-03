Tools
=====

Online Schema Change
--------------------
Change table-schemas without locking the table with [Percona's](http://www.percona.com/) pt-online-schema-change

**Usage**

```shell
pt-online-schema-change --execute --critical-load="Threads_running:500" --max-load "Threads_running:250" --charset=utf8 --user=root --ask-pass --database=[database] t=[table] --alter='ADD `userId` int(10) unsigned NOT NULL DEFAULT '0', ADD `createStamp` int(10) unsigned NOT NULL DEFAULT '0', ADD KEY `createStamp` (`createStamp`), ADD KEY `userId` (`userId`)'
```

**Download**

[Percona Toolkit for MySQL](http://www.percona.com/software/percona-toolkit)

**Full Documentation**

http://www.percona.com/doc/percona-toolkit/2.2/pt-online-schema-change.html

**IMPORTANT**

Read the full [documentation](http://www.percona.com/doc/percona-toolkit/2.2/pt-online-schema-change.html) before using it, there a lot of peculiarities that need to be considered before using this tool.
