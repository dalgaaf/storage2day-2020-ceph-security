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


<!-- .slide: data-state="normal" id="proact-3" data-timing="20s" data-menu-title="Proactive: CephX" -->
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


<!-- .slide: data-state="normal" id="proact-5" data-timing="20s" data-menu-title="Proactive: SCA" -->
## Preventing Breaches - Defects
