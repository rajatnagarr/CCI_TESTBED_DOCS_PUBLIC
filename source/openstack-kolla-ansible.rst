Meta Information
================

This tutorial is with OpenStack Yoga along with Ubuntu 20.04.

MAAS Installation
=================

`Install MAAS <https://docs.openstack.org/project-deploy-guide/charm-deployment-guide/yoga/install-maas.html>`_

The reason we’re installing MAAS is because we need to control the machines remotely. MAAS allows IPMI control over the servers (power on/off) along with installing Ubuntu OS remotely while also setting up public keys which will ensure that we can ssh into the machines without much of a hassle.

I’m skipping over this for now since it’s very straightforward. Below are the notes that Adam created when he deployed MAAS. It should be the same. You can also follow the OpenStack tutorial mentioned above:

`Adam’s MAAS Installation Notes <https://www.notion.so/Adam-s-MAAS-Installation-Notes-6476de00fff14ba88c124daeb6546e10?pvs=21>`_

It should be noted that ideally, we would want to implement OpenStack’s own BMaaS to manage the IPMI control. But, I felt that it was useful to have backend control of the machine outside of the OpenStack environment. But, moving forward, I think we can work on deploying this.

Ansible Installation
====================

Ansible’s deployment node will be on the same node as where MAAS is deployed.

- Update the package index as below along with installing all the dependent packages:

    .. code-block:: bash

        sudo apt update
        sudo apt install python3-dev libffi-dev gcc libssl-dev python3-venv

- Enter the virtual python environment. This is done so that you can avoid conflicting packages with the host packages and ansible will work correctly.

    .. code-block:: bash

        python3 -m venv /home/ccistack/venv
        source /home/ccistack/venv/bin/activate

- Install pip and ansible in succession. Since we are using a virtual environment, we don’t need to use sudo.

    .. code-block:: bash

        pip install -U pip
        pip install 'ansible>=4,<6'

    You need to make sure that the version of ansible installed is under 6 since kolla-ansible doesn’t support the later versions of ansible yet as of October 13, 2022.

- Install kolla-ansible with its dependencies using pip in development mode. This means that you need to install kolla-ansible from source. You need to do this because you need to modify the neutron configuration so that you can setup the ONOS router for this.

    .. code-block:: bash

        git clone --branch stable/yoga https://opendev.org/openstack/kolla-ansible

- Install the kolla-ansible local git:

    .. code-block:: bash

        pip install ./kolla-ansible

    You can make changes within this repo later on when you have to deploy ONOS.

- Create a kolla directory in ``/etc/kolla`` and move the configuration files over there:

    .. code-block:: bash

        sudo mkdir -p /etc/kolla
        sudo chown $USER:$USER /etc/kolla
        sudo cp -r ~/kolla-ansible/kolla-ansible/etc/kolla/* /etc/kolla
        sudo cp ~/kolla-ansible/kolla-ansible/ansible/inventory/* /etc/kolla

- Install all the Ansible Galaxy dependencies which are required from the Yoga release onward:

    .. code-block:: bash

        kolla-ansible install-deps

- Generate the ``ansible.cfg`` script using the command below. This will contain all the configurations by default.

    .. code-block:: bash

        ansible-config init --disabled -t all > ansible.cfg

- Edit the ``ansible.cfg`` file as per the following below (just enable them in the config):

    .. code-block:: bash

        [defaults]
        host_key_checking=False
        pipelining=True
        forks=100

    These configurations are just related to checking the ansible configuration - not related to OpenStack. So don’t worry too much about other tuning parameters unless you’re looking to speed things up.

Setting up the multi-node configuration
=======================================

- Setup the SSH key pairs across the nodes. To do this, you need to create public/private key pairs on the hosts and share the public key between the two.
    - Public Key of the Controller Node:

        .. code-block:: bash

            ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDmD2kc87f7vVB8R+LWFOVSFP8BoYjoqTXgiwl/NSU2s7SaV2/lvt5hqS6wbfRAY17N3sNow17qF40gIPKPySp0SrgODAbOtjvDxAvND6vfXJGMgEoGftUd9y5Y965ZDZqssESiZoc597UhLvIv9EWF8xg5drc4rx9Zwploi3cmjRxCYaIT9D2nYuFxsmE3mCrt2oMZWHdmIX3H0rRv4IkcJJkUyaVJoryTONI5twHvXrWsy1s3fEECcHfbipPwSPB1xILF735Z0vvIkKllmFKTM3Rc2iBpkDeBKKqACqcnOPomSU6AzE7goLm2/s4jdsdmcolUn+wdZ1BKTDki0WLZMLzS6yPOaXyLIlAPO0pMVhb5BJ3trsFjCgQBkVQ5fIgsi0hrGjAcUv85hwaPCE1RLs8jKMG4JpH0kPm5nnnd0N+GgE1wm+Bny0tZy8tcMCh1EAzS+aj+yblSCxM9qQlO9/AcP5nLKBaCXYn9s/kcYWjYSpeldVFYVJCqA2iUBi8= ubuntu@node-0

    - Public Key of the Compute Node:

        .. code-block:: bash

            ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC8SwfB8WQ/qZPLJ6o7uE6477aI5+NrXdiYIPH+T2745SDtAlKvjEhvlOIWPzlte92Ez7FKxbsfq6QaiDTsbHDFOT+z6cnW1W9DfPXiUPvlxax1vYybZSWGi0MKDResO0z6tXmf80Q2e9X7uR1PJUGkLKodwaYTvp+GYOfxDQe3aLQ2FrdVvwysuFtmjHpNL32zdkEo4qmy74ZNywXpTeaA07gRhNcwFkGypYl88HQ5/1C/vmhFq7G81OC0w5DWkYE4tqx6SPBrJXPM1LN6jotmwNEbnvHhhK2XRRjpk0I/friDjV+ID5oNJaw760lOuwOEPezUMA2YBt4+Jl2NzzSEAyu7n7PGyA+ZY2Uxgzw60thETELSWv0zUNDjXxeOCQXxtjFfc0oIOjburdZx8wIeIe6sDoWbF4KV4Fyy93M3e8CmexdrZ1r4UAegeFC/EmUUoZddaLRPyQWnGTAw2HZa4DCpLLKs7yjSfuOYZr/E5lueyaNYsK1hRBpdMcxLGg8= ubuntu@node-2

    Install the public keys by putting these public keys in the ``~/.ssh/authorized_keys`` folder of each node.

    After this, restart the ssh daemon sessions using the following command:

    .. code-block:: bash

        sudo systemctl restart sshd.service

- Setup the Ethernet ports so that you can setup the data and management network. It should be noted that the data network connects only between the nodes and the management network also connects to the internet.

    .. code-block:: bash

        sudo vi /etc/netplan/50-cloud-init.yaml

- Sample Network Configuration:

    .. code-block:: bash

        network:
            ethernets:
                eno1:
                    addresses:
                    - 10.0.0.27/24
                    gateway4: 10.0.0.1
                    match:
                        macaddress: 0c:42:a1:e1:f9:38
                    mtu: 1500
                    nameservers:
                        addresses:
                        - 10.0.0.100
                        - 10.0.0.1
                        search:
                        - maas
                    set-name: eno1
                eno2:
                    match:
                        macaddress: 0c:42:a1:e1:f9:39
