# sqldiff
(My)SQL db (snapshot &amp;) diff viewer ...in my mind.

Overview changes in database between two snapshots.

Suited for small dev / testing databases, during development (& debugging).

## cli

$ `sqldiff mydb`
 - takes snapshot of `mydb`

$ `sqldiff`
 - snapshots `mydb` again
 - prints diff to stdout

$ `sqldiff mydb --ui`
 - takes snapshot of `mydb`
 - starts webserver
 - opens diff viewer web page

$ `sqldiff --snapshot[="some snapshot name"]`
 - (given that dqldiff is running;) takes snapshot

## interface
I imagine primarily:
 - One HTML table for each SQL table.
 - New / INSERTED rows are green.
 - Changed / Updated rows are yellow
 - Removed / DELETED are red or greyed out.
 - Unchanged entries are not visible at all (unless perhaps neighbouring the changed ones...).

Secondary:
 - Hovering an ID / row with a foreign key highlights that / those rows in other tables.
 - MySQL error log diff (also diffed per snapshot).
 - Snapshots stored ~: ./snapshots/databasename-2015-01-22--08-31-32.348.sql|csv|...
 - Also represent new/modified/removed tables?
 - List of snapshots; allows you to compare any two snapshots.
 - Show only the tables that were touched?
 - Support (nice looking) database diagram with relations showing (& tables positioned always the same to aid memory).

## alternative usage
### debugging tests
```coffee
before: ->
  `sqldiff mydb`
...
afterEach: ->
  `sqldiff --snapshot="#{framework.getTestName()}"`
```

