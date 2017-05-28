.. _virtual_machine:

Virtual Machine
===============

We provide a pre-built virtual machine image (OVA) that you can import into most virtualization systems. It has been built using VirtualBox, where you can import the OVA image directly.

.. note::  This VM can be run only on 64-bit systems and is not recommended for use in production environments. Instead it can be a useful tool for proof of concepts and labs. Distributed architectures, and multi-node Elastic Stack clusters are usually a better fit for production environments, where higher performance is required.

1. This virtual appliance, available at https://packages.wazuh.com/vm/wazuh2.0.ova, contains the following components:

    - CentOS 7
    - Wazuh 2.0
    - RESTful API 2.0
    - Elasticsearch 5.3.2
    - Logstash 5.3.2
    - Kibana 5.3.2 port "**5601**""
    - WazuhAPP 2.0_5.3.2

2. Import the OVA in your virtualization platform, and run the virtual machine. The root password is "**wazuh**" and the username/password for the Wazuh API is "**foo/bar**".

  Although you don't need to change any Elastic Stack configuration settings, feel free to explore the options.  You can find Elasticsearch installed in ``/usr/share/elasticsearch``. Similarly, Logstash is installed in ``/usr/share/logstash`` and its config directory is ``/etc/logstash/conf.d/``.

3. **Wazuh Manager** and the **Elastic Stack** are configured to work out of the box. You can now deploy the Wazuh agents, on those systems that you intend to monitor, and connect them to your virtual appliance. More documentation at:

    - `How to install Wazuh agents <installing-wazuh-agent>`_.

  .. warning:: Before connecting any Wazuh agent, change the VM's network interface type from NAT - the factory default - to bridged so that it will be reachable to your network. By default, the VM will try to get an IP address from your network's DHCP server. Alternatively, you can set a static IP address for the VM by configuring the network files on the CentOS operating system this virtual machine is based on.

4. You can start and stop wazuh-manager, elasticsearch, logstash, and kibana with the 'systemctl' command. Examples ::

    systemctl restart wazuh-manager
    systemctl stop elasticsearch
    systemctl start logstash
    systemctl status kibana

5. In order to connect to Kibana web user interface, you can login with http://OVA_IP_ADRESS:5601 (where ``OVA_IP_ADDRESS`` is your system IP).
