#erp #sbo #hana #sles #installation

High-level checklist for installing SAP HANA 2.0 on SLES for a SAP Business One, version for SAP HANA deployment. Verify exact package/parameter names against the current SAP installation guide for the SLES version in use, HANA's supported-OS and prerequisite list changes across releases.

1. Register the SLES system and enable the SAP-specific repositories/modules required for HANA.
2. Map the machine's own hostname to loopback in `/etc/hosts` before installing, HANA on a single host expects this:
```
127.0.0.1   localhost
127.0.0.1   <hana_hostname>
127.0.0.2   <hana_hostname>
```
3. Apply the kernel and filesystem parameters SAP's prerequisite checker calls out (these are checked by the HANA installer itself, `hdblcm`, and it will refuse to proceed if they're wrong).
4. Extract the HANA installation media (`SAPCAR -xvf <archive>.SAR`) and run the interactive installer, it detects the HANA Database/Client/AFL components under the extraction path and offers `install`/`extract_components`:
```
./hdblcm
```
Follow the prompts for the system ID, instance number, and the service account passwords (`sapadm`, `hdbadm`, and the DB `SYSTEM` user), set these interactively, don't hardcode them anywhere.
5. Fix any missing packages the SAP Business One server components installer's dependency check reports (common ones: `python < 3.0.0`, `python-openssl`, `libcap-progs`, `libicu60_2`, needed by the analytics platform, SLD server tools, web client, service layer, and electronic document service respectively) via `zypper install <package>`.
6. Verify the instance is running, either at a glance or per-process:
```
HDB info
sapcontrol -nr <instance_number> -function GetProcessList
```
7. Some SAP Business One features (e.g. certain reporting/scripting integrations) need the HANA scriptserver enabled, connect with `hdbsql` and add it if it's missing:
```
hdbsql -u SYSTEM -n localhost:30013
hdbsql SYSTEMDB=> alter database HDB add 'scriptserver'
```
8. Set up a SAMBA (or equivalent) share on the server, conventionally named something like `B1_SHF`, so the SAP Business One client installer and HANA client can be pulled onto Windows machines that need them. If a Windows client fails to connect to an older SMB1-only share config, it needs the **SMB 1.0/CIFS Client** Windows feature enabled, and possibly the **Enable insecure guest logons** Group Policy setting under Network → Lanman Workstation, both loosen a real security control (SMB1 has known vulnerabilities), only do this if the share genuinely can't be reconfigured for SMB2/3 instead.
9. Install SAP Business One's server components against the HANA instance, then verify with [[Restart service layer]] and [[Restart client services]].
10. On an admin workstation, install HANA Studio (or HANA Cockpit for a more modern, browser-based option) to manage the instance day to day.
