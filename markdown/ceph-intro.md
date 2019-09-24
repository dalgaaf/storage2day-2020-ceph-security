<!-- .slide: data-state="section-break" id="section-break-2" data-timing="10s" -->
# Intro


<!-- .slide: data-state="normal" id="intro-2" data-timing="20s" data-menu-title="Ceph Overview" data-background-image="images/ceph-stack.svg" data-background-size="auto 90%" -->


<!-- .slide: data-state="normal" id="intro-3" data-timing="20s" data-menu-title="Ceph Components" -->
## Ceph Components

### Monitors (MON)
* lightweight daemon
* paxos protocol, odd number
* maintains maps of the cluster state
* authentication (CephX)

### Object Storage Daemon (OSD)
* smart storage daemon, coordinates with peers
* handles data replication, recovery, backfilling, and rebalancing
* BlueStore
  * utilize raw storage device
  * Object data, RocksDB (kv-store), Write-ahead log of RocksDB


<!-- .slide: data-state="normal" id="intro-3" data-timing="20s" data-menu-title="Ceph Components" -->
## Ceph Components

### Metadata Server (MDS)
* metadata for posix-compliant shared filesystem (CephFS)
  * directory hierachy
  * file metadata
* multi-MDS support  multi-active, standby, standby-replay, hot-standby)
* coordinate access

### Rados Gateway (RGW)
* RESTful gateway
  * Amazon S3
  * Swift
* Separate user management


<!-- .slide: data-state="normal" id="intro-4" data-timing="20s" data-menu-title="Ceph Components" -->
## Ceph Components

### Ceph Manager Daemon (MGR)
* runs alongside MONs to provide
  * additional monitoring
  * interface to external monitoring
  * interface to external management/orchestrators
* Flexible through modules, loaded via a python subinterpretor

### Ceph Dashboard Module 
* built-in web-based management and monitoring
* Multi-User and Role Management
* Single Sign-On
* SSL/TLS support
* Auditing


<!-- .slide: data-state="normal" id="intro-5" data-timing="20s" data-menu-title="Ceph Networks" -->
## Ceph Networks

* IPv4 or IPv6
* public
  * interface for clients
* cluster
  * replication
  * recovery
  * heartbeat


<!-- .slide: data-state="normal" id="intro-6" data-timing="20s" data-menu-title="Ceph Networks - Ports" -->
## Ceph Networks - Ports

<table align="center">
<tr>
    <th>Ports</th>
    <th>Ceph Daemon</th>
</tr>
<tr>
    <td width="50%">3300, 6789</td>
    <td width="50%">ceph-mon (v1/v2)</td>
</tr>
<tr>
    <td>6800-7300</td>
    <td>ceph-osd, ceph-mon</td>
</tr>
<tr>
    <td>6800</td>
    <td>ceph-mds</td>
</tr>
<tr>
    <td>80, 443, 7480</td>
    <td>ceph-radosgw</td>
</tr>
<tr>
    <td>8080, 8443</td>
    <td>ceph-mgr Dashboard</td>
</tr>
</table>

Note: 
- ceph-radosgw: 80 Beast, 7480 Civetweb

