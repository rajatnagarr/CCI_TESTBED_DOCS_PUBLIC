OpenSAS Architecture
====================

OpenSAS is a sophisticated spectrum access system designed to manage spectrum sharing efficiently. The architecture consists of several core components and interfaces that work together to ensure real-time spectrum management and communication.

Core Components
---------------

.. figure:: _static/OpenSASArchitecture.png
  :alt: CBRS Hardware
  :align: center
  :width: 1150px
  :height: 700px

|

VueJS Webserver
^^^^^^^^^^^^^^^

- **HTTP Server**: The HTTP server is responsible for handling incoming HTTP requests from users. It serves the web interface, allowing users to interact with the system through their browsers. This component is crucial for providing a user-friendly and interactive experience.

Core
^^^^

- **Database**:
  - **Grants**: Stores information about spectrum grants allocated to various users.
  - **Spectrum**: Contains data about the available spectrum and its current usage.
  - **CBSDs**: Maintains records of all registered CBSDs (Citizens Broadband Radio Service Devices), including their operational parameters and statuses.
- **ML Incumbent Inference**:
  - Utilizes machine learning algorithms to detect and infer the presence of incumbent users in the spectrum. This component ensures that the spectrum is dynamically and intelligently managed, avoiding interference with primary users.
- **SAS Functions & Spectrum Sharing Logic**:
  - Implements the core functionality of the Spectrum Access System (SAS), including dynamic spectrum allocation, interference management, and enforcement of spectrum usage policies. This logic ensures fair and efficient spectrum sharing among users.
- **SocketIO Server**:
  - Enables real-time, bidirectional communication between the core system and various clients. This server uses the SocketIO protocol to push updates and receive real-time data, ensuring that the system remains responsive and up-to-date.
- **HTTPS Server**:
  - Secures all communications within the system using HTTPS. This server encrypts data to ensure the privacy and integrity of the information being transmitted, protecting against unauthorized access and cyber threats.

Interfaces
----------

Web Interface
^^^^^^^^^^^^^

- **SocketIO Client**: The web interface includes a SocketIO client that connects to the SocketIO server. This client enables real-time updates and interactions, allowing users to receive immediate feedback and control the system dynamically.

External Sensor Connections
^^^^^^^^^^^^^^^^^^^^^^^^^^^

- **ESC (Environmental Sensing Capability) Sensors**:
  - **ESC Sensor 1 to n**: These sensors are deployed in the field to detect the presence of incumbent spectrum users, such as federal and military users. They report back to the core system, allowing it to make informed decisions about spectrum allocation and avoid interference.
- **CBSDs**:
  - **CBSD 1 to n**: These are the end-user devices that access the shared spectrum. They communicate with the core system through the SAS-CBSD interface, requesting spectrum grants and reporting their operational parameters. The core system allocates spectrum dynamically to these devices, ensuring efficient use of the available resources.

Detailed Workflow
-----------------

1. **User Interaction**: Users interact with the OpenSAS system through the web interface provided by the VueJS webserver. They can request spectrum access, view current spectrum usage, and monitor the status of their CBSDs.
2. **Real-Time Communication**: The SocketIO client in the web interface communicates with the SocketIO server in the core, ensuring real-time updates and responsiveness.
3. **Spectrum Management**:
   - **Data Collection**: ESC sensors continuously monitor the spectrum for incumbent users and report their findings to the core system.
   - **Inference and Allocation**: The ML incumbent inference component analyzes the sensor data to detect incumbent activity. The SAS functions and spectrum sharing logic then allocate spectrum dynamically to CBSDs, ensuring efficient and interference-free operation.
   - **Database Updates**: All spectrum grants, usage data, and CBSD information are stored and updated in the database, maintaining an accurate and up-to-date record of spectrum activities.

Summary
-------

OpenSAS provides a robust framework for dynamic spectrum management, leveraging real-time communication, machine learning, and secure web technologies to ensure efficient and fair spectrum sharing. Its modular architecture allows for scalability and flexibility, making it suitable for various deployment scenarios in modern telecom networks.
