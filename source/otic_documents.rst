Open Testing and Integration
=============================


The North American OTIC in Washington DC/Arlington VA Metro is aimed at facilitating the design, development, and deployment of cloud-enhanced and open-software-defined wireless technologies. It provides multiple testbeds to support real-world experimentation, testing, and interoperability on advanced wireless technologies and applications for the next generation. The facility is open to various users, including universities, industry research labs, and both US and non-US institutions. Commercial entities are also encouraged to use the facility for product development and evaluation with certain provisions. Researchers can run experiments remotely on the testbed by logging in via remote terminal (VPN and SSH), which provides various facilities for experiment execution, measurements, and data collection across four testbeds (see their location on Figure 1).


.. figure:: _static/otiv.png
  :alt: CBRS Hardware
  :align: center

Commonwealth Cyber Initiative (CCI) xG Testbed
----------------------------------------------


**Overview:** The CCI xG Testbed is part of the Virginia State Commonwealth Cyber Initiative program, focusing on workforce development and O-RAN-based testbed deployment. It allows users to explore cutting-edge technology across various spectrums (e.g., VT CBRS PAL, FCC Experimental and Commission License) in a real-world environment.
**Indoor Testbed:** Located at the Virginia Tech Research Center in the Washington DC area, this testbed features a 32'x29' two-dimensional grid of programmable advanced software-defined radio (SDR) nodes, including X310, X410, N310, B210, and B205-mini. These nodes can be interconnected into specified topologies with reproducible wireless channel models.
**Outdoor Testbed:** An outdoor, campus-scale testbed is deployed at the Virginia Tech main campus in Blacksburg, VA. It includes 3 commercial CBRS base stations, 3 SDR-based CBSD prototype nodes, fiber-optic front-haul and back-haul networks, and edge (Blacksburg location) and core cloud computing infrastructure (Washington DC/Arlington VA).
**Additional Facilities:** The CCI xG Testbed includes other locations such as the CCI – CORNET/CCI SWVA 5G+ indoor testbed and the CCI PORT5+ Lab at Virginia Tech main campus in Blacksburg, VA, the CCI George Mason University (GMU) NextG Lab at Arlington, VA, and the CCI Old Dominion University (ODU) Lab at Coastal VA.


**Testbed Capabilities**
-------------------------
The CCI xG Testbed supports several new classes of wireless experiments not currently available to the research community. This includes end-to-end CBRS experimentation with PAL and GAA users, end-to-end close-loop O-RAN experimentation, and edge-cloud-continuum experiments, utilizing an open-source Spectrum Access System (SAS) developed at Virginia Tech.


Here is the revised document with the provided text and figures integrated:


Physical Layout and Architecture of the Lab(s)
===========================================

The OTIC architecture focuses on ultra-high bandwidth and low latency wireless communication coupled with edge-cloud computing. The main outdoor OTIC facility is located at Stroubles Creek Park, Virginia Tech main campus, Blacksburg, VA. It features advanced SDR nodes, fiber-optic networks, and edge and core cloud computing infrastructure. The indoor facility has numerous processing elements (CPUs and GPUs) near the radios. Core testbed services are deployed on computing clusters at the CCI xG Testbed facility in Washington DC/Arlington VA. Researchers can access the OTIC testbed remotely via VPN, providing various facilities for experiment execution, measurements, and data collection.

.. raw:: html

   <div style="display: flex; justify-content: center;">
     <iframe src="https://www.google.com/maps/d/u/3/embed?mid=1482S18-61pp9zI-bNaLeKO7vpyn9tfY&ehbc=2E312F" width="640" height="480"></iframe>
   </div>


These core services support multiple experimentation domains. As shown in Figure 1, each domain consists of the following components:
- on-boarding (console) and domain support server(s)
- SDR nodes (user devices and radio hardware),
- edge cloud servers ("radio cloud") OpenStack-based
- general-purpose computing cloud servers ("core cloud")
- networking (electrical)

While most devices in each domain are entirely under user control (SDR and VM/Containers) for remote access and experimentation, some domain-level devices (i.e., Amari Callbox, COTS UE) are deployed with restricted user access. Similarly, many services and devices are deployed globally (i.e., MEC) for the entire testbed.

Multiple types of radio nodes are available, depending on the testbed:
- SDR-based base station (indoor ceiling deployed and rooftop deployment in-progress)
- Commercial CBRS base station (rooftop deployment in-progress)

Finally, the core cloud for both domains is located in Arlington: VTRC data center interconnected with the high-speed optical backbone to Blacksburg. It also includes AWS cloud environment for outdoor deployment.

The CCI xG Testbed deployment is built in a bottom-up manner with commodity components, programmable hardware, and open-source software. Three types of hardware components are included: (i) SDR nodes (user devices and radio hardware), (ii) edge cloud servers (radio cloud), and (iii) general-purpose cloud.

.. figure:: _static/lab_space.png
   :alt: Lab Space
   :align: center
   :width: 600px
   :height: 400px

The core of the proposed indoor OTIC facilities is located at the Virginia Tech Research Center in North Virginia (Washington DC area), Arlington, as shown in Figure 4. The ~2000 m² space includes:

- 500 m² housing the CCI xG Testbed radio grid (see Figure 5),
- 45 m² for maintenance workstations and miscellaneous network components (see Figure 6),
- ~6000 sq. feet of laboratory space including the radio ceiling, control room, infrastructure server room, electronics and machine shops/labs, cubicles, and staff offices.

The facility also includes one large conference room seating up to 30 people and two smaller conference rooms seating 6-10 people.



.. figure:: _static/radio_ceiling.jpeg
   :alt: Radio Ceiling
   :align: center

In addition to indoor laboratories, outdoor equipment can be deployed at one of the three locations in Blacksburg: on the roof of the Human and Agricultural Biosciences Building (Figure 7), Hahn Hall North (Figure 8), or the Animal Husbandry Barn (Figure 9).

Industry equipment may be visible to other clients due to the shared nature of the common lab area; however, access is strictly controlled, and operation of the test equipment is limited to authorized personnel. Photography is not allowed in the lab with industry equipment unless permitted and described in the NDA.

Each industry or project is assigned IP addresses from its isolated subnet range, depending on the scale of the project. The office/workroom is equipped with lockers, and a clean desk policy is applied, requiring industry partners to clear their desks of all sensitive documents at the end of the day or when leaving the desk. Confidential documents can be temporarily stored in the lockers.


This document integrates the provided text and figures into the reStructuredText format suitable for Sphinx documentation, including appropriate figure alignments and alt text for accessibility. Adjustments can be made based on specific formatting or content requirements.

**Location of the OTIC Facility**
-----------------------------------


**Human and Agricultural Biosciences Building**
-----------------------------------------------
.. figure:: _static/bio_science_buiding.jpeg
  :alt: CBRS Hardware
  :align: left
  :width: 400px
  :height: 300px

.. figure:: _static/human_and_agriculture_bioscience_building.png
  :alt: CBRS Hardware
  :align: left
  :width: 400px
  :height: 300px

|
|
|

|
|
|

|
|
|

|
|
|
**Hahn Hall North Rooftop**
----------------------------

.. figure:: _static/hahn_hall_north_hall_2.png
  :alt: CBRS Hardware
  :align: left
  :width: 400px
  :height: 300px

.. figure:: _static/hahn_hall_north_rooftop.jpeg
  :alt: CBRS Hardware
  :align: left
  :width: 400px
  :height: 300px
|
|
|

|
|
|

|
|
|

|
|
|
**Animal Husbandry Barn**
--------------------------
.. figure:: _static/animal.png
  :alt: CBRS Hardware
  :align: left
  :width: 400px
  :height: 300px

.. figure:: _static/animal_2.jpeg
  :alt: CBRS Hardware
  :align: left
  :width: 400px
  :height: 300px

|
|
|

|
|
|

|
|
|

|
|
|

**Security and Access**
------------------------

Remote access is provided through VPN, with different profiles for isolation across tenants and granular resource control. Physical access to the OTIC areas is restricted and requires a security badge. Access levels vary, and permissions must be granted by the Testbed Director and the Virginia Tech IT Director. Sensitive equipment and projects are physically separated, and photography of sensitive equipment is prohibited.

**Software Packages**
----------------------

The CORNET/CCI SWVA 5G+ indoor testbed at Virginia Tech uses open-source software, including:

- **OAI (Open Air Interface):** For the UE and gNB, with potential extensions to support srsRAN.
- **OAI-based 5GC:** With potential extensions to support open5GS.
- **O-RAN Software Community (OSC):** To realize O-RAN components and interfaces such as the Non-RT RIC, Near-RT RIC, and the E2 interface. Suitable xApps like KPIMON will be ported to and from the PORT5+ testbed as needed.
- **Other SDR Software:** GNU Radio, REDHAWK, liquid-dsp, and various other open-source SDR software packages can be installed to facilitate experiments involving non-5G waveforms.


**Testbed Introduction**
-------------------------
CORNET/CCI SWVA 5G+ indoor testbed at VT enables research on applications, enabling technologies, and potential enhancements to 5G and future generations of wireless communication systems, as well as other research related to software defined radio, cognitive radio and spectrum sharing including dynamic spectrum access.

**Testbed Configuration**
--------------------------
The CORNET/CCI SWVA 5G+ indoor testbed includes:

- **SDRs:** 10+ Ettus Research USRP X310s, USRP X410s, USRP N310s, and USRP2/USRP N210s.
- **Spectrum Analyzer:** Signal Hound SM200C real-time spectrum analyzer.
- **Workstations and Servers:** Nine rack-mount workstations, a GPU server with 8 GPUs.
- **Synchronization and Mobility:** GPS emulator, Ettus Research Octoclocks for synchronization, and portable resources for ad-hoc experimental configurations and scenarios involving mobility.

.. figure:: _static/test_config.png
  :alt: CBRS Hardware
  :align: center

**Key hardware components**
---------------------------
Key hardware components include:

- **GPU Server:** Dell PowerEdge R750 NVidia A100 GPU Rack-Mount Server.
- **Rack-Mount Servers:** Dell PowerEdge servers.
- **Switches:** Juniper Networks QFX5100-96S.
- **Other Equipment:** Wi-Fi routers, 40 Gbps cables, SDRs, Dell Precision laptops, power supplies, weather enclosures, Raspberry Pis, and UAVs.

**Software Packages**
----------------------
PORT5+ utilizes open-source software for implementation of a 5G and O-RAN-based testbed. Examples of key software packages include OAI for the UE and the gNB (with a potential extension to support srsrRAN), OAI-based 5GC (with a potential extension to support open5GS), and O-RAN Software Community (OSC) software to realize O-RAN components and interfaces such as the Non-RT RIC, Near-RT RIC and the E2 interface. Suitable xApps such as KPIMON will be available as demonstrations in the initial PORT5+ configuration.

**Testbed Introduction**
----------------------------
Portable O-RAN-based Testbed for 5G and beyond (PORT5+) is a Virginia Tech testbed that makes use of open-source software and software-defined radios to facilitate research and design of wireless communication systems. PORT5+ supports 5G New Radio (NR) in the standalone (SA) mode, the 5G core (5GC), and the O-RAN framework with key components such as Near Real-Time Radio Access Network Intelligent Controller (Near-RT RIC) and Non Real-Time Radio Access Network Intelligent Controller (Non-RT RIC).  PORT5+ current version supports Frequency Range 1 (FR1) (i.e., below 7 GHz such as 900 MHz, 3.5 GHz CBRS band, and 5 GHz). The open-source software, OAI (Open Air Interface) software, is used to implement the 5G User Equipment (UE) and the next-generation Node B (gNB). PORT5+ is being developed in stages, and the first version of PORT5+ is expected to be completed in July 2023.

.. figure:: _static/port5+arch.png
  :alt: CBRS Hardware
  :align: center