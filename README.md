
# iptables-admin-whitelist
IPTables Admin Whitelist

**Usage:**

Create /etc/iptadmin.lst (or specify a different file by changing the list= variable).  This file may contain hostnames, IPv4 and IPv6 addresses, or IPv4 and IPv6 CIDR blocks.  Basic sanity checks are in place but proper values fall solely on you.

Change the dudeservers= variable to the comma-separated IP addresses or hostnames of your Dude Servers.  Once your Dude Servers are added to a device, they will not be removed when the address list is purged and rewritten.  This will prevent Dude Server disconnects when the address list is updated.

Make the script executable and run.  Script will generate the file you specify by changing the file= value.

**Automation:**

It is recommended that you run the script with a cron job:

```
# IPTables Admin Whitelist Script

*/5 * * * * root /usr/local/bin/iptadmin
```

On each client device, use the scheduler to automatically download and import the whitelist as needed:

```
*/5 * * * * root curl -kOs https://example.com/iptadmin && chmod +x /tmp/iptadmin && /tmp/iptadmin
```
