<!-- .slide: data-state="section-break" id="section-break-2" data-timing="10s" -->
# Intro


<!-- .slide: data-state="normal" id="intro-2" data-timing="20s" data-menu-title="Ceph Overview" data-background-image="images/ceph-stack.svg" data-background-size="auto 90%" -->


<!-- .slide: data-state="normal" id="intro-3" data-timing="20s" data-menu-title="Ceph Components" -->
## Ceph Components

### Monitors (MON) <!-- .element: class="fragment" data-fragment-index="0" -->
* lightweight daemon <!-- .element: class="fragment" data-fragment-index="1" -->
* paxos protocol, odd number <!-- .element: class="fragment" data-fragment-index="1" -->
* maintains maps of the cluster state <!-- .element: class="fragment" data-fragment-index="1" -->
* authentication (CephX) <!-- .element: class="fragment" data-fragment-index="1" -->

### Object Storage Daemon (OSD) <!-- .element: class="fragment" data-fragment-index="2" -->
* smart storage daemon, coordinates with peers <!-- .element: class="fragment" data-fragment-index="3" -->
* handles data replication, recovery, backfilling, and rebalancing <!-- .element: class="fragment" data-fragment-index="3" -->
* BlueStore <!-- .element: class="fragment" data-fragment-index="4" -->
  * utilize raw storage device <!-- .element: class="fragment" data-fragment-index="5" -->
  * Object data, RocksDB (kv-store), Write-ahead log of RocksDB <!-- .element: class="fragment" data-fragment-index="5" -->


<!-- .slide: data-state="normal" id="intro-3" data-timing="20s" data-menu-title="Ceph Components" -->
## Ceph Components

### Metadata Server (MDS) <!-- .element: class="fragment" data-fragment-index="0" -->
* metadata for posix-compliant shared filesystem (CephFS) <!-- .element: class="fragment" data-fragment-index="1" -->
  * directory hierachy <!-- .element: class="fragment" data-fragment-index="1" -->
  * file metadata <!-- .element: class="fragment" data-fragment-index="1" -->
* multi-MDS support multi-active, standby, standby-replay, hot-standby <!-- .element: class="fragment" data-fragment-index="2" -->
* coordinate access <!-- .element: class="fragment" data-fragment-index="2" -->

### Rados Gateway (RGW) <!-- .element: class="fragment" data-fragment-index="3" -->
* RESTful gateway <!-- .element: class="fragment" data-fragment-index="4" -->
  * Amazon S3 <!-- .element: class="fragment" data-fragment-index="4" -->
  * Swift <!-- .element: class="fragment" data-fragment-index="4" -->
* Separate user management <!-- .element: class="fragment" data-fragment-index="5" -->


<!-- .slide: data-state="normal" id="intro-4" data-timing="20s" data-menu-title="Ceph Components" -->
## Ceph Components

### Ceph Manager Daemon (MGR) <!-- .element: class="fragment" data-fragment-index="0" -->
* runs alongside MONs to provide <!-- .element: class="fragment" data-fragment-index="1" -->
  * additional monitoring <!-- .element: class="fragment" data-fragment-index="2" -->
  * interface to external monitoring <!-- .element: class="fragment" data-fragment-index="2" -->
  * interface to external management/orchestrators <!-- .element: class="fragment" data-fragment-index="2" -->
* Flexible through modules, loaded via a python subinterpretor <!-- .element: class="fragment" data-fragment-index="3" -->

### Ceph Dashboard Module  <!-- .element: class="fragment" data-fragment-index="4" -->
* built-in web-based management and monitoring <!-- .element: class="fragment" data-fragment-index="5" -->
* Multi-User and Role Management <!-- .element: class="fragment" data-fragment-index="5" -->
* Single Sign-On <!-- .element: class="fragment" data-fragment-index="5" -->
* SSL/TLS support <!-- .element: class="fragment" data-fragment-index="5" -->
* Auditing <!-- .element: class="fragment" data-fragment-index="5" -->


<!-- .slide: data-state="normal" id="intro-5" data-timing="20s" data-menu-title="Ceph Networks" -->
## Ceph Networks

* IPv4 or IPv6 <!-- .element: class="fragment" data-fragment-index="0" -->
* public <!-- .element: class="fragment" data-fragment-index="1" -->
  * interface for clients <!-- .element: class="fragment" data-fragment-index="1" -->
* cluster <!-- .element: class="fragment" data-fragment-index="2" -->
  * replication <!-- .element: class="fragment" data-fragment-index="3" -->
  * recovery <!-- .element: class="fragment" data-fragment-index="4" -->
  * heartbeat <!-- .element: class="fragment" data-fragment-index="5" -->


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

