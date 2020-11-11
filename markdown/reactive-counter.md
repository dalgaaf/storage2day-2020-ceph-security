<!-- .slide: data-state="section-break" id="section-break-5" data-timing="10s" -->
# Reactive Countermeasures


<!-- .slide: data-state="normal" id="react-1" data-timing="20s" data-menu-title="Reactive: Breaches" -->
## Detecting and Preventing Breaches

### Brute force attacks on authentication <!-- .element: class="fragment" data-fragment-index="1" -->
* Logging of any failed attempt <!-- .element: class="fragment" data-fragment-index="2" -->
* Monitoring is easy <!-- .element: class="fragment" data-fragment-index="3" -->
* TODO: <!-- .element: class="fragment" data-fragment-index="4" -->
  * Automatic blacklisting of IPs/clients after n-failed attempts <!-- .element: class="fragment" data-fragment-index="4" -->

### Unauthorized injection of keys <!-- .element: class="fragment" data-fragment-index="5" -->
* Monitoring on the audit log <!-- .element: class="fragment" data-fragment-index="6" -->
  * trigger alerts for auth events <!-- .element: class="fragment" data-fragment-index="6" -->
* Periodic comparison with signed backup of auth keys <!-- .element: class="fragment" data-fragment-index="7" -->
  * trigger alerts on changes of caps <!-- .element: class="fragment" data-fragment-index="7" -->

Note:
- TODO is unfortunately open since 2015


<!-- .slide: data-state="normal" id="react-2" data-timing="20s" data-menu-title="Reactive: SecProcess" -->
## Security Process

### Community <!-- .element: class="fragment" data-fragment-index="1" -->
* Single point of contact for issues: security@ceph.io <!-- .element: class="fragment" data-fragment-index="2" -->
  * Not a mailing list you can subscribe to! <!-- .element: class="fragment" data-fragment-index="3" -->
    * Core development team <!-- .element: class="fragment" data-fragment-index="4" -->
    * Security teams of distributions <!-- .element: class="fragment" data-fragment-index="4" -->
    * Selected community members <!-- .element: class="fragment" data-fragment-index="4" -->
* Simply write an email w/: <!-- .element: class="fragment" data-fragment-index="5" -->
  * Description of the issue <!-- .element: class="fragment" data-fragment-index="6" -->
  * Affected Ceph Version <!-- .element: class="fragment" data-fragment-index="6" -->
  * How to reproduce / Proof of Concept <!-- .element: class="fragment" data-fragment-index="6" -->
  * Patches are welcome! <!-- .element: class="fragment" data-fragment-index="6" -->
* Security team will contact you <!-- .element: class="fragment" data-fragment-index="7" -->


<!-- .slide: data-state="normal" id="react-3" data-timing="20s" data-menu-title="Reactive: SecProcess" -->
## Security Process

### Community - Responsible disclosure process
* Strict SLA on issues raised with distros <!-- .element class="fragment" -->
* Community security team drives CVE process <!-- .element class="fragment" -->
* Escalation process to Ceph developers <!-- .element class="fragment" -->
* Security related fixes are prioritized and backported <!-- .element class="fragment" -->
* Releases may be accelerated on ad-hoc basis <!-- .element class="fragment" -->
* Issue gets disclosed after agreed time frame <!-- .element class="fragment" -->
* Security advisories to ceph-announce@ceph.io <!-- .element class="fragment" -->

