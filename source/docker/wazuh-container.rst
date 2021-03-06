.. _wazuh-container:

Wazuh container
===============================

Requirements
-------------

Increase max_map_count on your host (Linux)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You need to increase ``max_map_count`` on your Docker host::

  $ sudo sysctl -w vm.max_map_count=262144

To set this value permanently, update the vm.max_map_count setting in /etc/sysctl.conf. To verify after rebooting, run "sysctl vm.max_map_count".

.. warning::

  If you don't set the **max_map_count** on your host, Elasticsearch will probably don't work.

SELinux
^^^^^^^^^^

On distributions which have SELinux enabled out-of-the-box, you will need to either re-context the files or put SELinux into Permissive mode for docker-elk to start properly. For example, on Red Hat and CentOS the following command will apply the proper context::

  .-root@centos ~
  -$ chcon -R system_u:object_r:admin_home_t:s0 docker-elk/

Usage
-------------------------------

#. Copy the docker-compose file to your system:

    ::

      curl -so docker-compose.yml https://raw.githubusercontent.com/wazuh/wazuh-docker/master/docker-compose.yml

#. Start Wazuh and Elastic Stack using *docker-compose*:

    a) Foreground::

        $ docker-compose up


    b) Background::

        $ docker-compose up -d

    Then access the Kibana UI by hitting `http://localhost:5601 <http://localhost:5601>`_ with a web browser.


By default, the stack exposes the following ports:

+-----------+-----------------------------+
| **1514**  | Wazuh UDP                   |
+-----------+-----------------------------+
| **1515**  | Wazuh TCP                   |
+-----------+-----------------------------+
| **514**   | Wazuh UDP                   |
+-----------+-----------------------------+
| **55000** | Wazuh API                   |
+-----------+-----------------------------+
| **5000**  | Logstash TCP input          |
+-----------+-----------------------------+
| **9200**  | Elasticsearch HTTP          |
+-----------+-----------------------------+
| **9300**  | Elasticsearch TCP transport |
+-----------+-----------------------------+
| **5601**  | Kibana                      |
+-----------+-----------------------------+

.. note:: Configuration is not dynamically reloaded, so you will need to restart the stack after any change in the configuration of a component.
