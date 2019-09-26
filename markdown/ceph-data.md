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

### Maintain data consistency and cleanliness <!-- .element: class="fragment" data-fragment-index="0" -->
* Scrub: <!-- .element: class="fragment" data-fragment-index="1" -->
  * compare object metadata in one PG with it peers on other OSDs <!-- .element: class="fragment" data-fragment-index="2" -->
  * usually performed daily <!-- .element: class="fragment" data-fragment-index="2" -->
  * catches bugs and flaws <!-- .element: class="fragment" data-fragment-index="2" -->
* Deep Scrub: <!-- .element: class="fragment" data-fragment-index="3" -->
  * comparing data in objects bit-by-bit <!-- .element: class="fragment" data-fragment-index="4" -->
  * usually performed weekly <!-- .element: class="fragment" data-fragment-index="4" -->
  * catches e.g. bad sectors not found by normal scrubbing <!-- .element: class="fragment" data-fragment-index="4" -->
* CephFS provides own additional scubbing <!-- .element: class="fragment" data-fragment-index="5" -->
  * Forward scrub to ensure fs conistency <!-- .element: class="fragment" data-fragment-index="6" -->
  * Backward scrub to verify each RADOS object <!-- .element: class="fragment" data-fragment-index="6" -->


<!-- .slide: data-state="normal" id="data-5" data-timing="20s" data-menu-title="General considerations" -->
## Data Deletion

* Deleting RBD/RGW/CephFS objects Ceph destroys object on Rados <!-- .element: class="fragment" data-fragment-index="0" -->
* Deletion of a pool does destroy all related Rados objects <!-- .element: class="fragment" data-fragment-index="1" -->
* Objects are not recoverable after deletion <!-- .element: class="fragment" data-fragment-index="2" -->
* Residual data artifacs may reside on storage media till overwritten <!-- .element: class="fragment" data-fragment-index="3" -->
* CephFS: <!-- .element: class="fragment" data-fragment-index="4" -->
  * File marked as deleted in MDS <!-- .element: class="fragment" data-fragment-index="5" -->
  * Rados objects delayed lazily <!-- .element: class="fragment" data-fragment-index="5" -->
* Keep in mind: <!-- .element: class="fragment" data-fragment-index="6" -->
  * Snaphots may still hold data <!-- .element: class="fragment" data-fragment-index="7" -->
  * Client side encryption of data protects if key destroyed <!-- .element: class="fragment" data-fragment-index="7" -->

