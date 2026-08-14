#windows #iis-express #ssl #visual-studio #dotnet

1. If IIS Express isn't installed, enable it via Visual Studio's installer/Windows Features first.
2. If the project's SSL setup is stuck in a bad state, delete the project's `.vs` folder to reset the cached IIS Express config, Visual Studio regenerates it on next run.
3. In `Properties/launchSettings.json`, set `sslPort` and `launchUrl` for the `iisExpress` profile.
4. Find which SSL certificate ports are already registered:
```
netsh http show sslcert
```
5. If launching over HTTPS fails with `ERR_CONNECTION_RESET`, the bound self-signed certificate is likely stale or missing, recreate it:
```
"C:\Program Files\IIS Express\IisExpressAdminCmd.exe" setupsslUrl -url:https://localhost:<port>/ -UseSelfSigned
```
