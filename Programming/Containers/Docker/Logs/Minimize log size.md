#docker #logs #size #overaly2
Execute the following, in order to reduce the Docker logs size and limit the files' history version:

1. Create or update the `/etc/docker/daemon.json` file and paste the following: 
``` json
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}
```
This JSON will:
- Use the JSON file log driver for Docker and update the log options.
- Set the maximum size of each log file to 10Mb.
- Set the maximum number of log files to retain to 3.

2. Restart Docker: `sudo systemctl restart docker`