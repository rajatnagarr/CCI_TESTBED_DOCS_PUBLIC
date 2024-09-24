Launching OpenStack Instances
=============================================================

This documentation provides steps to create and launch OpenStack instances with USRP (Universal Software Radio Peripheral) access using the Command-Line Interface (CLI) and generic compute VMs through the OpenStack dashboard.

Keywords: USRP, Instance, OpenStack, CLI, Dashboard, Compute VM, Cloud Computing

.. note::
    - Each USRP can only be connected to one instance at a time.
    - Users cannot create an instance with a USRP network unless granted access by an OpenStack admin.
    - This guide is intended for users on Linux, macOS, and Windows devices.

CLI Instructions for USRP Access
--------------------------------

To create an OpenStack instance with **USRP access** using the Command-Line Interface (CLI), follow the steps below:

1. **Download Your OpenStack RC File**

   - Log in to the OpenStack portal: `Link <https://portal.ccixgtestbed.org/auth/login>`_.
   - Download your profile's RC file from the drop-down in the top-right corner.

   .. image:: _static/rc_file.gif
      :align: center

2. **Install Necessary Dependencies**

   **For Linux/macOS:**

   Ensure Python 3 and the required dependencies are installed by following these steps:

   .. code-block:: bash

       sudo apt update
       sudo apt install -y python3-pip python3-dev
       sudo pip3 install --upgrade pip
       sudo pip3 install python-openstackclient

   **For Windows:**

   Follow these steps to install Python 3 and pip, and then the OpenStack CLI tool:

   - **Install Python 3:**  
     Download and install Python from the `official Python website <https://www.python.org>`_. During installation, ensure to check the box for **"Add Python to PATH"**.

   - **Install pip:**  
     After Python is installed, pip (the Python package installer) should be installed automatically. You can verify this by running the following commands in Command Prompt (CMD):

     .. code-block:: bash

         python --version
         pip --version

   - **Upgrade pip:**  
     To upgrade pip, open Command Prompt (CMD) and run:

     .. code-block:: bash

         python -m pip install --upgrade pip

   - **Install OpenStack Client:**  
     Once pip is upgraded, you can install the OpenStack CLI tool:

     .. code-block:: bash

         pip install python-openstackclient

     After installation, you can use the OpenStack CLI by typing ``openstack`` in Command Prompt or PowerShell.

3. **Source the OpenStack RC File**

   Navigate to the directory where you downloaded the RC file and source it:

   .. code-block:: bash

       . <rc_file_name>.sh

   This command will prompt you to enter your OpenStack password.

    .. image:: _static/rc_file_command_2.png
        :align: center
        :width: 550px

4. **Create an Instance with USRP Access**

   Use the following command to create an instance with USRP access:

   .. code-block:: bash

       openstack server create --flavor <flavor_name> --image <image_name> --nic port-id=$(openstack port list | grep <usrp_number> | awk '{print $2}') --nic net-id=<internal_network_id> --availability-zone radio <instance_name>

   **Note**: Replace ``<flavor_name>``, ``<image_name>``, ``<usrp_number>``, ``<internal_network_id>``, and ``<instance_name>`` with the appropriate values.

   For further details, watch the tutorial video: https://youtu.be/NtC79iuUNNI

Dashboard Instructions for Compute VM Access
--------------------------------------------

To create a **compute VM** using the **OpenStack dashboard**, follow these steps:

1. **Log in to the OpenStack Dashboard**

   - Access the OpenStack portal: `Link <https://portal.ccixgtestbed.org/auth/login>`_.

   .. image:: _static/instance-1.png
        :align: center
        :width: 650px

   - Navigate to the "Launch Instance" screen under the project section.

2. **Configure Instance Settings**

   - Provide a name for the instance.
   - Select ``compute`` as the availability zone (for generic VMs, not ``radio``).
   
   .. image:: _static/instance-2.png
        :align: center
        :width: 650px

3. **Select Boot Source**

   - In the "Source" tab, select the appropriate boot source (e.g., an image or snapshot).
   - Set "Create New Volume" to "Yes" or "No" depending on your requirements.
   - Choose the boot source (e.g., ``Ubuntu-18.04-ServerImage``).

   .. image:: _static/instance-3.png
        :align: center
        :width: 650px

4. **Select Flavor**

   - Choose the flavor according to the VM's resource requirements (vCPUs, RAM, disk size).

   .. image:: _static/instance-4.png
        :align: center
        :width: 650px

5. **Select Network**

   - Choose the appropriate network for your instance.

   .. image:: _static/instance-5.png
        :align: center
        :width: 650px

6. **Configure Security Groups**

   - Select the desired security group(s) for the instance.

   .. image:: _static/instance-6.png
        :align: center
        :width: 650px

7. **Launch the Instance**

   After configuring all settings, click the **Launch Instance** button to provision the instance.

   .. image:: _static/instance-7.png
        :align: center
        :width: 650px

.. note::
    If you encounter any issues with the OpenStack dashboard, login credentials, or network access, raise a ticket in Redmine or contact the administrator at `cci.xg.testbed.admin@cyberinitiative.org`.
