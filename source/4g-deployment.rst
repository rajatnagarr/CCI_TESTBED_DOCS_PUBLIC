.. _4g-deployment-experiment:

4G Deployment Experiment
=========================

Introduction
------------

This document provides a step-by-step guide on how to set up and conduct a 4G deployment experiment using the srsRAN 4G suite and USRP hardware.

Prerequisites
-------------

Before starting the experiment, ensure that you have the following:

- UHD (USRP Hardware Driver) installed and set up
.. note::

   We can use this as a reference: :ref:`UHD Installation Guide <installation-script-documentation>`
- USRP hardware with a known IP address
- Two machines: one for the srsRAN 4G ePC and eNB, and another for the srsRAN UE

Setting up UHD
--------------

Verify the UHD installation by running `uhd_find_devices` with the address of your USRP. The last octet of the USRP IP will always be `.2`, regardless of the OpenStack network configuration.

Installing srsRAN 4G Suite
--------------------------

Install the srsRAN 4G suite on both the ePC/eNB machine and the UE machine:

.. code-block:: bash

   cd
   git clone https://github.com/srsRAN/srsRAN_4G.git
   cd srsRAN_4G
   mkdir build
   cd build
   cmake ../
   make

.. note::

   If you encounter the following error during the installation:

   .. code-block:: text

      <error message>

   To resolve this issue, follow these steps:

   .. code-block:: bash

      cd
      sudo apt install gcc-10 g++-10
      cd srsRAN_4G/build
      rm -f CMakeCache.txt
      export CC=$(which gcc-10)
      export CXX=$(which g++-10)
      cmake ../ -B build
      cmake --build build -j$(nproc)
      cmake ../
      make
      make test
      sudo make install
      sudo ldconfig

Configuring srsRAN UE
---------------------

- On the UE machine, edit the configuration file located at `/root/.config/srsran/ue.conf` after running the `srsran_install_configs.sh` script. You need to be the root user to access this file.
- Modify the configuration file according to your setup, such as the USRP address, `dl_earfcn`, etc.
- Run the following memory commands:

.. code-block:: bash

   sudo sysctl -w net.core.rmem_max=24862979
   sudo sysctl -w net.core.wmem_max=24862979

Configuring srsRAN eNB
----------------------

- On the ePC/eNB machine, install srsRAN eNB by following the instructions in the `srsRAN 4G documentation <https://docs.srsran.com/projects/4g/en/latest/usermanuals/source/srsenb/source/2_enb_getstarted.html>`_.
- Modify the eNB configuration file according to your setup.

Running the Experiment
======================

- On the ePC/eNB machine, start the srsRAN ePC:

.. code-block:: bash

   screen -S epc
   sudo srsepc

Detach from the screen by pressing `Ctrl+A` followed by `d`.

- On the same machine, start the srsRAN eNB:

.. code-block:: bash

   screen -S enb
   sudo srsenb

Press `t` and then `Enter` to enable tracing and view the UE attach and throughput information.

- On the UE machine, start the srsRAN UE:

.. code-block:: bash

   screen -S ue
   sudo srsue

Wait for the UE to attach and obtain an IP address (e.g., 172.16.0.X).

Generating Traffic with iPerf
-----------------------------

- On the eNB machine, install iPerf:

.. code-block:: bash

   sudo apt install iperf

- Start the iPerf server:

.. code-block:: bash

   screen -S iperf
   iperf -s

- On the UE machine, install screen and iPerf:

.. code-block:: bash

   sudo apt install screen iperf

- Start the iPerf client:

.. code-block:: bash

   screen -S iperf
   iperf -c 172.16.0.1 -i1 -t60 -u -b 40M

Note: The IP address `172.16.0.1` is used because the first address is always reserved for the core. Observe the data transfer on the eNB machine's iPerf screen.

Troubleshooting
---------------

- If the UE fails to attach, ensure that the eNB is configured correctly and running.
- Double-check the configuration files for the eNB and UE to ensure that the settings match your setup.
- Verify that the USRP hardware is properly connected and recognized by the system.
- If you encounter any errors or issues, refer to the srsRAN 4G documentation or seek assistance from the srsRAN community.

References
----------

- srsRAN 4G Documentation: https://docs.srsran.com/projects/4g/en/latest/index.html
- srsRAN GitHub Repository: https://github.com/srsRAN/srsRAN_4G
- USRP Hardware Driver (UHD) Documentation: https://files.ettus.com/manual/
```

This document follows the reStructuredText format and is ready to be used in a Sphinx documentation project.