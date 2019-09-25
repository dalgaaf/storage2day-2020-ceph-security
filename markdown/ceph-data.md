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
## Data Distribution

### Replication
<div>
  <center><img data-src="images/replica_explained.svg" style="width:30%"></center>
</div>


<!-- .slide: data-state="normal" id="EC-0.2" data-timing="20s" data-menu-title="Erasure Coding Diagram" -->
## Data Distribution

### Erasure Coding
<div>
  <center><img data-src="images/ec_explained_extra.svg" style="width:65%"></center>
</div>

Note:
- Object is split into *k* chunks
- Additonal *m* coding chunks will be created (encoded)
- chunks/shards will be distributed as defined in crush and erasure code profile


<!-- .slide: data-state="normal" id="data-1" data-timing="20s" data-menu-title="Thread Actors" -->
## Data Integrity

TODO: add scrubbing

<!-- .slide: data-state="normal" id="data-2" data-timing="20s" data-menu-title="General considerations" -->
## Data Deletion

TODO: add info 
