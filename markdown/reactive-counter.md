<!-- .slide: data-state="section-break" id="section-break-5" data-timing="10s" -->
# Reactive Countermeasures


<!-- .slide: data-state="normal" id="react-1" data-timing="20s" data-menu-title="Reactive: Breaches" -->
## Detecting and Preventing Breaches

### Brute force attacks on authentication
* Logging of any failed attempt
* Monitoring is easy
* TODO:
  * Automatic blacklisting of IPs/clients after n-failed attempts

### Unauthorized injection of keys
* Monitoring on the audit log
  * trigger alerts for auth events
* Periodic comparison with signed backup of auth keys
  * trigger alerts on changes of caps

Note:
- TODO is unfortunately open since 2015


<!-- .slide: data-state="normal" id="react-2" data-timing="20s" data-menu-title="Reactive: SecProcess" -->
## Security Process

### Community
* Single point of contact for issues: security@ceph.io
  * Not a mailing list you can subscribe to!
    * Core development team
    * Security teams of distributions
    * Selected community members
* Simply write an email w/:
  * Description of the issue
  * Affected Ceph Version
  * How to reproduce, Proof of Concept
  * Patch
* Security team will contact you


<!-- .slide: data-state="normal" id="react-3" data-timing="20s" data-menu-title="Reactive: SecProcess" -->
## Security Process

### Responsible disclosure process
* Strict SLA on issues raised with distros
* RedHat security team drives CVE process
* Escalation process to Ceph developers
* Security related fixes are prioritized and backported
* Releases may be accelerated on ad-hoc basis
* Issue gets disclosed after agreed time frame
* Security advisories to ceph-announce@ceph.io

