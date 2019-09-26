<!-- .slide: data-state="section-break" id="section-break-3" data-timing="10s" -->
# Attack Surface


<!-- .slide: data-state="normal" id="attack-0" data-timing="20s" data-menu-title="Attack Surface: misc" -->
## Attack Surface - General

### Generic Issues
* Not monitored systems and networks
* Not regulary updated/patched setups
* No automation
* Not hardened systems
* Not audited security requirements
* Not aware/trained system admins


<!-- .slide: data-state="normal" id="attack-1" data-timing="20s" data-menu-title="Attack Surface: DoS" -->
## Attack Surface - General

### Flaws and Bugs
* An issue in one daemon effects all daemons of this type!

### Denial of Service
* Open many connections <!-- .element class="fragment" -->
* Submit many/large/small or expensive IOs
* Use flaws to crash Ceph daemons <!-- .element class="fragment" -->
* Identify non-obvious but expensive features of client/cluster interfaces <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="attack-2" data-timing="20s" data-menu-title="Attack Surface: Network" -->
## Attack Surface - General

### Network

* Client/Cluster sessions prior Nautilus are not encrypted <!-- .element class="fragment" -->
  * Sniffer can recover any data read/written <!-- .element class="fragment" -->
* Sessions are authenticated with CephX <!-- .element class="fragment" -->
  * no impersonate clients or daemons
  * no man-in-the-middle attacks
  * no TCP session hijacking


<!-- .slide: data-state="normal" id="attack-3" data-timing="20s" data-menu-title="Attack Surface: " -->
## Attack Surface - Authentication

### CephX
* based on Kerberos <!-- .element class="fragment" -->
* unique key for each entity in the cluster <!-- .element class="fragment" -->
* Capabilities assigned to keys <!-- .element class="fragment" -->
* Keys/secrets are stored in the MONs <!-- .element class="fragment" -->
* Keys are usually stored plain-text on client machine <!-- .element class="fragment" -->

### Issues: <!-- .element class="fragment" -->
* Compromised hosts, stolen keys <!-- .element class="fragment" -->
* Leakage of keys <!-- .element class="fragment" -->
* Exploit flaws in the protocol/algorithm <!-- .element class="fragment" -->
* Wrong set /to wide capabilites for certain users<!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="attack-4" data-timing="20s" data-menu-title="Attack Surface: RGW" -->
## Attack Surface - Rados Gateway

<div>
    <img style="width: 30%; left: 70%; position: absolute" alt="RGW"
         data-src="images/rgw.svg" />
</div>

* S3/Swift <!-- .element class="fragment" -->
  * Network access only to RGW  <!-- .element class="fragment" -->
  * No direct access for clients to other daemon  <!-- .element class="fragment" -->
* RGW admin
  * add/remove users
  * admin tasks

* API attack surface

Note:
- typical http/https attacks


<!-- .slide: data-state="normal" id="attack-5" data-timing="20s" data-menu-title="Attack Surface: RBD" -->
## Attack Surface - RBD

<div>
    <img style="width: 100%; left: 35%; position: absolute" alt="RBD"
         data-src="images/rbd.svg" />
</div>

* RBD for virtualization: <!-- .element class="fragment" -->
  * Protection from hypervisor layer <!-- .element class="fragment" -->
  * At guest level:
    * No access to Ceph network
    * No access to CephX keys <!-- .element class="fragment" -->
  * Issue: 
    * hypervisor is software (see e.g. Venom)


<!-- .slide: data-state="normal" id="attack-6" data-timing="20s" data-menu-title="Attack Surface: RBD Host" -->
## Attack Surface - RBD Host

<div>
    <img style="height: 100%; left: 35%; position: absolute" alt="RBD-Host"
         data-src="images/rbd-host.svg" />
</div>

* No protection through virtualization if KRBD used
* If host compromised (or KVM), attacker has access to:
  * Ceph Keys on the host <!-- .element class="fragment" -->
  * Ceph public network <!-- .element class="fragment" -->
  * Ceph daemons

Note: same applies to CephFS and also librados


<!-- .slide: data-state="normal" id="attack-7" data-timing="20s" data-menu-title="Attack Surface: CephFS" -->
## Attack Surface - CephFS

<div>
    <img style="width: 35%; left: 65%; position: absolute" alt="CephFS"
         data-src="images/cephfs.svg" />
</div>

* Direct access to public network required <!-- .element class="fragment" -->
* Same vectors like host attack, plus <!-- .element class="fragment" -->
  * access files of other users <!-- .element class="fragment" -->
  * fill up file system <!-- .element class="fragment" -->
  * privilege escalation <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="attack-9" data-timing="20s" data-menu-title="Attack Surface: MONs" -->
## Attack Surface - Ceph MONs

* Compromise Auth database <!-- .element class="fragment" -->
  * Inject keys <!-- .element class="fragment" -->
  * Manipulate key capabilities <!-- .element class="fragment" -->
  * Extract keys <!-- .element class="fragment" -->
* Manipulate config settings <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="attack-10" data-timing="20s" data-menu-title="Attack Surface: MGR" -->
## Attack Surface - Ceph Manager

* Utilize Ceph flaws to:
  * load existing modules <!-- .element class="fragment" -->
  * load malicious modules <!-- .element class="fragment" -->
* Replace valid module on disk with malicious code <!-- .element class="fragment" -->
* Modules aren't loaded dynamically
* Modules are currently not verified/signed/...


<!-- .slide: data-state="normal" id="attack-11" data-timing="20s" data-menu-title="Attack Surface: Dashboard" -->
## Attack Surface - Ceph Dashboard

* Webservice <!-- .element class="fragment" -->
  * typical HTTP(s) / API attack surface <!-- .element class="fragment" -->
  * Flaws in authentication <!-- .element class="fragment" -->
  * Role escalation
  * Brute-force attack on weak passwords
* Runs in Ceph Manager context
* Stores login information on several external services in MON KV-store


