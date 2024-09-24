.. _ORAN:

ORAN (Open Radio Access Network)
================================

Overview of ORAN
----------------

ORAN (Open Radio Access Network) is an industry-wide initiative aimed at creating more open, intelligent, and programmable mobile networks. Unlike traditional RAN (Radio Access Network) systems, which are often closed and proprietary, ORAN seeks to introduce open interfaces and modular elements, fostering greater innovation and interoperability.

Importance and Benefits
------------------------

- **Interoperability:** Enables equipment from different vendors to work together seamlessly.
- **Flexibility:** Allows operators to customize and optimize their networks.
- **Cost Efficiency:** Reduces costs by leveraging off-the-shelf hardware and software.
- **Innovation:** Encourages new solutions and technologies through open standards.


ORAN Architecture
------------------

ORAN architecture is modular, consisting of several key components that communicate over standardized interfaces. These components include:

- **Radio Unit (RU)**
- **Distributed Unit (DU)**
- **Centralized Unit (CU)**
- **RAN Intelligent Controller (RIC)**

.. figure:: _static/ORANArchitecture.png
  :alt: CBRS Hardware
  :align: center
  :width: 1150px
  :height: 700px

Functional Splits
~~~~~~~~~~~~~~~~~

ORAN defines various functional splits between the components to optimize performance and deployment flexibility. The most common splits are:

- **Split 7-2x:** Between the RU and DU
- **Split 2:** Between the DU and CU

.. figure:: _static/FunctionalSplit.png
  :alt: CBRS Hardware
  :align: center
  :width: 1200px
  :height: 900px

|

Key Components of ORAN
-----------------------

**Radio Unit (RU)**
~~~~~~~~~~~~~~~~~~~
The RU handles the lower-layer functions of the RAN, including the physical layer (PHY) and parts of the RF processing. It interfaces directly with the antennas and is responsible for transmitting and receiving radio signals.

**Distributed Unit (DU)**
~~~~~~~~~~~~~~~~~~~~~~~~~
The DU manages real-time baseband processing and is responsible for the MAC (Medium Access Control) and parts of the PHY layer. It connects to the RU via the front-haul interface.

**Centralized Unit (CU)**
~~~~~~~~~~~~~~~~~~~~~~~~~~
The CU deals with non-real-time processing and higher-layer functions such as the RLC (Radio Link Control) and PDCP (Packet Data Convergence Protocol) layers. It connects to the DU via the mid-haul interface and to the core network via the back-haul interface.

**RAN Intelligent Controller (RIC)**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The RIC provides advanced control and optimization of the RAN. It supports two types of applications:

- **Near-Real-Time RIC (nRT-RIC):** For real-time control within milliseconds.
- **Non-Real-Time RIC (nRT-RIC):** For non-real-time control within seconds to minutes.

.. figure:: _static/ComponentsofORAN.png
  :alt: CBRS Hardware
  :align: center
  :width: 1300px
  :height: 700px

|

**ORAN Interfaces**
---------------------

**Front-haul**
~~~~~~~~~~~~~~

The interface between the RU and DU, typically using the eCPRI (enhanced Common Public Radio Interface) protocol.

**Mid-haul**
~~~~~~~~~~~~~
The interface between the DU and CU, which can use various protocols depending on the functional split implemented.

**Back-haul**
~~~~~~~~~~~~~~
The interface between the CU and the core network, typically using standard IP/Ethernet connections.

**ORAN Software and Hardware**
-------------------------------

Hardware Requirements**
~~~~~~~~~~~~~~~~~~~~~~~
- **Commercial Off-The-Shelf (COTS) Hardware:** Standard servers, switches, and network equipment.
- **Specialized Hardware:** For specific tasks like signal processing and RF transmission.

**Software Stack**
~~~~~~~~~~~~~~~~~~
-- **Network Functions Virtualization (NFV):** Virtualizes network functions to run on COTS hardware.
-- **Cloud-Native Principles:** Utilizes containerization (e.g., Kubernetes) for orchestration and management.
-- **Open APIs:** Ensures interoperability and modularity.


.. figure:: _static/Cloud-NativeORAN.png
  :alt: CBRS Hardware
  :align: center
  :width: 1200px
  :height: 900px

|

**Deployment Models**
----------------------

**Cloud-Native Deployments**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Leverage cloud infrastructure to deploy ORAN components in a scalable and flexible manner, using containers and microservices architecture.

**Edge Deployments**
~~~~~~~~~~~~~~~~~~~~
Deploy ORAN components closer to the end-users to reduce latency and improve performance, often in MEC (Multi-access Edge Computing) environments.

**Use Cases and Applications**
------------------------------
Enhanced Mobile Broadband (eMBB)
Provides high-speed internet access with improved bandwidth and coverage, supporting applications like streaming and virtual reality.

**Massive Machine Type Communications (mMTC)**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Supports a large number of IoT devices, enabling applications like smart cities and industrial automation.

**Ultra-Reliable Low Latency Communications (URLLC)**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Ensures low latency and high reliability for critical applications such as autonomous driving and remote surgery.

**Challenges and Considerations**
---------------------------------

**Interoperability**
~~~~~~~~~~~~~~~~~~~~~
Ensuring seamless integration between components from different vendors can be challenging and requires rigorous testing and standardization.

**Security**
~~~~~~~~~~~~~
As with any open system, ensuring robust security measures to protect against vulnerabilities and threats is crucial.

**Performance Optimization**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Balancing the flexibility and openness of ORAN with the need for high performance and low latency requires careful optimization.

**Future of ORAN**
------------------
ORAN represents a significant shift towards more open, flexible, and intelligent mobile networks. As the technology matures, it is expected to drive further innovation and efficiency in the telecom industry, ultimately benefiting operators and end-users alike.