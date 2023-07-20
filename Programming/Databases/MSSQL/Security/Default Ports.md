#mssql #database #ports
By default, the typical ports used/needed by MSSQL Server and associated database engine services are: 
1. TCP 1433:
	* ```New-NetFirewallRule -DisplayName "SQLServer default instance" -Direction Inbound -LocalPort 1433 -Protocol TCP -Action Allow```
2. TCP 4022
	* ```New-NetFirewallRule -DisplayName "SQLServer Service Broker" -Direction Inbound -LocalPort 4022 -Protocol TCP -Action Allow```
3. TCP 135
	* ```New-NetFirewallRule -DisplayName "SQLServer Transact-SQL debugger" -Direction Inbound -LocalPort 135 -Protocol TCP -Action Allow```
4. TCP 1434
	* ```New-NetFirewallRule -DisplayName "SQLServer Replication" -Direction Inbound -LocalPort 1434 -Protocol TCP -Action Allow```
5. UDP 1434
	* ```New-NetFirewallRule -DisplayName "SQLServer Browser service" -Direction Inbound -LocalPort 1434 -Protocol UDP -Action Allow```