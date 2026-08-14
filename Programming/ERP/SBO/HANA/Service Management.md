#erp #sbo #hana #systemd #service

A small wrapper script plus a `systemd` unit to keep a SAP Business One HANA instance's related services up after a reboot.

## Wrapper Script

``` bash
#!/bin/bash
# Starts the HDB instance and restarts SAP Business One's server tools once it's up.

su - hdbadm -c "HDB start"

# Give HDB time to fully come up before checking it.
sleep 60

su - hdbadm -c "HDB info"

systemctl restart sapb1servertools
```

## systemd Unit

``` ini
[Unit]
Description=SAP Business One HANA startup
After=network.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStartPre=/bin/sleep 180
ExecStart=/path/to/b1_hana.sh
TimeoutStartSec=900

[Install]
WantedBy=multi-user.target
```

Install with:
```
sudo cp b1hana.service /etc/systemd/system/
sudo chmod 640 /etc/systemd/system/b1hana.service
sudo systemctl daemon-reload
sudo systemctl enable --now b1hana.service
sudo systemctl status b1hana.service
```

The pre-start delay exists because HANA needs time to become available after a host reboot before the dependent service restart makes sense, tune it to the actual instance's boot time.
