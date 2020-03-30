# Zabbix PDF Report

Name all graph titles or item names you would like to generate a graph for. Define the scope of a host or host group. Select time period like last hour, last day, last week. Generate PDF. Events also can be included in the report.

I'm not the author of code. Just providing a nice instruction how to install the feature.

## Installation

This instruction assumes you are using default zabbix installation which points on http://192.168.56.100/zabbix/

The following solution uses zabbix API which are located at http://192.168.56.100/zabbix/api_jsonrpc.php

After you complete the installation steps you we be able to access reporting tool on http://192.168.56.100/zbxreport/

Prepare git utility on RHEL/CentOS family
```
yum -y install git
```

Prepare git utility on Debian/Ubuntu family
```
apt -y install git
```

Install project
```
cd /usr/share
git clone https://github.com/catonrug/zabbix-pdf-report.git
```

Prepare access
```
cd /usr/share/zabbix-pdf-report
cp config.inc.php.dist config.inc.php
```

Create working dir
```
cd /usr/share/zabbix-pdf-report
./fixrights.sh
```

Install httpd directive
```
cp /usr/share/zabbix-pdf-report/zabbix-pdf-report.conf /etc/httpd/conf.d
```

Restart httpd
```
systemctl restart httpd
```

Make sure SELinux is off
```
setenforce 0
```

## To create link without authorization
Do not ask for user to log in
```
sed -i "s|\$user_login=1;|\$user_login=0;|" /usr/share/zabbix-pdf-report/config.inc.php
```
If you are using different credentials than user: Admin, password: zabbix, then set the right credentials
```
vi /usr/share/zabbix-pdf-report/config.inc.php
```

Use url http://192.168.56.100/zbxreport/chooser.php

## In Production

Before put in production, change in "chooser.php" the line "ZabbixAPI::debugEnabled(TRUE) to FALSE to avoid expose sensitive information.

## Related
https://www.zabbix.com/forum/showthread.php?t=24998
