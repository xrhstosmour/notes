#mssql #database #http-functionality #ole #enable-http

Integrating MSSQL Server with external services via HTTP requests requires the configuration of SQL Server to enable OLE Automation Procedures. Follow this guide to set up for making HTTP calls.

``` sql
-- Enable advanced options
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO

-- Enable OLE Automation Procedures
sp_configure 'Ole Automation Procedures', 1;
GO
RECONFIGURE;
GO
```