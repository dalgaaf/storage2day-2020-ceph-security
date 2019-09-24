<!-- .slide: data-state="section-break" id="section-break-2" data-timing="10s" -->
# Intro


<!-- .slide: data-state="normal" id="intro-0" data-timing="20s" data-menu-title="Thread Actors" -->
## General considerations

### Threat Actors

* Nation-State Actors
* Organized Crime
* Highly Capable Groups (Hacktivist)
* Motivated Individuals Acting Alone (Insider)
* Script Kiddies


<!-- .slide: data-state="normal" id="intro-1" data-timing="20s" data-menu-title="General considerations" -->
## General considerations

### Is your Ceph:
* an internal cluster?
* exposed to customers?
* exposed to the internet?

### Understand:
* your security requirements and standards
* services you enable
* security risks implied
* who has access to your cluster


<!-- .slide: data-state="normal" id="intro-2" data-timing="20s" data-menu-title="Ceph Overview" data-background-image="images/ceph-stack.svg" data-background-size="auto 90%" -->


<!-- .slide: data-state="normal" id="intro-3" data-timing="20s" data-menu-title="Ceph Components" -->
## Ceph Components

# TODO: explain

* OSDs
* MONs
* MDS
* RadosGW
* MGR
  * Dashboard


<!-- .slide: data-state="normal" id="intro-3" data-timing="20s" data-menu-title="Ceph Networks" -->
## Ceph Networks

* IPv4 or IPv6

* public
  * interface for clients

* cluster
  * replication
  * recovery
  * heartbeat


<!-- .slide: data-state="normal" id="intro-4" data-timing="20s" data-menu-title="Ceph Networks - Ports" -->
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
