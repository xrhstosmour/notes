#sbo #erp #dll
The following procedure is only applicable for coding at Windows machines, using the Visual Studio.
  1. Install both x64 and x32 SAP Business One DI API.
  2. Open CMD as administrator.
  3. Type: ```regsvr32 "C:\Program Files\SAP\SAP Business One DI API\DI API <DI_API_VERSION>\SAPbobsCOM<DI_API_VERSION>.dll"```
  4. Type: ```regsvr32 "C:\Program Files (x86)\SAP\SAP Business One DI API\DI API <DI_API_VERSION>\SAPbobsCOM<DI_API_VERSION>.dll"```

- - -

## Troubleshooting
* In case you can't build the code or it does not run successfully, try download the ```SAPBusinessOneSDK.dll``` from the SAP Business One server, located at: ```C:\Program Files (x86)\SAP\SAP Business One SDK\Lib\``` and import the reference via Browse at Visual Studio.
