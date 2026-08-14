#mssql #database #remote-connections #security #firewall

Getting a SQL Server instance reachable from another machine takes three separate steps, missing any one of them looks like a firewall problem when it might not be:

1. **Enable the TCP/IP protocol.** In SQL Server Configuration Manager → SQL Server Network Configuration → Protocols for `<instance>`, enable **TCP/IP** (it's often disabled by default on a fresh install). Restart the SQL Server service after changing it.
2. **Allow remote connections on the instance.** Server Properties → Connections → check **Allow remote connections to this server**.
3. **Open the firewall port.** See [[Default Ports]] for the standard MSSQL ports, `New-NetFirewallRule` works, or the Windows Firewall GUI.

For step 3, scope the rule to specific known remote IP addresses (the rule's **Scope** tab, **Remote IP address → These IP addresses**) rather than leaving it open to **Any**, especially for an instance reachable from the internet, not just a LAN.
