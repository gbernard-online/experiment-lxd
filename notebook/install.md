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

$ sudo snap set lxd ui.enable=false

$ cat <<EOF | lxd init --preseed
networks:
  - config:
      ipv4.address: 172.18.0.1/24
      ipv4.nat: "true"
      ipv6.address: fd39:d8bd:967c:bb6f::1/64
      ipv6.nat: "true"
    name: lxdbr0
profiles:
  - devices:
      eth0:
        name: eth0
        network: lxdbr0
        type: nic
      root:
        path: /
        pool: default
        type: disk
    name: default
storage_pools:
  - driver: dir
    name: default
EOF

$ lxc version
To start your first container, try: lxc launch ubuntu:24.04
Or for a virtual machine: lxc launch ubuntu:24.04 --vm

Client version: 5.21.4 LTS
Server version: 5.21.4 LTS

$ ip address show lxdbr0
5: lxdbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen
1000
    link/ether 00:16:3e:d4:fa:2d brd ff:ff:ff:ff:ff:ff
    inet 1172.18.0.1/24 scope global lxdbr0
       valid_lft forever preferred_lft forever
    inet6 fd39:d8bd:967c:bb6f::1/64 scope global
       valid_lft forever preferred_lft forever

$ sudo nft list tables
table ip nat
table ip filter
table ip6 nat
table ip6 filter
table inet lxd

$ sudo nft list table inet lxd | expand --tabs=2
table inet lxd {
  chain pstrt.lxdbr0 {
    type nat hook postrouting priority srcnat; policy accept;
    ip saddr 172.18.0.0/24 ip daddr != 172.18.0.0/24 oifname != "lxdbr0" masquerade
    ip6 saddr fd39:d8bd:967c:bb6f::/64 ip6 daddr != fd39:d8bd:967c:bb6f::/64 oifname != "lxdbr0" mas
querade
  }

  chain fwd.lxdbr0 {
    type filter hook forward priority filter; policy accept;
    ip version 4 oifname "lxdbr0" accept
    ip version 4 iifname "lxdbr0" accept
    ip6 version 6 oifname "lxdbr0" accept
    ip6 version 6 iifname "lxdbr0" accept
  }

  chain in.lxdbr0 {
    type filter hook input priority filter; policy accept;
    iifname "lxdbr0" tcp dport 53 accept
    iifname "lxdbr0" udp dport 53 accept
    iifname "lo" tcp dport 53 accept
    iifname "lo" udp dport 53 accept
    ip daddr 172.18.0.1 tcp dport 53 drop
    ip daddr 172.18.0.1 udp dport 53 drop
    iifname "lxdbr0" icmp type { destination-unreachable, time-exceeded, parameter-problem } accept
    iifname "lxdbr0" udp dport 67 accept
    ip6 daddr fd39:d8bd:967c:bb6f::1 tcp dport 53 drop
    ip6 daddr fd39:d8bd:967c:bb6f::1 udp dport 53 drop
    iifname "lxdbr0" icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter
-problem, nd-router-solicit, nd-neighbor-solicit, nd-neighbor-advert, mld2-listener-report } accept
    iifname "lxdbr0" udp dport 547 accept
  }

  chain out.lxdbr0 {
    type filter hook output priority filter; policy accept;
    oifname "lxdbr0" tcp sport 53 accept
    oifname "lxdbr0" udp sport 53 accept
  }
}
```

&nbsp;

`-`

[![Monster](https://avatars.githubusercontent.com/u/47848582?s=96&v=4 "Boo!")](../README.md)
