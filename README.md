A collection of nagios scripts that aim to use ssh only without the need to install a nagios agent and plugins on the remote hosts.

check-disk-by-ssh (forked of edimass https://github.com/eddimas/nagios-plugins/blob/master/check_disk.sh)
* Added ssh identity file support
* Added -p argument to target a specific mountpoint instread of all

COMMAND-LINE FOR CHECK_DISKS
USAGE $USER1$/check_disk.sh -l username -H $HOSTNAME$ -w 75 -c 90"

COMMAND-LINE FOR SERVICE (EXAMPLE)
$USER1$/check_disk.sh!$USER1$!$HOSTNAME$!75!90

Output example for OK, warning, critical and (the worst) warning + critical
$ ./check_disk.sh -l nagios -H 192.168.1.74 -w 75 -c 90
OK. DISK STATS: / 14% of 33G, /dev 0% of 956M, /dev/shm 1% of 966M, /run 1% of 966M, /sys/fs/cgroup 0% of 966M, /boot 34% of 521M,
$ ./check_disk.sh -i /home/nagios/.ssh/privkey -l nagios -H 192.168.1.74 -w 30 -c 40
WARNING. DISK STATS: / 14% of 33G, /dev 0% of 956M, /dev/shm 1% of 966M, /run 1% of 966M, /sys/fs/cgroup 0% of 966M, /boot 34% of 521M,; Warning /boot has 34% of utilization or 175M of 521M,
$ ./check_disk.sh -i /home/nagios/.ssh/privkey -l nagios -H 192.168.1.74 -w 15 -c 30
CRITICAL. DISK STATS: / 14% of 33G, /dev 0% of 956M, /dev/shm 1% of 966M, /run 1% of 966M, /sys/fs/cgroup 0% of 966M, /boot 34% of 521M,; Critical /boot has 34% of utilization or 175M of 521M,
$ ./check_disk.sh -i /home/nagios/.ssh/privkey -l nagios -H 192.168.1.74 -w 10 -c 30
CRITICAL. DISK STATS: / 14% of 33G, /dev 0% of 956M, /dev/shm 1% of 966M, /run 1% of 966M, /sys/fs/cgroup 0% of 966M, /boot 34% of 521M,; Warning / has 14% of utilization or 4.3G of 33G,; Critical /boot has 34% of utilization or 175M of 521M,
