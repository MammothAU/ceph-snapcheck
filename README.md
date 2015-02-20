# ceph-snapcheck
ceph-snapcheck is a basic Python script to scan a Ceph OSD file structure for discrepancies between the ceph.snapset attribute and physical snapshot files.

Basic usage to scan an OSD's filestore:

    ceph-snapcheck  /var/lib/ceph/osd/ceph-0/current

You can scan  an individual placement group:

    ceph-snapcheck  /var/lib/ceph/osd/ceph-0/current/3.10_head

You can scan all OSD's with a simple loop:

    for FILESTORE in /var/lib/ceph/osd/*/current ; do ceph-snapcheck $FILESTORE ; done


Percentage progress is written to stderr. If a problem is found with a particular object, the current osdmap along with the detected issue are written to stdout. For example:

```
osdmap e79930 pool 'rbd_ssd' (4) object 'rbd_data.c3571a2ae8944a.000000000000123d' -> pg 4.73284b5b (4.b5b) -> up ([1,29], p1) acting ([1,29], p1)
        /var/lib/ceph/osd/ceph-1/current/4.b5b_head/DIR_B/DIR_5/DIR_B/DIR_4/rbd\udata.c3571a2ae8944a.000000000000123d__head_73284B5B__4 : snaps are on disk but not in attr
['87bf']
```

