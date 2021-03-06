High Performance Tuning
=======================

Ubuntu Server
-------------

For best performance, we recommend starting with Ubuntu Server (no GUI) and adding our Security Onion packages as described in our `<Production Deployment>`_ guide.

Disable GUI
-----------

If you're unable to start with Ubuntu Server (no GUI) as recommended above, you can `disable the GUI <Desktop>`_ after the system is installed.

Best Practices
--------------

When you run Setup, make sure you choose `Best Practices <Best-Practices>`__.

Disable Unnecessary Services
----------------------------

Disable any other unnecessary services.  For example, to disable bluetooth:

::

    sudo systemctl stop bluetooth.service
    sudo systemctl disable bluetooth.service
    
CPU Affinity/Pinning
--------------------

For best performance, CPU intensive processes like Zeek, Suricata, and Snort should be pinned to specific CPUs.  In most cases, you'll want to pin sniffing processes to the same CPU that your sniffing NIC is bound to.

`Snort Performance <snort.html#performance>`__

`Suricata Performance <suricata.html#performance>`_

`Zeek Performance <zeek.html#performance>`_

RSS
---

| Check your sniffing interfaces to see if they have Receive Side Scaling (RSS) queues. If so, you may need to reduce to 1:
| https://suricata.readthedocs.io/en/latest/performance/packet-capture.html#rss

Disk/Memory
-----------

If you have plenty of RAM, disable swap altogether.

| Use ``hdparm`` to gather drive statistics and alter settings, as described here:
| http://www.linux-magazine.com/Online/Features/Tune-Your-Hard-Disk-with-hdparm

``vm.dirty_ratio`` is the maximum amount of system memory that can be filled with dirty pages before everything must get committed to disk.

``vm.dirty_background_ratio`` is the percentage of system memory that can be filled with “dirty” pages, or memory pages that still need to be written to disk -- before the pdflush/flush/kdmflush background processes kick in to write it to disk.

| More information:
| https://lonesysadmin.net/2013/12/22/better-linux-disk-caching-performance-vm-dirty_ratio/

Elastic
-------
You will want to make sure that each part of the pipeline is operating at maximum efficiency.  Depending on your configuration, this may include `syslog-ng <syslog>`__, `Logstash <logstash>`_, `Redis <redis>`__, and `Elasticsearch <elasticsearch>`__.  For really high volume logs, you may want to consider the `LOGSTASH_MINIMAL <logstash#logstash-minimal>`__ option.

Other
-----

| Consider adopting some of the suggestions from here:
| https://suricata.readthedocs.io/en/latest/performance/packet-capture.html
| https://github.com/pevma/SEPTun
| https://github.com/pevma/SEPTun-Mark-II
