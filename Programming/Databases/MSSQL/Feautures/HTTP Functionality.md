#mssql #database #http-functionality
To enable HTTP functionality inside the Microsoft SQL Server, run the following commands:
``` sql 
exec [DBO].sp_configure 'show advanced options', 1;
RECONFIGURE;
exec [DBO].sp_configure 'Ole Automation Procedures', 1;
RECONFIGURE;
```