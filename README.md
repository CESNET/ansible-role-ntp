# ansible-role-ntp
Ansible role for setting up NTP time synchronization on Debian.

There are 3 packages for NTP in Debian: ntp, chrony and systemd-timesyncd.
This role installs the package **chrony** which uninstalls ntp or systemd-timesyncd
if any of them is already installed. 

Then the file /etc/chrony/chrony.conf is edited to contain NTP server definitions
specified in the variable ntp_servers.

Role Variables
--------------

* **ntp_servers** - fragment of /etc/chrony/chrony.conf, default is 
```
server ntp.muni.cz iburst
server tik.cesnet.cz iburst
server tak.cesnet.cz iburst
```

Examples of Playbooks
----------------

```yaml
    - hosts: all 
      roles:
         - role: cesnet.ntp
           vars:
             ntp_servers: |2
               server: tik.cesnet.cz iburst
```
or
```yaml
    - hosts: all 
      tasks:
        - import_role:
            name: "cesnet.ntp"
          vars:
            ntp_servers: "{{ my_ntp_servers }}"
```