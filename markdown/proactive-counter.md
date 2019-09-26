<!-- .slide: data-state="section-break" id="section-break-4" data-timing="10s" -->
# Proactive Countermeasures


<!-- .slide: data-state="normal" id="proact-1" data-timing="20s" data-menu-title="Proactive: Networks" -->
## Deployment and Setup

### Networks <!-- .element: class="fragment" data-fragment-index="0" -->
* Separate cluster and public <!-- .element: class="fragment" data-fragment-index="1" -->
  * either physically or e.g. w/ VLANs <!-- .element: class="fragment" data-fragment-index="1" -->
* Separate control nodes from other networks <!-- .element: class="fragment" data-fragment-index="2" -->
* Do not expose to the internet <!-- .element: class="fragment" data-fragment-index="3" -->
* Encrypt inter-datacenter traffic <!-- .element: class="fragment" data-fragment-index="4" -->
* Enable Ceph client host ip:port(s) in firewall <!-- .element: class="fragment" data-fragment-index="5" -->


<!-- .slide: data-state="normal" id="proact-2" data-timing="20s" data-menu-title="Proactive: Hyper-converged" -->
## Deployment and Setup

### Hyper-converged infra <!-- .element: class="fragment" data-fragment-index="0" -->
* Avoid if possible <!-- .element: class="fragment" data-fragment-index="1" -->
  * separate compute and storage <!-- .element: class="fragment" data-fragment-index="2" -->
  * scale them independently <!-- .element: class="fragment" data-fragment-index="3" -->
  * some degree of risk mitigation if daemons are compromided or DoS'd <!-- .element: class="fragment" data-fragment-index="4" -->
  * Do not mix control nodes with compute/storage <!-- .element: class="fragment" data-fragment-index="5" -->
* At least use hardened container setup <!-- .element: class="fragment" data-fragment-index="6" -->
  * as hypervisor: it's still software <!-- .element: class="fragment" data-fragment-index="6" -->


<!-- .slide: data-state="normal" id="proact-3" data-timing="20s" data-menu-title="Proactive: CephX" -->
## Deployment and Setup

### CephX <!-- .element: class="fragment" data-fragment-index="0" -->
* Always enable authentication <!-- .element: class="fragment" data-fragment-index="1" -->

<pre><!-- .element: class="fragment" data-fragment-index="2" --><code>
auth_cluster_required = cephx
auth_service_required = cephx
auth_client_required = cephx
</code></pre>

* <!-- .element: class="fragment" data-fragment-index="3" --> If possible use Ceph >= Nautilus release (CEPHX_V2)

Note: see CVEs


<!-- .slide: data-state="normal" id="proact-4" data-timing="20s" data-menu-title="Proactive: CephX" -->
## Deployment and Setup

### CephX Key management <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="1" --> Separate key for each client/user
* <!-- .element: class="fragment" data-fragment-index="2" --> Restrict users to __absolute minimum__ required caps
* <!-- .element: class="fragment" data-fragment-index="3" --> Distribute keys __only where absolutely__ needed
* <!-- .element: class="fragment" data-fragment-index="4" --> Limit permissions to key files
* <!-- .element: class="fragment" data-fragment-index="5" --> Limit administrator power
  * <!-- .element: class="fragment" data-fragment-index="6" --> may use keys with 'read-only' caps
  * <!-- .element: class="fragment" data-fragment-index="7" --> restrict __profile role-definer__ or __'allow *'__ keys
  * <!-- .element: class="fragment" data-fragment-index="8" --> admin keys __MUST__ only be distribute to admin/management nodes 

### TODOs: <!-- .element: class="fragment" data-fragment-index="9" -->
* <!-- .element: class="fragment" data-fragment-index="9" --> implement counterpart to __allow__ to strip caps

Note:
* Limit permissions to key files (admin=root, user=user,root)


<!-- .slide: data-state="normal" id="proact-5" data-timing="20s" data-menu-title="Proactive: Hardening" -->
## Deployment and Setup

### Hardening <!-- .element: class="fragment" data-fragment-index="0" -->

* Harden your base system <!-- .element: class="fragment" data-fragment-index="1" -->
* Run non-root Ceph daemons <!-- .element: class="fragment" data-fragment-index="2" -->
  * no escalation to root privileges <!-- .element: class="fragment" data-fragment-index="3" -->
  * run as 'ceph' user and group <!-- .element: class="fragment" data-fragment-index="3" -->
* MAC <!-- .element: class="fragment" data-fragment-index="4" -->
  * SELinux / AppArmor <!-- .element: class="fragment" data-fragment-index="5" -->
  * SELinux profiles available <!-- .element: class="fragment" data-fragment-index="5" -->
* May run (some daemons) in containers or VMs <!-- .element: class="fragment" data-fragment-index="6" -->
  * MONs and RGWs <!-- .element: class="fragment" data-fragment-index="6" -->


<!-- .slide: data-state="normal" id="proact-5.1" data-timing="20s" data-menu-title="Proactive: Hardening" -->
## Deployment and Setup

### Denial of Service Attacks <!-- .element: class="fragment" data-fragment-index="0" -->

* Limit load from clients <!-- .element: class="fragment" data-fragment-index="1" -->
  * RBD: use qemu throtteling features <!-- .element: class="fragment" data-fragment-index="2" -->
  * CephFS/RGW: use quotas <!-- .element: class="fragment" data-fragment-index="2" -->
* Monitoring! <!-- .element: class="fragment" data-fragment-index="3" -->
  * Check e.g. for false attempts on authentication <!-- .element: class="fragment" data-fragment-index="4" -->
  * consider automatically blacklist IPs in special scenarios <!-- .element: class="fragment" data-fragment-index="5" -->

<pre><!-- .element: class="fragment" data-fragment-index="5" --><code>
ceph osd blacklist add ADDRESS[:source_port] [TIME]
</code></pre>

#### TODO: <!-- .element: class="fragment" data-fragment-index="7" -->
  * Limit max open sockets per OSD/source IP <!-- .element: class="fragment" data-fragment-index="7" -->
  * Throttle operations per-session/-client <!-- .element: class="fragment" data-fragment-index="7" -->

Note: limit on max open sockets per IP may be done on network layer


<!-- .slide: data-state="normal" id="proact-6" data-timing="20s" data-menu-title="Proactive: CephX" -->
## Deployment and Setup

### Encryption - Data at Rest

* ceph-volme supports dm-crypt <!-- .element: class="fragment" data-fragment-index="1" -->
  * Encrypt raw block device (OSD and WAL/DB) <!-- .element: class="fragment" data-fragment-index="2" -->
  * Separate key for each volume <!-- .element: class="fragment" data-fragment-index="3" -->
  * No performance impact with modern processors <!-- .element: class="fragment" data-fragment-index="4" -->
  * Allows disks to be safely discarded if key remains secret <!-- .element: class="fragment" data-fragment-index="5" -->
* Encryption keys are stored in the MON <!-- .element: class="fragment" data-fragment-index="6" -->
  * Get a regular protected backup copy of the keys <!-- .element: class="fragment" data-fragment-index="7" -->
  * Limit access to these config keys (CephX) <!-- .element: class="fragment" data-fragment-index="7" -->


<!-- .slide: data-state="normal" id="proact-7" data-timing="20s" data-menu-title="Proactive: CephX" -->
## Deployment and Setup

### Encryption - On Wire

* <!-- .element: class="fragment" data-fragment-index="1" --> Protect data from listener on networks
* <!-- .element: class="fragment" data-fragment-index="2" --> Starting with Nautilus enable messenger v2 protocol

<pre><!-- .element: class="fragment" data-fragment-index="3" --><code>
 ceph mon enable-msgr2
</code></pre>

* <!-- .element: class="fragment" data-fragment-index="4" --> enable ``secure`` mode for encryption (AES-GCM stream cipher)

<pre><!-- .element: class="fragment" data-fragment-index="4" --><code>
 ms_cluster_mode = secure
 ms_service_mode = secure
 ms_client_mode = secure
 ms_mon_cluster_mode = secure
 ms_mon_service_mode = secure
 ms_mon_client_mode = secure
</code></pre>

Note:
* Alternatives: client-side encryption


<!-- .slide: data-state="normal" id="proact-8" data-timing="20s" data-menu-title="Proactive: RGW" -->
## Deployment and Setup

<div>
    <img style="width: 100%; left: 35%; position: absolute" alt="RGW"
         data-src="images/rgw-appliance.svg" />
</div> <!-- .element: class="fragment" data-fragment-index="3" -->

### Rados Gateway

* Big and easy taget through HTTP(s) protocol <!-- .element: class="fragment" data-fragment-index="1" -->
* Allways enable SSL/HTTPs <!-- .element: class="fragment" data-fragment-index="2" -->
* Small appliance in front of RGW <!-- .element: class="fragment" data-fragment-index="3" -->
  * Seprate Network (e.g. one per consumer) <!-- .element: class="fragment" data-fragment-index="4" -->
  * SSL terminated proxy forwarding to RGW <!-- .element: class="fragment" data-fragment-index="5" -->
  * WAF (mod_security) to filter API request <!-- .element: class="fragment" data-fragment-index="6" -->
    * allows e.g. blockage of admin API <!-- .element: class="fragment" data-fragment-index="6" -->
* Don't share buckets/users between consumers <!-- .element: class="fragment" data-fragment-index="7" -->
<br>


<!-- .slide: data-state="normal" id="proact-9" data-timing="20s" data-menu-title="Proactive: CephFS" -->
## Deployment and Setup

### CephFS

* No standard virtualization layer <!-- .element: class="fragment" data-fragment-index="1" -->
  * Filesystem passthrough (9p/virtfs) to host <!-- .element: class="fragment" data-fragment-index="2" -->
  * Direct access from host/VM <!-- .element: class="fragment" data-fragment-index="3" -->
* Run CephFS-only cluster, do not mix <!-- .element: class="fragment" data-fragment-index="4" -->
* Enable and set quotas <!-- .element: class="fragment" data-fragment-index="5" -->
* Alternativly proxy through NFS gateway <!-- .element: class="fragment" data-fragment-index="6" -->

Note: 
- 9p: performance impact
- NFS: complexer setup, performance impact


<!-- .slide: data-state="normal" id="proact-10" data-timing="20s" data-menu-title="Proactive: CephFS" -->
## Deployment and Setup

### CephFS - Access Control

* Path restrictions on mount <!-- .element: class="fragment" data-fragment-index="1" -->

<pre><!-- .element: class="fragment" data-fragment-index="2" --><code>
ceph fs authorize cephfs client.foo /bar rw
</code></pre>

* Snapshots restrictions: enable only if needed <!-- .element: class="fragment" data-fragment-index="3" -->
* In complex setups consider network restrictions <!-- .element: class="fragment" data-fragment-index="4" -->

<pre><!-- .element: class="fragment" data-fragment-index="5" --><code>
caps: [mds] allow r network 10.0.0.0/8, allow rw path=/bar
caps: [mon] allow r network 10.0.0.0/8
caps: [osd] allow rw tag cephfs data=cephfs_a network 10.0.0.0/8
</code></pre>

* Limit user by uid/gids <!-- .element: class="fragment" data-fragment-index="6" -->

<pre><!-- .element: class="fragment" data-fragment-index="7" --><code>
caps: [mds] allow rw uid=1 gids=1,2
</code></pre>

Note: 
- network restrictions: e.g. with multiple CephFS instances


<!-- .slide: data-state="normal" id="proact-11" data-timing="20s" data-menu-title="Proactive: Manager" -->
## Deployment and Setup

### Ceph Manager

* Monitor loading of modules on start <!-- .element class="fragment" -->
* Ensure only root/ceph user can access the module directories <!-- .element class="fragment" -->
* Use MAC to control access to modules <!-- .element class="fragment" -->
* Run ceph-mgr in a container <!-- .element class="fragment" -->

### TODO: <!-- .element class="fragment" -->
* Verification of modules? <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="proact-12" data-timing="20s" data-menu-title="Proactive: Dashboard" -->
## Deployment and Setup

### Ceph Dashboard

* Enable SSL/TLS <!-- .element class="fragment" -->
* User accounts <!-- .element class="fragment" -->
  * enforce strong passwords (WIP for Octopus) <!-- .element class="fragment" -->
  * Cleanup users <!-- .element class="fragment" -->
  * Limit user roles, security scopes and permissions to minimum <!-- .element class="fragment" -->
* Monitor ceph auth log <!-- .element class="fragment" -->
* Consider using a WAF (mod_security) <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="proact-20" data-timing="20s" data-menu-title="Proactive: Defects" -->
## Community

### Preventing Breaches - Defects

* Regular Static Code Analysis (SCA) <!-- .element: class="fragment" data-fragment-index="0" -->
  * Coverity scans <!-- .element: class="fragment" data-fragment-index="1" -->
  * cppcheck <!-- .element: class="fragment" data-fragment-index="1" -->
  * LLVM: clang/scan-build <!-- .element: class="fragment" data-fragment-index="1" -->
  * python code checker <!-- .element: class="fragment" data-fragment-index="1" -->
* Runtime Analysis <!-- .element: class="fragment" data-fragment-index="2" -->
  * valgrind memcheck <!-- .element: class="fragment" data-fragment-index="2" -->
* Code review process <!-- .element: class="fragment" data-fragment-index="3" -->


<!-- .slide: data-state="normal" id="proact-21" data-timing="20s" data-menu-title="Proactive: Testing" -->
## Community

### Preventing Breaches - Testing

* Unit tests and QA with each pull request <!-- .element: class="fragment" data-fragment-index="1" -->
* Pen-testing (WIP) <!-- .element: class="fragment" data-fragment-index="2" -->
  * human attempt to subvert security, code review <!-- .element: class="fragment" data-fragment-index="2" -->
* Fuzz testing (WIP) <!-- .element: class="fragment" data-fragment-index="3" -->
  * automated attempt to subvert or crash by feeding garbade input <!-- .element: class="fragment" data-fragment-index="3" -->


<!-- .slide: data-state="normal" id="proact-22" data-timing="20s" data-menu-title="Proactive: Hardening" -->
## Community

### Preventing Breaches - Build Hardening

* Harden build <!-- .element: class="fragment" data-fragment-index="1" -->
  * done by all distros with different settings <!-- .element: class="fragment" data-fragment-index="2" -->
  * -fPIE -fPIC <!-- .element: class="fragment" data-fragment-index="3" -->
  * -fstack-protector-strong <!-- .element: class="fragment" data-fragment-index="3" -->
  * -fstack-clash-protection <!-- .element: class="fragment" data-fragment-index="3" -->
  * LDFLAGS=-Wl,-z,relro -Wl,-z,now <!-- .element: class="fragment" data-fragment-index="3" -->

