Sensor Stops Seeing Traffic
===========================

If you want an alert when your sensor stops seeing traffic, there are a few options:

Wazuh
-----

Wazuh checks your sniffing interfaces every 10 minutes. If no packets have been received within that 10 minute window, then Wazuh will generate an alert. This alert can be found in Sguil, Squert, and Kibana. If you'd like Wazuh to email you, then configure it for email as shown in the `Email <Email>`__ section.

Zeek
----

Zeek will automatically email you when it stops seeing traffic on an interface. All you have to do is configure Zeek per the `Email <Email>`__ section.
