# check_linux_filesystems
nagios check to confirm all linux filesystems are mounted correctly

# Requirements
bash, ssh

# Configuration

This script is executed remotely on a monitored system by the NRPE or check_by_ssh methods available in nagios.

If you are using the check_by_ssh method, you will need to add a section similar to the following to the services.cfg file on the nagios server.
This assumes you already have ssh key pairs configured.
```
define service {
       use                             generic-service
       hostgroup_name                  all_linux
       service_description             filesystems
       check_command                   check_by_ssh!/usr/local/nagios/libexec/check_linux_filesystems
       }
```

If you are using the NRPE method, you will also need a command definition similar to the following on each monitored host in the /usr/local/nagios/nrpe/nrpe.cfg file:
```
command[check_linux_filesystems]=/usr/local/nagios/libexec/check_linux_filesystems
```

# Sample Output
filesystems OK - All required filesystems from /etc/fstab are mounted: / /boot /boot/efi /var/lib/libvirt/images 

filesystems CRITICAL - Missing filesystem mounts: /mountpoint1 /mountpoint2 /mountpoint3
