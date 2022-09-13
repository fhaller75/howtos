SAP ASE admin tips
==================

## SQL query plan tracing
- interactive in current session:
```SQL
set statistics time, io, plancost, resource on
go
set showplan on
go
set nodata on
go
--Query blocks of the studied proc
go
set showplan off
go
set statistics time, io, plancost, resource off
go
set nodata off
go
```
- on another process current query:
```SQL
sp_showplan <spid>,null,null,null[,'short|full|long']
go
```
- to display batch_id:
```SQL
declare @batch int
declare @context int
declare @statement int
exec sp_showplan <spid>, @batch output, @context output, @statement output
go
```
