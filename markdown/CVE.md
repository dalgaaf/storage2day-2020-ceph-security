<!-- .slide: data-state="section-break" id="section-break-6" data-timing="10s" -->
# Ceph CVE's


<!-- .slide: data-state="normal" id="ceph-CVEs-0" data-timing="20s" data-menu-title="CVE-Stats" -->
## Ceph CVE Statistics

<canvas data-chart="bar">
<!--
{
 "data" : {
     "labels": ["2013", "2014", "2015", "2016", "2017", "2018", "2019"],

     "datasets": [
         {
             "data": [1, 3, 5, 6, 3, 8, 1],
             "backgroundColor": [
                 "rgba(166, 206, 227, 0.6)",
                 "rgba(31, 120, 180, 0.6)",
                 "rgba(178, 223, 138, 0.6)",
                 "rgba(51, 160, 44, 0.6)",
                 "rgba(251, 154, 153, 0.6)",
                 "rgba(227, 26, 28, 0.6)",
                 "rgba(253, 191, 111, 0.6)"]
         }
     ]
 },
 "options": {
     "animateScale": "true",
     "responsive": "true",
     "legend": {
           "display": 0
     },
     "plugins": {
         "datalabels": {
             "align": "end",
             "anchor": "end",
             "display": 1
         }
     },
     "scales": {
         "yAxes": [{
             "gridLines": {
                 "color": "rgba(0, 0, 0, 0)"
             },
             "ticks": {
                 "display": 0,
		 "min": 0,
		 "max": 9
             },
             "scaleLabel": {
                 "display": 1,
                 "labelString": "number of CVE's"
             }
         }],
         "xAxes": [{
             "gridLines": {
                 "color": "rgba(0, 0, 0, 0)"
             }
         }]
    }
 }
}
-->
</canvas>


<!-- .slide: data-state="normal" id="ceph-CVEs-0" data-timing="20s" data-menu-title="CVE-2019-3821" -->
## CVE-2019-3821

### Ceph Versions
* mimic

### Issue
* civetweb frontend flaw in handling requests to ceph RGW server with SSL enabled
* unauthenticated attacker could create multiple connections to Radosgw to exhaust file descriptors

### Impact
* remote Denial of Service

Note: cause by imported code


<!-- .slide: data-state="normal" id="ceph-CVEs-1" data-timing="20s" data-menu-title="CVE-2018-7262" -->
## CVE-2018-7262

### Ceph versions
* before 12.2.3
* 13.x till 13.0.1

### Issue
* Radosgw doesn't handle malformed HTTP headers properly

### Impact
* remote Denial of Service


<!-- .slide: data-state="normal" id="ceph-CVEs-2" data-timing="20s" data-menu-title="CVE-2018-14662" -->
## CVE-2018-14662

### Ceph Versions
* before 13.2.4

### Issue
* authenticated users with read-only permissions could steal dm-crypt encryption keys

### Impact
* encryption keys leak


<!-- .slide: data-state="normal" id="ceph-CVEs-3" data-timing="20s" data-menu-title="" -->
## CVE-2018-1128

### Ceph Versions
* mimic
* luminous
* jewel

### Issue
* cephx authentication protocol did not verify ceph clients correctly

### Impact
* replay attack


<!-- .slide: data-state="normal" id="ceph-CVEs-4" data-timing="20s" data-menu-title="" -->
## CVE-2018-1129

### Ceph Versions
* mimic
* luminous
* jewel

### Issue
* signature calculation was handled weakly by cephx authentication protocol

### Impact
* alter payload

Note: solved by introducing CEPHX_V2 in Nautilus
