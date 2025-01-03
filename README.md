[![CI](https://github.com/de-it-krachten/ansible-role-clamav/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-clamav/actions?query=workflow%3ACI)


# ansible-role-clamav

Manage ClamAV


## Dependencies

#### Roles
None

#### Collections
- ansible.posix

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- OracleLinux 9
- AlmaLinux 8
- AlmaLinux 9
- SUSE Linux Enterprise 15<sup>1</sup>
- openSUSE Leap 15
- Debian 11 (Bullseye)
- Debian 12 (Bookworm)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Ubuntu 24.04 LTS
- Fedora 40
- Fedora 41

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>

</pre></code>

### defaults/family-Debian.yml
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

# freshclam_conf
clamav_freshclam_conf: /etc/clamav/freshclam.conf

# clamav configuration
clamav_scan_conf:
  User: root
  LocalSocket: /var/run/clamd.scan/clamd.sock
  LocalSocketGroup: virusgroup
  LocalSocketMode: '660'
  FixStaleSocket: 'yes'
  ExcludePath: "^(/proc/|/sys/)"
  ScanOnAccess: 'yes'
  OnAccessMaxFileSize: 25M
  OnAccessExcludeRootUID: 'yes'
  # OnAccessExcludeUname: clamav
  OnAccessPrevention: 'yes'
  OnAccessDisableDDD: 'no'
</pre></code>

### defaults/family-RedHat.yml
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
clamav_services_disabled: []

# clamav main configuration file
clamav_conf: /etc/clamd.d/scan.conf

# freshclam_conf
clamav_freshclam_conf: /etc/freshclam.conf

# clamav configuration
clamav_scan_conf:
  User: root
  LocalSocket: /var/run/clamd.scan/clamd.sock
  LocalSocketGroup: virusgroup
  LocalSocketMode: '660'
  FixStaleSocket: 'yes'
  ExcludePath: "^(/proc/|/sys/)"
  ScanOnAccess: 'yes'
  OnAccessMaxFileSize: 25M
  OnAccessExcludeRootUID: 'yes'
  # OnAccessExcludeUname: clamav
  OnAccessPrevention: 'yes'
  OnAccessDisableDDD: 'no'
</pre></code>

### defaults/family-Suse.yml
<pre><code>
# List of required packages
clamav_packages:
  - clamav
  - clamav-database

# clamav systemd services
clamav_services:
  - clamd
  - freshclam

# clamav systemd services to disable
clamav_services_disabled: []

# clamav main configuration file
clamav_conf: /etc/clamd.conf

# freshclam_conf
clamav_freshclam_conf: /etc/freshclam.conf

# clamav configuration
clamav_scan_conf:
  User: root
  LocalSocket: /var/run/clamd.scan/clamd.sock
  LocalSocketGroup: vscan
  LocalSocketMode: '660'
  FixStaleSocket: 'yes'
  ExcludePath: "^(/proc/|/sys/)"
  ScanOnAccess: 'yes'
  OnAccessMaxFileSize: 25M
  OnAccessExcludeRootUID: 'yes'
  # OnAccessExcludeUname: clamav
  OnAccessPrevention: 'yes'
  OnAccessDisableDDD: 'no'
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'clamav'
  hosts: all
  become: 'yes'
  tasks:
    - name: Include role 'clamav'
      ansible.builtin.include_role:
        name: clamav
</pre></code>
