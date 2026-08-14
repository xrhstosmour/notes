#typescript #nodejs #pm2 #windows #process-manager

[pm2](https://pm2.keymetrics.io/) keeps a Node.js app running as a background process and restarts it on crash, on Windows it needs a bit more setup than on Linux since there's no native systemd-style service manager.

## Setup

1. Install globally: `npm install -g pm2`
2. Set `PM2_HOME` to a stable path (an env var), otherwise it defaults under the current user's profile.
3. Start the app: `pm2 start <app>.js`
4. Save the process list so it can be restored later: `pm2 save`

## Autorun on Boot

Windows has no native `pm2 startup` support like Linux does. Two options:

- Use the `pm2-windows-startup` package (`npm install -g pm2-windows-startup && pm2-startup install`), check it's still maintained before relying on it, third-party startup helpers for pm2 come and go.
- Or create a small batch script that sets up the environment and resurrects the saved process list:
```bat
@echo off
set HOMEDRIVE=C:
set HOMEPATH=\Users\%USERNAME%
pm2 delete all
pm2 resurrect
```
Then register that script as a Scheduled Task (Task Scheduler → Create Task → Trigger: "At startup" → Action: run the `.bat` → **Run with highest privileges**).

## Monitoring

`pm2 monit` gives a local live view. PM2 Plus (hosted monitoring/alerting) is optional if remote visibility is needed.
