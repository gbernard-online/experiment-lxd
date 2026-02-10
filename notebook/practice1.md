# EXPERIMENT LXD

## REFERENCES

https://documentation.ubuntu.com/lxd/latest/tutorial/first_steps  
https://images.linuxcontainers.org  
https://documentation.ubuntu.com/lxd/latest/reference/manpages/lxc/launch  
https://documentation.ubuntu.com/lxd/latest/reference/manpages/lxc/list  
https://documentation.ubuntu.com/lxd/latest/reference/manpages/lxc/exec  
https://documentation.ubuntu.com/lxd/latest/reference/manpages/lxc/image/list  
https://documentation.ubuntu.com/lxd/latest/reference/manpages/lxc/image/info  
https://documentation.ubuntu.com/lxd/latest/reference/manpages/lxc/stop  
https://documentation.ubuntu.com/lxd/latest/reference/manpages/lxc/start  
https://documentation.ubuntu.com/lxd/latest/reference/manpages/lxc/delete  
https://documentation.ubuntu.com/lxd/latest/reference/manpages/lxc/image/delete

https://www.youtube.com/watch?v=A9FKc65os6Y&list=PLn6POgpklwWp9TsSy2yg-dPfpuAdUe276  
https://www.youtube.com/watch?v=zmPmL0z8QW4&list=PLn6POgpklwWp9TsSy2yg-dPfpuAdUe276


## PRACTICE #1 - LXD 5 - UBUNTU 24

[![LXD](img/lxd.webp "LXD")](https://canonical.com/lxd)5
[![Ubuntu](img/ubuntu.webp "Ubuntu")](https://ubuntu.com)24

```bash
$ lxc list
+------+-------+------+------+------+-----------+
| NAME | STATE | IPV4 | IPV6 | TYPE | SNAPSHOTS |
+------+-------+------+------+------+-----------+

$ lxc launch images:alpine/3.23 alpine
Launching alpine

$ lxc list --fast
+--------+---------+--------------+----------------------+----------+-----------+
|  NAME  |  STATE  | ARCHITECTURE |      CREATED AT      | PROFILES |   TYPE    |
+--------+---------+--------------+----------------------+----------+-----------+
| alpine | RUNNING | x86_64       | 2026/02/10 20:00 UTC | default  | CONTAINER |
+--------+---------+--------------+----------------------+----------+-----------+

$ lxc list --columns=ns46
+--------+---------+---------------------+-----------------------------------------------+
|  NAME  |  STATE  |        IPV4         |                     IPV6                      |
+--------+---------+---------------------+-----------------------------------------------+
| alpine | RUNNING | 172.18.0.244 (eth0) | fd39:d8bd:967c:bb6f:216:3eff:fe13:afdc (eth0) |
+--------+---------+---------------------+-----------------------------------------------+

$ lxc list --columns=ns46 --format=compact
   NAME    STATE          IPV4                              IPV6
  alpine  RUNNING  172.18.0.244 (eth0)  fd39:d8bd:967c:bb6f:216:3eff:fe13:afdc (eth0)

$ lxc list --columns=n,config:image.os
+--------+----------+
|  NAME  | IMAGE OS |
+--------+----------+
| alpine | Alpine   |
+--------+----------+

$ lxc list --columns=n --format=json | jq '[.[] | {name,status,type}]'
[
  {
    "name": "alpine",
    "status": "Running",
    "type": "container"
  }
]

$ lxc list --columns=n --format=yaml | yq 'map(pick(["name","status","type"]))'
- name: alpine
  status: Running
  type: container

$ lxc exec alpine hostname
alpine

$ lxc exec alpine id
uid=0(root) gid=0(root)

$ lxc exec alpine cat /etc/alpine-release
3.23.3
```

```bash
$ lxc image list --columns=fd
+--------------+-----------------------------------+
| FINGERPRINT  |            DESCRIPTION            |
+--------------+-----------------------------------+
| f0285ec3feda | Alpine 3.23 amd64 (20260210_0102) |
+--------------+-----------------------------------+

$ lxc image info f0285ec3feda
Fingerprint: f0285ec3feda41995ec292c9b9efab78eb08f8b08a73d775c84facf9d458015e
Size: 3.26MiB
Architecture: x86_64
Type: container
Public: no
Timestamps:
    Created: 2026/02/10 01:02 UTC
    Uploaded: 2026/02/10 20:00 UTC
    Expires: never
    Last used: 2026/02/10 20:00 UTC
Properties:
    description: Alpine 3.23 amd64 (20260210_0102)
    os: Alpine
    release: 3.23
    requirements.secureboot: false
    serial: 20260210_0102
    type: squashfs
    variant: default
    architecture: amd64
Aliases:
Cached: yes
Auto update: enabled
Source:
    Server: https://images.lxd.canonical.com
    Protocol: simplestreams
    Alias: alpine/3.23
Profiles:
    - default
```

```bash
$ lxc stop alpine

$ lxc list --columns=ns46
+--------+---------+------+------+
|  NAME  |  STATE  | IPV4 | IPV6 |
+--------+---------+------+------+
| alpine | STOPPED |      |      |
+--------+---------+------+------+

$ lxc start alpine

$ lxc list --columns=ns46
+--------+---------+---------------------+-----------------------------------------------+
|  NAME  |  STATE  |        IPV4         |                     IPV6                      |
+--------+---------+---------------------+-----------------------------------------------+
| alpine | RUNNING | 172.18.0.244 (eth0) | fd39:d8bd:967c:bb6f:216:3eff:fe13:afdc (eth0) |
+--------+---------+---------------------+-----------------------------------------------+

$ lxc stop alpine

$ lxc delete alpine

$ lxc list --columns=ns46
+------+-------+------+------+
| NAME | STATE | IPV4 | IPV6 |
+------+-------+------+------+

$ lxc image delete f0285ec3feda

$ lxc image list --columns=fd
+-------------+-------------+
| FINGERPRINT | DESCRIPTION |
+-------------+-------------+
```

&nbsp;

`-`

[![Monster](https://avatars.githubusercontent.com/u/47848582?s=96&v=4 "Boo!")](../README.md)
