# Tango Robot Setup

## Time sync
When errors occur during runtime using RTABMap which appear similar to the following:

```Timed out waiting for transform from base_link to map to bedome available before running costmap, tf erro: **Look up would require extrapolation 21231.90123s into the past**...```

It is likely that the system time of the raspbery pi on board Tango is not synced with the system time of the device running ROSCORE. You can confirm this by running ```sudo timedatectl status```. NTP service should be active and System Clock Synchorinized should be yes.

If this is not the case, begin by setting up a NTP server on the device running roscore. Install NTP using apt, all default settings should work. Start the service with ```sudo service ntp start```.

SSH into Tango and edit ```/etc/systemd/timesyncd.conf```. Edit the line begining ```NTP=``` to add the IP address of the device running roscore after the equals. Make sure it is not commented out by removing any ```#``` at the start of the line that may be present. Multiple IPs can be added with a space between them, but this is not advsed.

Timesyncd only syncs with the NTP server on startup, so if the server was not running, or the device was not on the ROSBOX network when Tango started, run the following three commands on Tango:
- ```sudo systemctl daemon-reload```
- ```sudo timedated set-ntp off```
- ```sudo timedated set-ntp on```

Now confirm that Timesyncd has synced with the NTP server by once again running ```sudo timedatectl status```.
