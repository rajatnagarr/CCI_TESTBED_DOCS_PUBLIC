.. _network_architecture:


CCIxG Testbed Network Architecture
=========================================

This provides a detailed description of the network infrastructure setup, including requirements, components, and the flow of information between them.



Infrastructure Diagram
-----------------------

.. figure:: _static/Infrastructure-diag.png
  :alt: CBRS Hardware
  :align: center
  :width: 1150px
  :height: 700px

|

Requirements
-------------------

- Internet connectivity for the local network.
- Routing and traffic management between the internet and internal network
- Central switching for connecting various network components
- Public hosting server for running services and applications
- OpenStack environment for virtualization and resource management
- Scalable and flexible infrastructure for running and managing virtual machines, storage, and networking resources


Components - Internet Cloud 
-----------------------------------

- Represents the global internet
- Connects to the local network through the Cisco Router

Cisco Router (10.0.0.1)
-------------------------------

- Acts as a gateway between the internet and the internal network
- Manages traffic flow between the two networks

Backhaul Switch (10.0.0.x) 
--------------------------------

- Central switching component for connecting various network elements
- Routes traffic between the Public Hosting Server and the OpenStack environment

Public Hosting Server (internal IP: 10.0.0.4)
----------------------------------------------------

- Hosts various services and applications

|

Components
----------------

- MAAS (10.0.0.12): Metal as a Service for provisioning and managing physical servers
- Gitlab (10.0.0.xx): Web-based Git repository manager for version control and collaboration
- Docs (38.68.231.174 and 38.68.231.xxx): Documentation servers or content management system
- Gateway (172.167.0.10): Server acting as a gateway for specific services or applications
- Redmine (10.0.0.12): Project management and issue tracking tool
- CAM (38.68.231.179): Content Addressable Memory or custom application
- Ansible (10.0.0.6): Configuration management and automation tool



OpenStack Environment
----------------------------

- Provides a scalable and flexible infrastructure for running and managing virtual machines, storage, and networking resources

|

Components:
------------------

- OpenStack Controller (10.0.0.143): Central management component for orchestrating and managing OpenStack services
- OpenStack Storage Server (10.0.0.139): Provides storage services (e.g., block storage, object storage)
- OpenStack Compute Nodes (10.0.0.202, 10.0.0.201, 10.0.0.205): Run virtual machines and provide computing resources
- OpenStack Radio Nodes (10.0.0.200, 10.0.0.203): Manage software-defined radio or wireless communication




Flow of Information
--------------------------

- Internet traffic enters the network through the Internet Cloud and is routed by the Cisco Router to the internal network.
- The Cisco Router forwards the traffic to the Backhaul Switch, which acts as a central distribution point.
- The Backhaul Switch routes traffic between the Public Hosting Server and the OpenStack environment based on the destination IP addresses.
- The Public Hosting Server receives incoming traffic for its hosted services and applications, processes the requests, and sends responses back through the Backhaul Switch and Cisco Router to the internet.

OpenStack components communicate with each other through the Backhaul Switch:
-----------------------------------------------------------------------------------------------
- The OpenStack Controller manages and orchestrates the other OpenStack services.
- OpenStack Compute Nodes receive instructions from the Controller to create, manage, and terminate virtual machines.
- OpenStack Storage Server provides storage resources to the virtual machines and other services.
- OpenStack Radio Nodes handle software-defined radio or wireless communication within the OpenStack environment.




Conclusion
----------------

This technical document provides an overview of the network infrastructure setup, detailing the requirements, components, and flow of information. The setup is designed to provide a scalable, flexible, and efficient environment for hosting services, managing resources, and enabling communication between various components. By understanding the roles and interactions of each element, administrators can effectively maintain and troubleshoot the network infrastructure.


