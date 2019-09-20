<!-- .slide: data-state="section-break" id="section-break-3.1" data-timing="10s" -->
# Ceph Networks


<!-- .slide: data-state="normal" id="ceph-store-emails-0" data-timing="20s" data-menu-title="Ceph: Option CephFS" -->
## Ceph Network Security

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="CephFS"
         data-src="images/cephfs.svg" />
</div>

### CephFS

* requires direct access to storage network <!-- .element class="fragment" -->
* only for dedicated platform <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-store-emails-1" data-timing="20s" data-menu-title="Ceph: Option RBD" -->
## Ceph Network Security

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="RBD"
         data-src="images/rbd.svg" />
</div>

### RBD

* no direct access to storage network required <!-- .element class="fragment" -->
* secure through hypervisor abstraction (libvirt) <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-store-emails-2" data-timing="20s" data-menu-title="Ceph: Option RadosGW" -->
## Ceph Network Security

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="RGW"
         data-src="images/rgw.svg" />
</div>

#### <b>Security</b> <!-- .element class="fragment" -->
* no direct access to Ceph storage network required <!-- .element class="fragment" -->
* connection to RadosGW can be secured (WAF) <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-store-emails-3" data-timing="20s" data-menu-title="Ceph: Option librados" -->
## Ceph Network Security

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="librados"
         data-src="images/librados.svg" />
</div>

### Librados
* requires direct access to storage network <!-- .element class="fragment" -->
* only for dedicated platform <!-- .element class="fragment" -->

