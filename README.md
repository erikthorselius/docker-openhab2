Overview
========

Docker image for Openhab.

Building
========

```docker build -t <username>/openhab```

Running
=======

* The image exposes Openhab ports 8080, 8443, 5555 and 9001 (supervisord).
* It expects you to make a configurations directory on the host to /opt/openhab/configurations.  This allows you to inject your openhab configuration into the container (see example below).
* To enable specific plugins, add a file with name addons.cfg in the configuration directory which lists all addons you want to add.

Example content for addons.cfg:
```
org.openhab.action.mail-1.5.0.jar
org.openhab.action.squeezebox-1.5.0.jar
org.openhab.action.xmpp-1.5.0.jar
org.openhab.binding.exec-1.5.0.jar
org.openhab.binding.http-1.5.0.jar
org.openhab.binding.knx-1.5.0.jar
org.openhab.binding.mqtt-1.5.0.jar
org.openhab.binding.networkhealth-1.5.0.jar
org.openhab.binding.serial-1.5.0.jar
org.openhab.binding.squeezebox-1.5.0.jar
org.openhab.io.squeezeserver-1.5.0.jar
org.openhab.persistence.cosm-1.5.0.jar
org.openhab.persistence.db4o-1.5.0.jar
org.openhab.persistence.gcal-1.5.0.jar
org.openhab.persistence.rrd4j-1.5.0.jar
```

* The openhab process is managed using supervisord.  You can manage the process (and view logs) by exposing port 9001.
* The container supports starting without network (--net="none"), and adding network interfaces using pipework.
* You can add a timezone file in the configurations directory, which will be placed in /etc/timezone.

Example content for timezone:
```
Europe/Brussels
```

Example run command:
```docker -d -p 8080:8080 -v /tmp/configuration:/opt/openhab/configurations tdeckers/openhab```

