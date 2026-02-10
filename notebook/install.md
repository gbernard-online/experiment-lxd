# EXPERIMENT LXD

## REFERENCES

https://canonical.com/lxd/install  
https://documentation.ubuntu.com/lxd/latest/installing  
https://documentation.ubuntu.com/lxd/latest/howto/initialize

https://www.youtube.com/watch?v=7SOTKSMpFQA&list=PLn6POgpklwWp9TsSy2yg-dPfpuAdUe276

## INSTALL - LXD 5 - UBUNTU 24

[![LXD](img/lxd.webp "LXD")](https://canonical.com/lxd)5
[![Ubuntu](img/ubuntu.webp "Ubuntu")](https://ubuntu.com)24

```bash
$ sudo snap install lxd
|...|
lxd (5.21/stable) 5.21.4-de343be from Canonical✓ installed

$ lxd version
5.21.4 LTS

$ cat <<EOF | lxd init --preseed
cluster: null
config:
  core.https_address: '[::]:8443'
networks:
  - config:
      ipv4.address: auto
      ipv6.address: auto
    description: ""
    name: lxdbr0
    type: ""
    project: default
profiles:
  - config: {}
    description: ""
    devices:
      eth0:
        name: eth0
        network: lxdbr0
        type: nic
      root:
        path: /
        pool: default
        type: disk
    name: default
projects: []
storage_pools:
  - config: {}
    description: ""
    name: default
    driver: dir
storage_volumes: []
EOF
```

&nbsp;

`-`

[![Monster](https://avatars.githubusercontent.com/u/47848582?s=96&v=4 "Boo!")](../README.md)
