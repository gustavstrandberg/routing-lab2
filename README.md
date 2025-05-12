# Routing lab

This is a 2 spine, 2 racks routing lab. Spines are based on srlinux. Each rack has 2 leaf switches, running frr and 4 hosts running frr as well.

Rack 1 is fully based on ebgp with a ASN per leaf and host.
Rack 2 is fully based on ibgp with the leaf and hosts sharing 1 ASN.

## Depolying

```
guran@containerlab01:~/routing-lab2$ containerlab deploy
10:48:40 INFO Containerlab started version=0.68.0
10:48:40 INFO Parsing & checking topology file=srlfrr01.clab.yml
10:48:40 INFO Creating docker network name=clab IPv4 subnet=172.20.20.0/24 IPv6 subnet=3fff:172:20:20::/64 MTU=1500
10:48:40 ERRO node "spine01" (nokia_srlinux) has a minimum available memory requirement of 2 GB whilst only 1 GB memory is available
10:48:40 ERRO node "spine02" (nokia_srlinux) has a minimum available memory requirement of 2 GB whilst only 1 GB memory is available
10:48:40 INFO Creating lab directory path=/home/guran/routing-lab2/clab-routing-lab3
10:48:40 INFO Creating container name=r2-host04
10:48:40 INFO Creating container name=r2-leaf01
10:48:40 INFO Creating container name=r1-leaf02
10:48:40 INFO Creating container name=r2-host01
10:48:40 INFO Creating container name=r1-host03
10:48:40 INFO Creating container name=r1-leaf01
10:48:40 INFO Creating container name=r2-host05
10:48:40 INFO Creating container name=spine02
10:48:42 INFO Creating container name=r1-host01
10:48:42 INFO Creating container name=r2-host02
10:48:43 INFO Creating container name=r2-leaf02
10:48:43 INFO Created link: spine02:e1-1 (ethernet-1/1) ▪┄┄▪ r1-leaf01:eth2
10:48:43 INFO Created link: spine02:e1-3 (ethernet-1/3) ▪┄┄▪ r2-leaf01:eth2
10:48:44 INFO Running postdeploy actions kind=nokia_srlinux node=spine02
10:48:44 INFO Creating container name=r1-host04
10:48:44 INFO Created link: r2-host01:eth1 ▪┄┄▪ r2-leaf01:eth20
10:48:44 INFO Created link: spine02:e1-2 (ethernet-1/2) ▪┄┄▪ r1-leaf02:eth2
10:48:44 INFO Created link: r1-host03:eth1 ▪┄┄▪ r1-leaf01:eth22
10:48:45 INFO Created link: r2-host04:eth1 ▪┄┄▪ r2-leaf01:eth23
10:48:45 INFO Created link: r2-host05:eth1 ▪┄┄▪ r2-leaf01:eth24
10:48:45 INFO Creating container name=r2-host03
10:48:45 INFO Created link: r1-host03:eth2 ▪┄┄▪ r1-leaf02:eth22
10:48:45 INFO Creating container name=r1-host02
10:48:45 INFO Creating container name=spine01
10:48:46 INFO Created link: r1-host01:eth1 ▪┄┄▪ r1-leaf01:eth20
10:48:46 INFO Created link: r1-host01:eth2 ▪┄┄▪ r1-leaf02:eth20
10:48:46 INFO Creating container name=r1-host05
10:48:49 INFO Created link: r1-host04:eth1 ▪┄┄▪ r1-leaf01:eth23
10:48:49 INFO Created link: r1-host04:eth2 ▪┄┄▪ r1-leaf02:eth23
10:48:49 INFO Created link: r2-host02:eth1 ▪┄┄▪ r2-leaf01:eth21
10:48:50 INFO Created link: spine02:e1-4 (ethernet-1/4) ▪┄┄▪ r2-leaf02:eth2
10:48:50 INFO Created link: r2-host01:eth2 ▪┄┄▪ r2-leaf02:eth20
10:48:50 INFO Created link: r2-host02:eth2 ▪┄┄▪ r2-leaf02:eth21
10:48:50 INFO Created link: r2-host03:eth1 ▪┄┄▪ r2-leaf01:eth22
10:48:50 INFO Created link: r2-host03:eth2 ▪┄┄▪ r2-leaf02:eth22
10:48:50 INFO Created link: r2-host04:eth2 ▪┄┄▪ r2-leaf02:eth23
10:48:50 INFO Created link: spine01:e1-1 (ethernet-1/1) ▪┄┄▪ r1-leaf01:eth1
10:48:50 INFO Created link: spine01:e1-2 (ethernet-1/2) ▪┄┄▪ r1-leaf02:eth1
10:48:50 INFO Created link: spine01:e1-3 (ethernet-1/3) ▪┄┄▪ r2-leaf01:eth1
10:48:50 INFO Created link: spine01:e1-4 (ethernet-1/4) ▪┄┄▪ r2-leaf02:eth1
10:48:50 INFO Running postdeploy actions kind=nokia_srlinux node=spine01
10:48:51 INFO Created link: r1-host05:eth1 ▪┄┄▪ r1-leaf01:eth24
10:48:51 INFO Created link: r1-host02:eth1 ▪┄┄▪ r1-leaf01:eth21
10:48:51 INFO Created link: r1-host02:eth2 ▪┄┄▪ r1-leaf02:eth21


10:50:08 INFO Adding host entries path=/etc/hosts
10:50:09 INFO Adding SSH config for nodes path=/etc/ssh/ssh_config.d/clab-routing-lab3.conf
╭─────────────────────────────┬──────────────────────────────┬─────────┬────────────────────╮
│             Name            │          Kind/Image          │  State  │   IPv4/6 Address   │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r1-host01 │ linux                        │ running │ 172.20.20.10       │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::a  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r1-host02 │ linux                        │ running │ 172.20.20.16       │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::10 │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r1-host03 │ linux                        │ running │ 172.20.20.4        │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::4  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r1-host04 │ linux                        │ running │ 172.20.20.13       │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::d  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r1-host05 │ linux                        │ running │ 172.20.20.17       │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::11 │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r1-leaf01 │ linux                        │ running │ 172.20.20.2        │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::2  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r1-leaf02 │ linux                        │ running │ 172.20.20.9        │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::9  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r2-host01 │ linux                        │ running │ 172.20.20.8        │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::8  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r2-host02 │ linux                        │ running │ 172.20.20.11       │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::b  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r2-host03 │ linux                        │ running │ 172.20.20.14       │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::e  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r2-host04 │ linux                        │ running │ 172.20.20.3        │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::3  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r2-host05 │ linux                        │ running │ 172.20.20.7        │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::7  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r2-leaf01 │ linux                        │ running │ 172.20.20.6        │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::6  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-r2-leaf02 │ linux                        │ running │ 172.20.20.12       │
│                             │ quay.io/frrouting/frr:10.1.3 │         │ 3fff:172:20:20::c  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-spine01   │ nokia_srlinux                │ running │ 172.20.20.15       │
│                             │ ghcr.io/nokia/srlinux:latest │         │ 3fff:172:20:20::f  │
├─────────────────────────────┼──────────────────────────────┼─────────┼────────────────────┤
│ clab-routing-lab3-spine02   │ nokia_srlinux                │ running │ 172.20.20.5        │
│                             │ ghcr.io/nokia/srlinux:latest │         │ 3fff:172:20:20::5  │


```

## checking the status

You can get a console into the network by using the hostname combined with `docker exec`. Getting into host03 for rack 2 can be done with:

```
docker exec -it clab-routing-lab3-r2-host03 bash
```

you can check the routing table with running `ip r`. More useful commands on frr can be run through `vtysh`.

**BGP summary:**
```
r2-host03:/# vtysh 
% Can't open configuration file /etc/frr/vtysh.conf due to 'No such file or directory'.
Configuration file[/etc/frr/frr.conf] processing failure: 11

Hello, this is FRRouting (version 10.1.3_git).
Copyright 1996-2005 Kunihiro Ishiguro, et al.

2025/04/30 17:18:53 [YDG3W-JND95] FD Limit set: 1048576 is stupidly large.  Is this what you intended?  Consider using --limit-fds also limiting size to 100000
r2-host03# show bgp summary 

IPv4 Unicast Summary:
BGP router identifier 10.10.172.203, local AS number 65022 VRF default vrf-id 0
BGP table version 24
RIB entries 27, using 3456 bytes of memory
Peers 2, using 33 KiB of memory

Neighbor        V         AS   MsgRcvd   MsgSent   TblVer  InQ OutQ  Up/Down State/PfxRcd   PfxSnt Desc
r2-leaf01(eth1) 4      65022       190       177       24    0    0 00:08:40           12        1 FRRouting/10.1.3_git
r2-leaf02(eth2) 4      65022       190       178       24    0    0 00:08:41           12        1 FRRouting/10.1.3_git

Total number of neighbors 2
r2-host03# 
```

**Showing the path to host01 in rack1**

```
r2-host03# show bgp ipv4 10.10.172.101
BGP routing table entry for 10.10.172.101/32, version 20
Paths: (2 available, best #1, table default)
  Not advertised to any peer
  65001 65011 65101
    fe80::a8c1:abff:fe0a:fb76(r2-leaf01) from r2-leaf01(eth1) (10.10.20.1)
      Origin IGP, localpref 100, valid, internal, multipath, bestpath-from-AS 65001, best (Router ID)
      Last update: Wed Apr 30 17:10:34 2025
  65001 65011 65101
    fe80::a8c1:abff:fe3e:6168(r2-leaf02) from r2-leaf02(eth2) (10.10.20.2)
      Origin IGP, localpref 100, valid, internal, multipath
      Last update: Wed Apr 30 17:10:34 2025
```# routing-lab2
