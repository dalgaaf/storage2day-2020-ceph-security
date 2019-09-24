<!-- .slide: data-state="section-break" id="section-break-4" data-timing="10s" -->
# Proactive Countermeasures


<!-- .slide: data-state="normal" id="proact-1" data-timing="20s" data-menu-title="Proactive: Networks" -->
## Deployment and Setup

### Networks
* Separate cluster and public
  * either physically or e.g. w/ VLANs
* Separate control nodes from other networks
* Do not expose to the internet
* Encrypt inter-datacenter traffic


<!-- .slide: data-state="normal" id="proact-2" data-timing="20s" data-menu-title="Proactive: Hyper-converged" -->
## Deployment and Setup

### Hyper-converged infra
* Avoid if possible
  * separate compute and storage
  * scale them independently
  * some degree of risk mitigation if daemons are compromided or DoS'd
  * Do not mix control nodes with compute/storage
* At least use hardened container setup
  * as hypervisor: it's still software


<!-- .slide: data-state="normal" id="proact-3" data-timing="20s" data-menu-title="Proactive: CephX" -->
## Deployment and Setup

### CephX
* Always enable authentication

``` none
auth_cluster_required = cephx
auth_service_required = cephx
auth_client_required = cephx
```

* If possible use Ceph >= Nautilus release (CEPHX_V2)

Note: see CVEs


<!-- .slide: data-state="normal" id="proact-4" data-timing="20s" data-menu-title="Proactive: CephX" -->
## Deployment and Setup

### CephX Key management
* Separate key for each client/user
* Restrict users to __absolute minimum__ required caps
* Distribute keys __only where absolutely__ needed
* Limit administrator power
  * may use keys with 'read-only' caps
  * restrict __profile role-definer__ or __'allow *'__ keys
  * admin keys should only be distribute to admin/management nodes 

### TODOs:
* implement counterpart to __allow__ to strip caps


<!-- .slide: data-state="normal" id="proact-5" data-timing="20s" data-menu-title="Proactive: Hardening" -->
## Deployment and Setup

### Hardening

* Harden your base system
* Run non-root Ceph daemons
  * no escalation to root privileges
  * run as 'ceph' user and group

* MAC
  * SELinux / AppArmor
  * SELinux profiles available

* May run (some daemons) in containers or VMs
  * MONs and RGWs


<!-- .slide: data-state="normal" id="proact-5.1" data-timing="20s" data-menu-title="Proactive: Hardening" -->
## Deployment and Setup

### Denial of Service Attacks

* Limit load from clients
  * RBD: use qemu throtteling features
  * CephFS/RGW: use quotas
* Monitoring!
  * Check e.g. for false attempts on authentication
  * consider automatically blacklist IPs in special scenarios

```none
  ceph osd blacklist add ADDRESS[:source_port] [TIME]
```

* TODO:
  * Limit max open sockets per OSD/source IP
  * Throttle operations per-session/-client

Note: limit on max open sockets per IP may be done on network layer


<!-- .slide: data-state="normal" id="proact-6" data-timing="20s" data-menu-title="Proactive: CephX" -->
## Deployment and Setup

### Encryption - Data at Rest

* ceph-volme supports dm-crypt
  * Encrypt raw block device (OSD and WAL/DB)
  * Separate key for each volume
  * No performance impact with modern processors
  * Allows disks to be safely discarded if key remains secret
* Encryption keys are stored in the MON
  * Get a regular protected backup copy of the keys
  * Limit access to these config keys (CephX)


<!-- .slide: data-state="normal" id="proact-7" data-timing="20s" data-menu-title="Proactive: CephX" -->
## Deployment and Setup

### Encryption - On Wire

* Protect data from listener on networks
* Since Nautilus: Encryption to MONs
  * protects e.g. configuring keys
* Currently not supported in Ceph for data payload, but planed
* Alternatives:
  * RBD: use dm-crypt
  * others: encrypt on client side
  * may consider IPSec


<!-- .slide: data-state="normal" id="proact-8" data-timing="20s" data-menu-title="Proactive: RGW" -->
## Deployment and Setup

<div>
    <img style="width: 100%; left: 35%; position: absolute" alt="RGW"
         data-src="images/rgw-appliance.svg" />
</div>

### Rados Gateway

* Big and easy taget through HTTP(s) protocol
* Allways enable SSL/HTTPs
* Small appliance in front of RGW
  * Seprate Network (e.g. one per consumer)
  * SSL terminated proxy forwarding to RGW
  * WAF (mod_security) to filter API request
    * allows e.g. blockage of admin API
* Don't share buckets/users between consumers
<br>


<!-- .slide: data-state="normal" id="proact-9" data-timing="20s" data-menu-title="Proactive: CephFS" -->
## Deployment and Setup

### CephFS

* No standard virtualization layer
  * Proxy through NFS gateway
  * Filesystem passthrough (9p/virtfs) to host
  * Direct access from host/VM
* Enable and set quotas

Note: 
- 9p: performance impact
- NFS: complexer setup, performance impact


<!-- .slide: data-state="normal" id="proact-10" data-timing="20s" data-menu-title="Proactive: CephFS" -->
## Deployment and Setup

### CephFS - Access Control

* Path restrictions on mount

```none
ceph fs authorize cephfs client.foo /bar rw
```
* Snapshots restrictions: enable only if needed
* In complex setups consider network restrictions

```none
caps: [mds] allow r network 10.0.0.0/8, allow rw path=/bar
caps: [mon] allow r network 10.0.0.0/8
caps: [osd] allow rw tag cephfs data=cephfs_a network 10.0.0.0/8
```
* Limit user by uid/gids

```none
caps: [mds] allow rw uid=1 gids=1,2
```

Note: 
- network restrictions: e.g. with multiple CephFS instances


<!-- .slide: data-state="normal" id="proact-11" data-timing="20s" data-menu-title="Proactive: CephFS" -->
## Deployment and Setup

### Ceph Dashboard

# TODO !!!


<!-- .slide: data-state="normal" id="proact-20" data-timing="20s" data-menu-title="Proactive: Defects" -->
## Community

### Preventing Breaches - Defects

* Regular Static Code Analysis (SCA)
  * Coverity scans
  * cppcheck
  * LLVM: clang/scan-build
  * python code checker
* Runtime Analysis
  * valgrind memcheck
* Code review process


<!-- .slide: data-state="normal" id="proact-21" data-timing="20s" data-menu-title="Proactive: Testing" -->
## Community

### Preventing Breaches - Testing

* Unit tests and QA with each pull request
* Pen-testing (WIP)
  * human attempt to subvert security, code review
* Fuzz testing (WIP)
  * automated attempt to subvert or crash by feeding garbade input


<!-- .slide: data-state="normal" id="proact-22" data-timing="20s" data-menu-title="Proactive: Hardening" -->
## Community

### Preventing Breaches - Hardening

* Harden build
  * done by all distros with different settings
  * -fPIE -fPIC
  * -fstack-protector-strong
  * -fstack-clash-protection
  * LDFLAGS=-Wl,-z,relro -Wl,-z,now

