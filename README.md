
# iptables-admin-whitelist
IPTables Admin Whitelist

**Usage:**

Create /etc/iptadmin.lst (or specify a different file by changing the list= variable).  This file may contain hostnames, IPv4 and IPv6 addresses, or IPv4 and IPv6 CIDR blocks.  Basic sanity checks are in place but proper values fall solely on you.

Change the dudeservers= variable to the comma-separated IP addresses or hostnames of your Dude Servers.  Once your Dude Servers are added to a device, they will not be removed when the address list is purged and rewritten.  This will prevent Dude Server disconnects when the address list is updated.

Make the script executable and run.  Script will generate the file you specify by changing the file= value.

**Automation:**

It is recommended that you run the script with systemd timers:

```
printf '[Unit]
Description=IPTables Admin Whitelist Creator
[Service]
Type=simple
ExecStart=/usr/local/bin/iptadmin
[Install]
WantedBy=multi-user.target
' | tee /etc/systemd/system/iptadmin.service

printf '[Unit]
Description=IPTables Admin Whitelist Scheduler
[Timer]
OnCalendar=*:0/5
Unit=iptadmin.service
[Install]
WantedBy=multi-user.target
' | tee /etc/systemd/system/iptadmin.timer

systemctl daemon-reload
systemctl enable iptadmin.timer
```

On each client device, install the script using the following.  The script will install the cron job, and maintain it:

```
curl -kOs https://example.com/admin.ipt /tmp/admin.ipt && sh /tmp/admin.ipt
```
