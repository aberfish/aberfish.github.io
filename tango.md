# Tango Robot Setup

## Time sync
When errors occur during runtime using RTABMap which appear similar to the following:

`Timed out waiting for transform from base_link to map to bedome available before running costmap, tf erro: **Look up would require extrapolation 21231.90123s into the past**...`

It is likely that the system time of the raspbery pi on board Tango is not synced with the system time of the device running ROSCORE. Tango runs a chrony NTP server so that users can sync their computer's time to Tango (note Tango's time is almost certainly incorrect, this is not an issue aslong as the time is the same across the devices).

### Setting up chrony as a client \[UBUNTU]
If the user's device (ie the one running roscore) is not synced with the time on tango, begin by installing chrony using apt: `sudo apt install chrony` on the user's device when it is connected to the internet. Once complete connect the device to the ROSBOX network so that it has access to tango.

Edit `/etc/chrony/chrony.conf` on the device you just installed chrony to. You should see a number of lines begining with "pool" near the start. Comment these out. Then below, add the line ```server 192.168.2.2``` (ie setting Tango's ip as the chrony server). There is no need to change anything else in the conf file.

Chrony uses the port '123' to confer between server and clients, so this must be allowed within the firewall useing the command `sudo ufw allow 123`.

Restart chrony with `sudo service chrony restart`. Confirm that tango is in the list of NTP servers with the command `sudo chronyc sources`. It should appear in the table with the name 'tango' and values other than 0 for all other columns.

Finally confirm that the device time is synced to Tango using the command `timedatectl status`. "System clock synchronized" should be "yes". If "NTP service" is not shown as active, run the command `sudo timedatectl set-ntp on`.

### Setting up chrony as a server (e.g. on Tango)
Install chrony, as Tango does not have access to the internet a .deb file may be provided in ~/docs. If not, look for a chrony .deb file for ubuntu 20.04 arm64. We found one at ubuntu.pkgs.org. Install the deb file with `sudo apt install ./<deb file name>` from the same directory as the file. Note that installing using dpkg instead of apt will not work due to conflicts.

Once installed on the server device, edit `/etc/chrony/chrony.conf` and comment out the lines near the begining which start with "pool". Add 3 new lines after these:

`local stratum 8
manual
allow 192.168.2`

The final line "allow 192.168.2" defines the network/submask which can access the server. Here it is set the the ROSBOX network.

Restart chrony with `sudo service chrony restart`. You can check how many clients are using the server with `sudo chronyc clients`.
