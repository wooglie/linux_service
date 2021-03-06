# linux_service
How to make a service in Ubuntu Linux


Save the following at `/lib/systemd/system/you_service_name.service`:
```
[Unit]
Description=My First Service
After=network-online.target

[Service]
Restart=on-failure
# do chdir before running the service
WorkingDirectory=/path/to/your/app
ExecStart=/usr/bin/node /path/to/your/app/app.js
# limit CPU and RAM quota for our service
CPUAccounting=true
CPUQuota=10%
MemoryAccounting=true
MemoryLimit=50M

[Install]
WantedBy=multi-user.target
```

Let the system know about our service:
```
systemctl daemon-reload
```

Load this service on boot:
```
systemctl enable you_service_name
```

Run:
```
systemctl restart you_service_name
```


Watch:
```
journalctl -lf -u you_service_name
```

Stop:
```
systemctl stop you_service_name
```

Disable:
```
systemctl disable you_service_name
```

Status:
```
systemctl status you_service_name
```
