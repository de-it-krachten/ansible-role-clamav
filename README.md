[![CI](https://github.com/de-it-krachten/ansible-role-clamav/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-clamav/actions?query=workflow%3ACI)


# ansible-role-clamav

Manage ClamAV


## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- CentOS 7
- RockyLinux 8
- AlmaLinux 8<sup>1</sup>
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# clamav configuration
clamav_scan_conf:
  User:                   root
  LocalSocket:            /var/run/clamd.scan/clamd.sock
  LocalSocketGroup:       virusgroup
  LocalSocketMode:        '660'
  FixStaleSocket:         'yes'
  ExcludePath:            "^(/proc/|/sys/)"
  ScanOnAccess:           'yes'
  OnAccessMaxFileSize:    25M
  OnAccessExcludeRootUID: 'yes'
  # OnAccessExcludeUname:   clamav
  OnAccessPrevention:     'yes'
  OnAccessDisableDDD:     'no'
</pre></code>

### vars/family-RedHat.yml
<pre><code>
# List of required packages
clamav_packages:
  - clamav
  - clamav-update
  - clamav-server
  - clamav-server-systemd
#  - clamav-scanner
#  - clamtk

# clamav systemd services
clamav_services:
  - clamd@scan
  - freshclam

# clamav systemd services to disable
clamav_services_disabled:
  - clamd@scam

# clamav main configuration file
clamav_conf: /etc/clamd.d/scan.conf
</pre></code>

### vars/family-Debian.yml
<pre><code>
# List of required packages
clamav_packages:
  - clamav
  - clamav-daemon
  - clamav-freshclam
#  - clamav-scanner
#  - clamtk

# clamav systemd services
clamav_services:
  - clamav-daemon

# clamav systemd services to disable
clamav_services_disabled: []

# clamav main configuration file
clamav_conf: /etc/clamav/clamd.conf
</pre></code>



## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'clamav'
  hosts: all
  vars:
  tasks:
    - name: Include role 'clamav'
      include_role:
        name: clamav
</pre></code>
