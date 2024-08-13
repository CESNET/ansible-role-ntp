# ansible-role-ntp
Ansible role for setting up NTP time synchronization on Debian/Ubuntu.

There are 3 packages for NTP in Debian: ntp, chrony and systemd-timesyncd.
This role installs the package **chrony** which uninstalls ntp or systemd-timesyncd
if any of them is already installed. 

Then the file /etc/chrony/sources.d/cesnet.sources is created to contain NTP server definitions
specified in the variable ntp_servers.

Role Variables
--------------

* **ntp_servers** - content of /etc/chrony/sources.d/cesnet.sources, default is 
```
server tik.cesnet.cz iburst
server tak.cesnet.cz iburst
server ntp1.cesnet.cz iburst
server ts1.cesnet.cz iburst
server ts2.cesnet.cz iburst
```
* **ntp_disable_default_pool**
  * Default: `false`
  * Should be `true` if the default Debian pool should be disabled

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