<!-- .slide: data-state="section-break" id="section-break-2.2" data-timing="10s" -->
# Data Management


<!-- .slide: data-state="normal" id="data-1" data-timing="20s" data-menu-title="Thread Actors" -->
## Data Distribution

### Replication <!-- .element: class="fragment" data-fragment-index="0" -->
* copy each object n-times <!-- .element: class="fragment" data-fragment-index="0" -->
* at least 200% overhead (3x) <!-- .element: class="fragment" data-fragment-index="0" -->
* fast read <!-- .element: class="fragment" data-fragment-index="0" -->
* quicker recovery <!-- .element: class="fragment" data-fragment-index="0" -->

### Erasure Coding (EC) <!-- .element: class="fragment" data-fragment-index="1" -->
* one copy plus parity <!-- .element: class="fragment" data-fragment-index="1" -->
* space effective <!-- .element: class="fragment" data-fragment-index="1" -->
* performance impact on small objects <!-- .element: class="fragment" data-fragment-index="1" -->
* expensive recovery <!-- .element: class="fragment" data-fragment-index="1" -->

Note:
- read on replication faster due to fact that k objects need to read (latency, CPU)


<!-- .slide: data-state="normal" id="data-2" data-timing="20s" data-menu-title="Replication Diagram" -->
## Replication
<div>
  <center><img data-src="images/replica_explained.svg" style="width:35%"></center>
</div>


<!-- .slide: data-state="normal" id="data-3" data-timing="20s" data-menu-title="Erasure Coding Diagram" -->
## Erasure Coding
<div>
  <center><img data-src="images/ec_explained_extra.svg" style="width:65%"></center>
</div>

Note:
- Object is split into *k* chunks
- Additonal *m* coding chunks will be created (encoded)
- chunks/shards will be distributed as defined in crush and erasure code profile


<!-- .slide: data-state="normal" id="data-4" data-timing="20s" data-menu-title="Thread Actors" -->
## Data Integrity

### Maintain data consistency and cleanliness
* Scrub:
  * compare object metadata in one PG with it peers on other OSDs
  * usually performed daily
  * catches bugs and flaws
* Deep Scrub:
  * comparing data in objects bit-by-bit
  * usually performed weekly
  * catches e.g. bad sectors not found by normal scrubbing
* CephFS provides own additional scubbing
  * Forward scrub to ensure fs conistency
  * Backward scrub to verify each RADOS object


<!-- .slide: data-state="normal" id="data-5" data-timing="20s" data-menu-title="General considerations" -->
## Data Deletion

* Deleting RBD/RGW/CephFS objects Ceph destroys object on Rados
* Deletion of a pool does destroy all related Rados objects
* Objects are not recoverable after deletion
* Residual data artifacs may reside on storage media till overwritten
* CephFS:
  * File marked as deleted in MDS
  * Rados objects delayed lazily
* Keep in mind:
  * Snaphots may still hold data
  * Client side encryption of data protects if key destroyed

