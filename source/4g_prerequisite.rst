.. _installation-script-documentation:


Installation Script Documentation
=================================

This document explains the purpose and functionality of each command in the installation script.

Update and Upgrade System
-------------------------

.. code-block:: bash

   sudo apt update && sudo apt upgrade -y

These commands ensure that the system is up-to-date by updating the package lists and upgrading installed packages to their latest versions.

Install MongoDB and Prerequisites
---------------------------------

.. code-block:: bash

   sudo apt install -y gnupg mongodb

This command installs MongoDB, a NoSQL database, and its prerequisites. The ``-y`` flag automatically answers "yes" to prompts during the installation.

Install Open5GS Dependencies
----------------------------

.. code-block:: bash

   sudo apt install -y python3-pip python3-setuptools python3-wheel ninja-build build-essential flex bison git cmake libsctp-dev libgnutls28-dev libgcrypt-dev libssl-dev libidn11-dev libmongoc-dev libbson-dev libyaml-dev libnghttp2-dev libmicrohttpd-dev libcurl4-gnutls-dev libnghttp2-dev libtins-dev libtalloc-dev meson libtool libdw-dev binutils-dev libdwarf-dev doxygen libmbedtls-dev libfftw3-dev libgtest-dev libyaml-cpp-dev libsctp-dev libboost-program-options-dev libconfig++-dev ca-certificates curl

This command installs the necessary dependencies for Open5GS, an open-source 5G core network implementation. It includes various libraries and development tools required for building and running Open5GS.

.. _uhd-installation:

Install UHD Dependencies
------------------------

.. code-block:: bash

   sudo apt install -y cmake git libboost-all-dev libusb-1.0-0-dev libudev-dev libncurses5-dev libuhd-dev uhd-host

This command installs the dependencies for UHD (USRP Hardware Driver), which is required for interfacing with USRP software-defined radio devices.

.. note::
   For detailed instructions on installing and configuring UHD, please refer to the :ref:`UHD Installation Guide <uhd-installation-guide>`.

Configure UHD
^^^^^^^^^^^^^

After installing UHD, you need to configure it to work with your USRP device. Here are the steps to configure UHD:

1. Connect your USRP device to your system using a USB or Ethernet cable.

2. Run the following command to list the available USRP devices:

   .. code-block:: bash

      uhd_find_devices

   This command will display information about the connected USRP devices, including their IP addresses.

3. If your USRP device is not automatically detected, you may need to specify the device address manually using the ``uhd_usrp_probe`` command:

   .. code-block:: bash

      uhd_usrp_probe --args="addr=<USRP_IP_ADDRESS>"

   Replace ``<USRP_IP_ADDRESS>`` with the IP address of your USRP device.

4. Once UHD is configured and able to detect your USRP device, you can proceed with using UHD-based applications and libraries, such as srsRAN, to interact with the device.

For more information on configuring UHD and troubleshooting device detection, refer to the UHD documentation.

Install srsRAN Dependencies
---------------------------

.. code-block:: bash

   sudo apt-get install -y cmake make gcc g++ pkg-config libfftw3-dev libmbedtls-dev libsctp-dev libyaml-cpp-dev libgtest-dev

This command installs the dependencies for srsRAN, an open-source 4G/5G software radio suite. It includes build tools, libraries, and development files necessary for compiling and running srsRAN.

Install Missing Libraries for srsRAN
------------------------------------

.. code-block:: bash

   sudo apt-get install -y libyaml-cpp-dev libdw-dev binutils-dev libdwarf-dev libelf-dev

This command installs additional missing libraries specifically required by srsRAN. These libraries are needed for proper functionality and compilation of srsRAN.

Install iPerf3
--------------

.. code-block:: bash

   sudo apt -y install iperf3

This command installs iPerf3, a network testing tool used for measuring network bandwidth and performance.