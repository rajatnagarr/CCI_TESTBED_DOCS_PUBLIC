Adding a Cloud-Config Script to OpenStack Server(VM) Creation
==============================================================

When creating an OpenStack server instance, you can provide a cloud-config script to customize the instance's configuration during the initialization process. This allows you to automate tasks such as setting passwords, configuring SSH access, and more.

To add a cloud-config script to your OpenStack server creation command, follow these steps:

1. Create a Cloud-Config File
-----------------------------

First, create a file named ``cloud-config.yml`` (or any other desired name) in the same directory where you will run the OpenStack server creation command. Add your cloud-config script to the file using the YAML format. Here's an example cloud-config script that sets a password, disables password expiration, and enables SSH password authentication:



.. code-block:: yaml

   #cloud-config

   password: <password>
   chpasswd:
     expire: False
   ssh_pwauth: True

.. note::
   Replace ``<password>`` with the desired password for the instance.
   Make sure to create the ``cloud-config.yml`` file in the same directory where you will run the OpenStack server creation command. Alternatively, you can provide the appropriate path to the file in the command.

The YAML file structure for the cloud-config script is as follows:

.. code-block:: yaml

   #cloud-config

   key1: value1
   key2:
     subkey1: value2
     subkey2: value3
   key3: value4

In this structure, ``#cloud-config`` is a special comment that indicates the start of the cloud-config script. The rest of the file contains key-value pairs and nested mappings that define the desired configurations.

2. Modify the OpenStack Server Creation Command
-----------------------------------------------

Next, modify your OpenStack server creation command to include the ``--user-data`` flag followed by the path to your ``cloud-config.yml`` file. Here's an example command:

.. code-block:: bash

   openstack --insecure server create --flavor 8cpu-8ram-32disk --image Ubuntu-20.04-ServerImage --nic port-id=`openstack --insecure port list | grep USRP-121 | awk '{print $2}'` --nic net-id=ff409397-4e45-4af9-afbe-00a979369aea --user-data cloud-config.yml --availability-zone radio USRP-121-UE

Output:
-------

.. figure:: _static/121_output.png
  :alt: CBRS Hardware
  :align: center
  :width: 1150px
  :height: 700px

Make sure to replace ``USRP-120`` and ``ff409397-4e45-4af9-afbe-00a979369aea`` with the appropriate values for your environment.

3. Run the Modified Command
---------------------------

Execute the modified OpenStack server creation command. OpenStack will pass the cloud-config script to the instance during the creation process.

The cloud-config script will be applied during the instance's initialization, and the specified configurations will take effect. In this example, the password will be set to "coolpass", password expiration will be disabled, and SSH password authentication will be enabled.

By leveraging cloud-config scripts, you can automate and customize the configuration of your OpenStack server instances, saving time and ensuring consistent setups across multiple instances.


Finding USRP Devices with uhd_find_devices
==========================================

The `uhd_find_devices` command is a utility provided by the USRP Hardware Driver (UHD) software suite. It is used to discover and display information about connected USRP devices.

Running `uhd_find_devices`
---------------------------

To find the specific IP address for your USRP device, run the following command in the terminal:

.. code-block:: bash

  uhd_find_devices

Sample Output
-------------

Here's an example output of running `uhd_find_devices`:

.. figure:: _static/find_devices.png
  :alt: CBRS Hardware
  :align: center


.. code-block:: text

  ubuntu@usrp-120-gnb:~$ uhd_find_devices
  [INFO] [UHD] linux; GNU C++ version 9.2.1 20200304; Boost_107100; UHD_3.15.0.0-2build6
  -- UHD Device 0
  -------------------------------
  Device Address:
      serial: 320D123
      addr: 192.168.107.2
      addr: 192.168.108.2
      addr: 192.168.109.2
      addr: 192.168.110.2
      addr: 192.168.111.2
      addr: 192.168.112.2
      addr: 192.168.121.2
      addr: 192.168.124.2
      addr: 192.168.131.2
      addr: 192.168.132.2
      addr: 192.168.133.2
      addr: 192.168.134.2
      addr: 192.168.135.2
      addr: 192.168.136.2
      addr: 192.168.143.2
      addr: 192.168.144.2
      addr: 192.168.145.2
      addr: 192.168.146.2
      addr: 192.168.156.2
      addr: 192.168.157.2
      addr: 192.168.158.2
      addr: 192.168.159.2
      addr: 192.168.160.2
  name:
  type: x300

  -- UHD Device 1
  -------------------------------
  Device Address:
      serial: 320EC17
      addr: 192.168.120.2
  fpga: HG
  name:
  product: X310
  name: X300

Interpreting the Output
-----------------------

In this example, the `uhd_find_devices` command discovers one UHD device, which is the associated USRP with IP address 192.168.120.2.

The output provides the following information about the USRP device:
- Device Address: The serial number and IP address(es) associated with the device.
- FPGA: The FPGA image loaded on the device (e.g., HG for a high-performance image).
- Product: The specific USRP model (e.g., X310).
- Name: The name of the USRP device (e.g., X300).

.. note::
  In most cases, the USRP IP address will have `.2` at the end, indicating the default IP address assigned to the device.


Testing srsEPC and Deploying srsUE
==================================

After completing the 4G installation process using CMake and other necessary steps, you can proceed with testing the srsEPC (srsRAN EPC) and deploying the srsUE (srsRAN User Equipment) on another virtual machine (VM).

Installing srsEPC
-----------------

To install srsEPC, follow these steps:

1. Run the following command to install the built files:

   .. code-block:: bash

      sudo make install

2. Run the following command to install the configuration files:

   .. code-block:: bash

      sudo srsran_install_configs.sh user

Testing srsEPC
--------------

Once the installation is complete, you can test the srsEPC by running the following command:

.. code-block:: bash

   sudo srsepc

If srsEPC starts without any errors, it indicates that the installation and configuration are successful.

Deploying srsUE on Another VM
-----------------------------

Since srsEPC is working correctly, you can now move on to deploying the srsUE on another virtual machine. The process for deploying the VM with USRP access is the same as before.

.. note::
   Please refer to the previous screenshots and instructions for deploying the VM with USRP access to ensure a clear understanding of the process.

Follow these steps to deploy the srsUE on the new VM:

1. Create a new virtual machine with the necessary specifications and resources.

2. Configure the VM to have access to the USRP device.

3. Install the required dependencies and libraries for srsUE on the new VM.

4. Build and install srsUE using the same CMake process as used for srsEPC.

5. Configure the srsUE with the appropriate settings and parameters.

6. Test the srsUE by running the necessary commands and verifying its functionality.

.. note::
   Make sure to refer to the srsRAN documentation and guides for detailed instructions on building, installing, and configuring srsUE on the new VM.

Network Configuration Changes using Netplan
===========================================
The file tree for the `/etc/netplan/` directory is as follows:

.. code-block:: text

   /etc/netplan/
   ├── 50-cloud-init.yaml

The provided images showcase the modifications made to the network configuration files using Netplan, a network configuration tool in Ubuntu.

50-cloud-init.yaml (Before Changes)
-----------------------------------

In the second image, the modified ``50-cloud-init.yaml`` file is shown with the following changes:


.. figure:: _static/after_edit.png
  :alt: CBRS Hardware
  :align: center
  :width: 1150px
  :height: 700px

.. code-block:: yaml

   network:
     version: 2
     ethernets:
       ens3:
         dhcp4: true
         match:
           macaddress: fa:16:3e:9f:4B:85
         set-name: ens3
       ens5:
         addresses:
           - 192.168.121.6/24
         mtu: 9000
         #dhcp4: true
         #match:
         #macaddress: fa:16:3e:3f:ff:75
         #set-name: ens5

The changes made to the configuration are as follows:

1. ``ens3``:
   - The MAC address has been updated to ``fa:16:3e:9f:4B:85``.
   - The interface continues to use DHCP to obtain an IP address.

2. ``ens5``:
   - The ``dhcp4`` parameter has been commented out, indicating that DHCP is disabled for this interface.
   - The ``match`` and ``macaddress`` parameters have been commented out, suggesting that the MAC address matching is not being used for ``ens5``.
   - The ``addresses`` parameter has been added, assigning a static IP address ``192.168.121.6`` with a subnet mask of ``/24`` (255.255.255.0) to ``ens5``.
   - The ``mtu`` (Maximum Transmission Unit) parameter has been set to ``9000``, indicating a larger packet size for ``ens5``. This allows for improved network performance by enabling jumbo frames.

50-cloud-init.yaml (After Changes)
-----------------------------------

In the first image, the ``50-cloud-init.yaml`` file is displayed, which is a network configuration file generated by cloud-init. The file contains the following configuration:

.. figure:: _static/orignal_yaml_file.png
  :alt: CBRS Hardware
  :align: center
  :width: 1150px
  :height: 700px

.. code-block:: yaml

   network:
     version: 2
     ethernets:
       ens3:
         dhcp4: true
         match:
           macaddress: fa:16:3e:50:9c:c1
         set-name: ens3
       ens5:
         dhcp4: true
         match:
           macaddress: fa:16:3e:76:4c:11
         set-name: ens5

This configuration defines two network interfaces:

1. ``ens3``:
   - Configured to obtain an IP address via DHCP (Dynamic Host Configuration Protocol).
   - The ``match`` section specifies the MAC address ``fa:16:3e:50:9c:c1`` to identify the interface.
   - The ``set-name`` parameter sets the interface name to ``ens3``.

2. ``ens5``:
   - Configured to obtain an IP address via DHCP.
   - The ``match`` section specifies the MAC address ``fa:16:3e:76:4c:11`` to identify the interface.
   - The ``set-name`` parameter sets the interface name to ``ens5``.

Explanation of Changes
----------------------

The modifications in the ``50-cloud-init.yaml`` file alter the network settings for the ``ens3`` and ``ens5`` interfaces:

- ``ens3`` continues to use DHCP for IP address assignment, but the MAC address has been updated to ``fa:16:3e:9f:4B:85``. This change ensures that the correct physical interface is identified based on its MAC address.

- ``ens5`` has been reconfigured to use a static IP address instead of DHCP. The ``addresses`` parameter assigns the IP address ``192.168.121.6`` with a subnet mask of ``/24``. This means that ``ens5`` will always have the specified IP address, providing a consistent and predictable network configuration.

- The ``mtu`` parameter for ``ens5`` has been set to ``9000``, enabling jumbo frames. Jumbo frames allow for larger packet sizes, reducing overhead and improving network efficiency. However, it's important to ensure that all devices on the network support and are configured for jumbo frames.

By modifying the Netplan configuration file, you can customize the network settings according to your specific requirements. This includes assigning static IP addresses, configuring subnet masks, enabling or disabling DHCP, and adjusting MTU sizes for optimal network performance.

It's crucial to carefully review and test the network configuration changes before applying them to avoid any network connectivity issues or conflicts.


Network Configuration and Testing with Netplan and srsRAN
=========================================================

This document outlines the steps involved in configuring the network using Netplan and testing the srsRAN software suite, specifically the srsEPC (Evolved Packet Core) and srsUE (User Equipment), in an Ubuntu environment.

Netplan Configuration
---------------------

The network configuration was modified using Netplan, a powerful network configuration tool in Ubuntu. The changes were made to the ``50-cloud-init.yaml`` file, which is a YAML-formatted configuration file used by cloud-init.

The modifications included:

1. Updating the MAC address for the ``ens3`` interface to ``fa:16:3e:9f:4B:85``.
2. Disabling DHCP and assigning a static IP address ``192.168.121.6/24`` to the ``ens5`` interface.
3. Configuring a larger MTU value of ``9000`` for the ``ens5`` interface to enable jumbo frames.

These changes were made to customize the network settings according to the specific requirements of the system and to optimize network performance.

srsRAN Testing
--------------

After configuring the network, the focus shifted to testing the srsRAN software suite. The srsRAN project provides an open-source implementation of the 4G/5G Radio Access Network (RAN) and Core Network (CN) functionalities.

The testing process involved the following steps:

1. Installing the srsEPC component using the ``sudo make install`` command.
2. Installing the configuration files for srsEPC using the ``sudo srsran_install_configs.sh user`` command.
3. Testing the srsEPC by running the ``sudo srsepc`` command and verifying its functionality.

Upon successful testing of srsEPC, the next step was to deploy the srsUE component on another virtual machine (VM). The process for deploying the VM with USRP (Universal Software Radio Peripheral) access remained the same as before.

Conclusion
----------

The network configuration and testing process demonstrated the power and flexibility of Netplan in managing network settings in an Ubuntu environment. By modifying the ``50-cloud-init.yaml`` file, it was possible to customize the network interfaces, assign static IP addresses, and enable jumbo frames for improved performance.

The successful installation and testing of the srsEPC component of the srsRAN software suite laid the foundation for further exploration and deployment of the srsUE component on a separate virtual machine. The ability to configure and test these components independently allows for a modular and scalable approach to building and experimenting with 4G/5G networks.

Overall, the combination of Netplan for network configuration and srsRAN for radio access and core network functionalities provides a powerful toolset for researchers, developers, and network engineers working in the field of wireless communications. The steps outlined in this document serve as a starting point for further exploration, optimization, and integration of these technologies in various network scenarios.