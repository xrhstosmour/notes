#erp #sbo #administration #backup #security

Pointers to what's covered in SAP's official Business One Administrator's Guide, worth checking before reinventing an approach:

- **Backup and restore strategy**: SAP's guide documents the supported backup approaches per database platform (MSSQL/HANA), including how SBO-specific metadata needs to be handled alongside a plain database backup, don't rely on a database-only backup without checking this.
- **System Landscape Directory (SLD) and HTTPS**: setting up SLD and certificates for the Service Layer and other B1 web components, needed for a properly secured multi-server deployment.
- **Default ports**: see [[Default Ports]] for the MSSQL-side ports, the guide also covers the B1-specific service ports (Service Layer, License Manager, etc.).
- **Security hardening**: license manager security, user authentication options, and role/permission setup beyond the basics.

This is a reference pointer, not a substitute for reading the actual guide for the SBO/database version in use, the specifics shift between versions.
