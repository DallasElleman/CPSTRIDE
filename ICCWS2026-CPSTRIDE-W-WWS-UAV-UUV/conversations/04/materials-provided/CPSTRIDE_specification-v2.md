# CPSTRIDE Framework Specification
## A Comprehensive Guide to Cyber-Physical Systems Threat Modeling

---

## Table of Contents
1. [Executive Summary](#executive-summary)
2. [Introduction and Background](#introduction-and-background)
3. [CPSTRIDE vs. STRIDE: Key Differences](#cpstride-vs-stride-key-differences)
4. [Cyber-Physical Flow Diagram (CPFD) Specification](#cyber-physical-flow-diagram-cpfd-specification)
5. [CPSTRIDE Security Properties](#cpstride-security-properties)
6. [CPSTRIDE Threats](#cpstride-threats)
7. [Element-Threat Susceptibility Matrix](#element-threat-susceptibility-matrix)
8. [The CPSTRIDE Threat Modeling Process](#the-cpstride-threat-modeling-process)

---

## Executive Summary

CPSTRIDE is a purpose-built threat modeling framework for Cyber-Physical Systems (CPS) that extends the classic STRIDE model to address the unique security challenges of systems integrating computational elements with physical processes. While STRIDE excels at modeling purely cyber threats to software systems, it lacks capability to represent physical components, energy flows, material transfers, and complex cyber-physical interactions characterizing modern CPS—from additive manufacturing and IoT deployments to critical infrastructure including power grids, transportation networks, and water supply systems.

**Key Innovations:** 

CPSTRIDE expands STRIDE's Security Properties and Threat categories to more broadly cover physical and cyber-physical aspects of systems. CPSTRIDE also introduces the Cyber-Physical Flow Diagram (CPFD), a novel modeling paradigm that extends STRIDE in the following significant ways:
  - It distinguishes between cyber (information/data), physical (material/energy), and cyber-physical (integrated) elements, enabling comprehensive threat identification across all three domains.
  - It provides two completely new flow diagram elements: Devices, which represent Process enablers and Store media; and Links, which represent Flow paths and media.
  - It augments STRIDE's Store element with Nesting to represent hierarchical storage structures within CPS.

---

## Introduction and Background

### What Are Cyber-Physical Systems?

Cyber-Physical Systems (CPS) are technologies and networks characterized by their integration of computation with sensors and actuators to control physical processes. Examples range from:
- **Small-scale:** Medical implants, home appliances, wearable devices
- **Medium-scale:** Autonomous vehicles, industrial robots, smart building systems
- **Large-scale:** Electrical grids, traffic control systems, manufacturing facilities, water treatment plants

### The Problem with Traditional Threat Modeling

Conventional cyber-threat modeling frameworks like STRIDE, MITRE ATT&CK, and the Cyber Kill Chain were designed for information technology (IT) systems and focus primarily on digital assets. This cyber-centric perspective reflects decades of digital transformation that lowered barriers to entry and operational risks for adversaries while simultaneously increasing the potential impact of cyber-attacks. However, this IT-centric worldview creates critical blind spots when applied to CPS:

1. **Lack of Physical Representation:** No standardized way to model physical components, materials, or energy in system diagrams
2. **Incomplete Threat Coverage:** Missing threat categories affecting physical processes and cyber-physical interactions
3. **Data-Centric Security Properties:** Security properties (like Confidentiality) that don't extend naturally to physical resources
4. **No Physical Attack Vectors:** Cannot model attacks that manifest physically or bridge cyber-physical boundaries

### Emerging Cyber-Physical Threat Vectors

Just as digital transformation empowered cyber adversaries by lowering technical and financial barriers to attack, **autonomous and unmanned systems**—including aerial, ground, and underwater vehicles (UAVs, UGVs, UUVs)—are emerging as cyber-physical threat vectors that will similarly empower adversaries across the threat landscape. Nation-states, violent extremist organizations, and lone actors increasingly leverage these systems as both targets and weapons, creating new attack surfaces that transcend purely digital or purely physical domains. These platforms integrate sensors, actuators, and networked computation with physical mobility and capability, making them paradigmatic examples of the cyber-physical security challenges CPSTRIDE addresses.

### Why CPSTRIDE?

CPSTRIDE fills the gap by:
- Providing a systematic framework for modeling both cyber and physical elements
- Expanding security properties to encompass physical and cyber-physical contexts
- Enabling identification of hybrid threats that cross domain boundaries
- Maintaining compatibility with STRIDE's proven methodology while extending its scope

### Real-World Motivation: Additive Manufacturing Vulnerabilities

Additive Manufacturing (AM) systems exemplify CPSTRIDE's scope: digital design files can be stolen or tampered with (cyber); physical parts can contain hidden defects from cyber-attacks (cyber-physical); manufacturing equipment can be damaged through malicious toolpaths (cyber-physical); supply chains can introduce compromised materials (physical); and side channels can leak sensitive information (cyber-physical). These attack vectors span domains, making traditional IT security models insufficient.

---

## CPSTRIDE vs. STRIDE: Key Differences

### Similarities with STRIDE

CPSTRIDE maintains STRIDE's core methodology: a four-step workflow (diagram creation, threat identification, vulnerability investigation, mitigation planning), threat-property mapping, element-based analysis, and iterative refinement.

### Key Differences from STRIDE

#### 1. Diagram Paradigm
| Aspect | STRIDE (DFD) | CPSTRIDE (CPFD) |
|--------|--------------|-----------------|
| **Element Count** | 5 elements | 7 elements (+2 new) |
| **Scope** | Data and code only | Data, energy, and material |
| **Domains** | Cyber only | Cyber, Physical, Cyber-Physical |
| **New Elements** | N/A | Link (L), Device (D), Nested Store (NS) |
| **Element Variants** | Single version each (cyber only) | 3 variants each (C/P/CP) |

#### 2. Security Properties
| STRIDE Property | CPSTRIDE Property | Key Difference |
|-----------------|-------------------|----------------|
| Authentication | **Authenticity** | Extends to verify physical components, e.g., materials, energy sources |
| Integrity | **Integrity** | Extends to physical components, e.g., material composition, structural integrity, energy calibration |
| Non-Repudiation | **Non-Repudiation** | Extends to physical evidence trails, e.g., paper logs, biometrics |
| Confidentiality | **Containment** | Extends to physical materials and energy |
| Availability | **Availability/Reliability** | Extends to physical component reliability, material accessibility, etc. |
| Authorization | **Authorization** | Extends to physical access rights, material handling permissions, etc. |

#### 3. Threat Categories
| STRIDE Threat | CPSTRIDE Threat | Key Difference |
|---------------|-----------------|----------------|
| Spoofing | **Spoofing** | Extends to counterfeit parts, fake physical credentials, physical signals, etc. |
| Tampering | **Tampering** | Extends to physical alteration of components, materials, energy flows, etc. |
| Repudiation | **Repudiation** | Extends to destruction of physical evidence |
| Information Disclosure | **Interception** | Broader concept including unauthorized access to energetic and material components, processes, etc. |
| Denial of Service | **Denial of Service** | Extends to physical destruction, energy disruption, etc. |
| Elevation of Privilege | **Elevation of Privilege** | Extends to physical access to restricted areas |

#### 4. Element Susceptibility
**STRIDE Assumptions (Restrictive):**
- Data Stores: NOT susceptible to Spoofing
- Data Flows: NOT susceptible to Spoofing
- Interactors: NOT susceptible to Tampering, Information Disclosure, Denial of Service
- Only Processes susceptible to Elevation of Privilege

**CPSTRIDE Approach (Comprehensive):**
- ALL elements assumed susceptible to ALL threat categories
- Rationale: Physical dimensions and novel attack vectors in CPS invalidate STRIDE's restrictive assumptions
- Benefit: More thorough threat identification, though requires more analysis effort

#### 5. Conceptual Distinctions

**Process vs. Process Enabler:**
- STRIDE: "Process" conflates the transformation (what) with the software/hardware (how)
- CPSTRIDE: "Process" represents transformations; "Device" represents the physical/cyber-physical enablers
- Examples: 3D printing (Process) vs. 3D printer machine (Device); Chemical synthesis (Process) vs. Chemical reactor (Device)

**Flow vs. Flow Medium:**
- STRIDE: Data Flow doesn't distinguish between data and its transport mechanism
- CPSTRIDE: "Flow" represents data/energy/material in motion; "Link" represents the enabling path/channel/medium
- **Interconnection Rules:**
  - **Flows** interconnect: Stores ↔ Processes ↔ Interactors
  - **Links** interconnect: Devices ↔ Interactors (and enable Flows)
- Examples: 
  - Network packet (Flow) traveling through Ethernet cable (Link)
  - Water (Flow) moving through pipe (Link)
  - Current (Flow) along power line (Link)

**Store vs. Storage Medium:**
- STRIDE: Data Store doesn't account for hierarchical storage or storage media
- CPSTRIDE: "Store" represents contents at rest; "Device" represents containers; "Nested Store" enables hierarchy
- Example: CAD file (Store) on hard drive (Device) within workstation (Device)

#### 6. CPFD Interconnection Architecture

**Critical Architectural Rules:**

CPFD elements follow specific interconnection patterns that reflect the cyber-physical architecture:

**1. Flow Interconnections (F ↔ Elements):**
- **Flows connect:** Stores ↔ Processes ↔ Interactors
- **Flows do NOT directly connect:** Devices
- **Rationale:** Flows represent content in motion (data/energy/material) that is transformed by Processes, held in Stores, or exchanged with Interactors

**2. Link Interconnections (L ↔ Elements):**
- **Links connect:** Devices ↔ Interactors
- **Links enable:** Flows (providing the path/channel/medium)
- **Rationale:** Links represent infrastructure that enables Flows but doesn't transform or store content

**3. Device Role:**
- Devices **enable** Processes and Stores
- Devices are connected by Links
- Flows pass through/between Devices via Links but don't directly connect to Devices

**Valid Connection Patterns:**
```
Store → Flow → Process → Flow → Store
Process → Flow → Interactor
Interactor → Flow → Process
Device ← Link → Device
Device ← Link → Interactor
```

**Invalid Connection Patterns:**
```
Device → Flow → Device [WRONG: Use Link instead]
Store → Link → Store [WRONG: Use Flow instead]
Process ← Link → Process [WRONG: Links don't connect Processes]
```

**Illustrative Example:**
```
[Workstation Computer] ← Link: Ethernet → [Network Router]
      (Device)                 (CL)             (Device)
         |
      enables
         |
[Data Processing] → Flow: Packet → [Database Store]
    (Process)          (CF)              (CS)
```

---

## Cyber-Physical Flow Diagram (CPFD) Specification

### Core Principles

**Domain Classification:**
- **Cyber (C):** Information, data, running code, control signals
- **Physical (P):** Material, machinery, energy, force, space
- **Cyber-Physical (CP):** Integration or combination of both

**Classification Heuristic:**
Each element is categorized based on vulnerability to cyber and/or physical threats:
- Cyber-only: Vulnerable only to cyber attacks (e.g., software, digital files)
- Physical-only: Vulnerable only to physical attacks (e.g., mechanical valve, raw material storage)
- Cyber-physical: Vulnerable to both (e.g., IoT device, smart material, 3D-printed object)

**Visual Conventions:**
1. All lines are solid except for trust boundaries (dashed/dotted)
2. Links and Devices use dashed lines to indicate their special role as enablers with inherent trust boundaries
3. Color optional but must not be required for understanding
4. All elements must be labeled
5. Context diagrams optional for complex systems

### CPFD Elements: Detailed Specifications

---

#### 1. INTERACTOR (I)
**Abbreviations:** CI (Cyber), PI (Physical), CPI (Cyber-Physical)

**Symbol:** Rectangle with sharp corners

**Definition:** An entity that exchanges data, energy, or material with the CPS but remains outside its design scope and/or control boundary.

**Core Meaning:** "Beyond system scope" — entities that interact with but are not part of the system being modeled

**Expanded from STRIDE:** External Entity/Interactor now includes physical and cyber-physical entities

**Connectivity:**
- **Via Flows:** Connects to Stores, Processes, and other Interactors
- **Via Links:** Connects to Devices and other Interactors
- **Trust Boundaries:** Can cross Trust Boundaries in both directions
- **Rationale:** As external entities, Interactors exchange content (Flows) and utilize infrastructure (Links)

**Cyber Interactor (CI) Examples:**
- External APIs and web services
- The Internet and other external networks
- Cloud service providers
- Remote database servers
- External software systems

**Physical Interactor (PI) Examples:**
- Raw material sources (e.g., metal powder suppliers)
- Utility mains (water, gas, electric)
- Manual labor workforce (when not using cyber systems)
- Environmental systems (atmospheric conditions, geographic terrain)
- Simple mechanical input sources

**Cyber-Physical Interactor (CPI) Examples:**
- **Humans:** Employees, contractors, operators, customers interacting via physical and digital interfaces
- **External Organizations:** Supply chain providers, partners, downstream manufacturers
- **Autonomous Systems:** UAVs, UGVs, UUVs, delivery robots, service drones, autonomous vehicles
- **Smart Infrastructure:** Intelligent transportation systems, smart grid components

**Modeling Considerations:**
- Represents entities outside system control; often sources of inputs or recipients of outputs; may be trusted or untrusted (indicated by trust boundaries); can originate intentional attacks or unintentional errors.

---

#### 2. TRUST BOUNDARY (TB)
**Abbreviations:** CTB (Cyber), PTB (Physical), CPTB (Cyber-Physical)

**Symbol:** Dashed or dotted line enclosing areas, rectangular with sharp corners

**Definition:** A virtual and/or physical zone of privileged access.

**Core Meaning:** "Privileged zone" — demarcates areas of different trust levels

**Expanded from STRIDE:** Trust Boundary now includes physical and cyber-physical access controls

**Connectivity:**
- **Not a connectable element** - represents a security zone or perimeter
- **Elements that cross:** Flows, Links, Processes, Stores, and Devices can all cross Trust Boundaries
- **Key principle:** Any element crossing a Trust Boundary should be analyzed for authentication/authorization threats
- **Nesting:** Trust Boundaries can be nested (e.g., secure room within secure building)

**Cyber Trust Boundary (CTB) Examples:**
- Password-protected systems
- Encrypted file systems or databases
- Virtual Private Networks (VPNs)
- Firewalls and DMZs
- Access Control Lists (ACLs)
- Trusted computing environments (TPMs, secure enclaves)
- Authentication-required APIs

**Physical Trust Boundary (PTB) Examples:**
- Physically secured areas with controlled access
- Locked rooms or buildings
- Fenced perimeters with guards
- Analog safes and vaults
- Motor housings and sealed enclosures
- Machine casings protecting internal components
- Physically separated air-gapped networks

**Cyber-Physical Trust Boundary (CPTB) Examples:**
- Clean rooms with both physical locks and electronic badge access
- Data centers with biometric authentication and physical barriers
- Manufacturing facilities with both fences and cyber surveillance
- Server rooms with keycard access and encrypted communications
- Vehicles with both physical keys and immobilizer systems
- Smart safes requiring both combination and biometric verification

**Modeling Considerations:**
- Trust is contextual; boundaries can be nested; crossing boundaries typically involves authentication/authorization; attackers seek to bypass or breach boundaries; defense-in-depth implies multiple boundaries.

---

#### 3. STORE (S) / NESTED STORE (NS)
**Abbreviations:** CS (Cyber), PS (Physical), CPS (Cyber-Physical), NCS (Nested Cyber), NPS (Nested Physical), NCPS (Nested Cyber-Physical)

**Symbol:** Drum shape, solid outline; alternatively, two parallel horizontal solid lines (often referred to as an "open rectangle")

**Definition:** Data, energy, or material at rest, distinct from its storage medium or container. Nesting is allowed.

**Core Meaning:** "At rest" — content that is stored, not in motion

**Expanded from STRIDE:** Data Store now includes physical materials and energy, and supports hierarchical nesting

**Connectivity:**
- **Via Flows:** Connects to Processes, Interactors, and other Stores
- **Does NOT connect via Links** (Links connect infrastructure, not content)
- **Enabled by:** Devices (Stores exist within/on storage Devices)
- **Nesting:** Stores can be nested within other Stores to represent hierarchical storage structures
- **Valid Example:** `[Database] (CS) → Flow → [Data Analysis Process] (CP)`
- **Invalid Example:** `[Database] (CS) ← Link → [Server] (CPD)`

**Cyber Store (CS) Examples:**
- **Files:** CAD files, 3D models, toolpath files, configuration files
- **Databases:** Relational databases, NoSQL databases, time-series data
- **Registry Keys:** Windows registry, system configuration stores
- **Memory:** RAM, cache, buffers (when data is at rest)
- **Logs:** Audit logs, system logs, security event logs
- **Keys/Certificates:** Cryptographic keys, digital certificates

**Physical Store (PS) Examples:**
- **Raw Materials:** Metal powders, plastic filaments, chemical reagents
- **Energy Reserves:** Batteries, charged capacitors, fuel tanks
- **Manufactured Objects:** Completed products, work-in-progress parts
- **Physical Keys:** Mechanical keys, physical tokens
- **Consumables:** Lubricants, coolants, cleaning supplies

**Cyber-Physical Store (CPS) Examples:**
- **Smart Materials:** RFID-tagged inventory, materials with embedded sensors
- **Physical Keycards:** Magnetic stripe or chip-based access cards
- **3D-Printed Objects:** *Special case* — physical objects that carry cyber vulnerabilities from their digital origins (design flaws, embedded defects)
- **Instrumented Components:** Parts with embedded sensors or identification
- **Tagged Assets:** Equipment with IoT monitoring capabilities

**Nested Stores:**
Represent hierarchical storage relationships:
- **Example 1:** Part CAD File (NCS2) contains:
  - Design History (NCS2.1)
  - 3D Model (NCS2.2)
  - Simulation Results (NCS2.3)
  - Sliced Model (NCS2.4)
  - Toolpath (NCS2.5)
- **Example 2:** Material Cartridge (CPS) contains:
  - Metal Powder (PS)
  - Purity Certification Data (CS)

**Modeling Considerations:**
- Distinguish contents from storage medium (use Device for containers); nested stores represent logical containment; consider both intentional storage and unintentional remnants; think about persistence duration.

---

#### 4. FLOW (F)
**Abbreviations:** CF (Cyber), PF (Physical), CPF (Cyber-Physical)

**Symbol:** One-way or two-way arrow (indicating directionality), solid line

**Definition:** Data, energy, or material in motion, distinct from its enabling path, channel, or medium.

**Core Meaning:** "In motion" — the transfer or movement of content

**Expanded from STRIDE:** Data Flow now includes energy and material transfers

**Connectivity:**
- **Connects:** Store ↔ Process ↔ Interactor
- **Does NOT directly connect:** Devices
- **Enabled by:** Links (which provide the path, channel, or medium)
- **Directionality:** All Flows have direction (indicated by arrows)
- **Key distinction:** Represents content in motion, not the medium enabling that motion

**Cyber Flow (CF) Examples:**
- **Network Communications:** HTTP/HTTPS traffic, TCP/IP packets, UDP datagrams
- **Function Calls:** API calls, method invocations, system calls
- **Data Transfers:** File transfers (FTP, SCP), database queries/responses
- **Messages:** Email, instant messages, message queue traffic
- **Process I/O:** Input from keyboard, output to display
- **Streaming Data:** Video streams, audio streams, real-time telemetry

**Physical Flow (PF) Examples:**
- **Material Flows:** 
  - Raw materials moving through pipes or conveyors
  - Parts being transported between workstations
  - Waste material removal
- **Energy Transfers:**
  - Electrical current through wires
  - Heat transfer via conduction/convection/radiation
  - Hydraulic or pneumatic pressure
- **Mechanical Forces:**
  - Applied pressure or torque
  - Vibration or shock transmission
- **Physical Process I/O:** Manual material handling, manual inspection

**Cyber-Physical Flow (CPF) Examples:**
- **Sensor Data Streams:** Temperature, pressure, position readings transmitted digitally
- **Control Signals:** Digital commands that trigger physical actuation
- **HVAC Communications:** Smart thermostat controlling physical heating/cooling
- **IoT Data:** Smart devices transmitting status and receiving commands
- **Transport of Smart Materials:** Moving materials with embedded sensors/RFID
- **Human-Machine Interaction:** Touchscreen input, voice commands, haptic feedback
- **Cyber-Physical Process I/O:** Automated material handling with tracking

**Modeling Considerations:**
- Flows are directional; distinguish content (Flow) from medium (Link); consider intended flows and covert channels; assess integrity, confidentiality, and availability; prioritize flows crossing trust boundaries.

---

#### 5. PROCESS (P)
**Abbreviations:** CP (Cyber), PP (Physical), CPP (Cyber-Physical)

**Symbol:** Rectangle with rounded corners, solid outline

**Definition:** Activity that transforms inputs into outputs.

**Core Meaning:** "Transformation" — functions that modify, combine, or convert inputs

**Expanded from STRIDE:** Process now explicitly distinguishes transformations from their enablers (Devices)

**Connectivity:**
- **Via Flows:** Connects to Stores, Interactors, and other Processes
- **Does NOT connect via Links** (Links connect infrastructure, not transformations)
- **Enabled by:** Devices (Processes execute on/within computational or physical Devices)
- **Pattern:** Processes typically receive input Flows and produce output Flows
- **Example:** `[Sensor Data] (CS) → Flow → [Analysis Process] (CP)`
- **Invalid:** `[Analysis Process] (CP) ← Link → [Computer] (CPD)`

**Cyber Process (CP) Examples:**
- **Software Execution:** Any running code or computational transformation
- **CAD Software Operations:** Design, simulation, finite element analysis
- **Slicing Algorithms:** Converting 3D models to layered instructions
- **Toolpath Generation:** Creating machine instructions from sliced data
- **Data Analysis:** Statistical processing, machine learning inference
- **Encryption/Decryption:** Cryptographic transformations
- **Compilation:** Source code to executable transformation

**Characteristics:**
- Only digital inputs and outputs
- Typically enabled by software running on cyber or cyber-physical devices

**Physical Process (PP) Examples:**
- **Manual Manufacturing:** Hand assembly, manual machining
- **Simple Chemical Reactions:** Mixing raw materials without digital control
- **Mechanical Transformations:** Manual cutting, grinding, polishing
- **Raw Material Refining:** Simple physical separation or purification
- **Combustion:** Burning fuel for heat/energy (distinct from digital control processes)
- **Natural Processes:** Cooling, drying, settling

**Characteristics:**
- Only physical inputs and outputs
- No computational or digital control elements
- May be enabled by purely physical devices (PP) or simple mechanical tools

**Cyber-Physical Process (CPP) Examples:**
- **Additive Manufacturing (3D Printing):**
  - Inputs: Toolpath file (C), Material cartridge (CP)
  - Outputs: Printed part (CP)
  - Transformation: Digital instructions → Physical object
- **CNC Machining:**
  - Inputs: G-code (C), Raw material stock (P)
  - Outputs: CNC-machined part (CP)
- **Robotic Assembly:**
  - Inputs: Assembly instructions (C), Component parts (P), Sensor feedback (CP)
  - Outputs: Assembled product (CP)
- **Smart Building HVAC:**
  - Inputs: Temperature setpoints (C), Environmental sensors (CP)
  - Outputs: Heated/cooled air (P), Status data (C)
- **Automated Quality Control:**
  - Inputs: Inspection parameters (C), Physical part (P)
  - Outputs: Pass/fail decision (C), Automatically sorted parts (CP)

**Characteristics:**
- Cyber-physical inputs and/or outputs
- Integration of digital control with physical action
- Typically enabled by cyber-physical devices (CPD)

**Modeling Considerations:**
- Focus on WHAT transforms, not HOW (use Devices for "how"); consider transformation failures and unexpected behaviors; processes are prime Elevation of Privilege targets; assess intended functionality and potential abuse.

---

#### 6. LINK (L) — NEW IN CPSTRIDE
**Abbreviations:** CL (Cyber), PL (Physical), CPL (Cyber-Physical)

**Symbol:** Dashed two-way arrow (Links are inherently bi-directional, while Flows are either uni-directional or bi-directional)

**Definition:** A logical and/or physical path, channel, or medium that connects and enables Flows between CPFD elements.

**Core Meaning:** "Enabler of flows" — the infrastructure that makes transfers possible

**New Element Rationale:** 
In CPS, the medium of a flow is often as security-relevant as the flow itself. For example:
- An encrypted message (Flow) over an unencrypted WiFi channel (Link) is vulnerable
- Gas (Flow) through a corroded pipe (Link) presents safety/security risks
- The "how" of connectivity matters for security analysis

**Connectivity:**
- **Connects:** Device ↔ Device, Device ↔ Interactor  
- **Does NOT connect:** Stores, Processes, other Interactors
- **Enables:** Flows (by providing the physical/logical path, channel, or medium)
- **Key distinction:** Represents infrastructure and medium, not the content traveling across it
- **Example relationship:** Ethernet cable (Link) enables network packets (Flow)

**Cyber Link (CL) Examples:**
- **Communication Protocols:** HTTP, HTTPS, SSH, TLS, MQTT, Modbus
- **Network Media (logical):** TCP/IP, UDP, Ethernet protocol, WiFi 802.11
- **Data Structures:** JSON, XML, Protocol Buffers, file formats
- **Communication Ports:** Port 80 (HTTP), Port 443 (HTTPS), Port 22 (SSH)
- **Channels:** Named pipes, message queues, shared memory
- **File Formats/Schema:** CAD file specifications, database schemas

**Physical Link (PL) Examples:**
- **Geographic Routes:** Roads, railways, shipping lanes, flight paths
- **Power Lines:** Electrical transmission lines, power distribution cables
- **Fluid Pipes:** Water pipes, gas pipelines, hydraulic lines, pneumatic tubes
- **Mechanical Connections:** Axles, gears, belts, chains
- **Wired Media (physical):** Copper wire, fiber optic cable

**Cyber-Physical Link (CPL) Examples:**
- **Radio Frequency Spectrum:** WiFi bands, Bluetooth, cellular networks, satellite links
- **Optical Transmission Through Air:** Visible light, infrared, laser communication
- **Acoustic Transmission Through Air:** Sound waves (including ultrasonic)
  - *Security Relevance:* Side-channel attacks via acoustic emanations from machinery
- **Wired Connections with Cyber Protocols:** Ethernet cables (Cat5/Cat6), USB cables, RS-232
- **Electromagnetic Fields:** Near-field communication (NFC), wireless charging

**Modeling Considerations:**
- Links enable Flows—identify both
- Links are inherently bi-directional, while Flows are either uni-directional or bi-directional.
- Assess Link security independently of Flow security
- Determine Link domain (C/P/CP) by the potential presence of only cyber vulnerabilities, only physical vulnerabilities, or both types.
- Distinguish broadcast vs. point-to-point media
- Link failures can cause denial of service.

**Examples in Context:**
- Email message (CF) transmitted via SMTP protocol (CL) via Ethernet cable (CPL)
- Natural gas (PF) flowing through pipeline (PL)
- Sensor reading (CPF) transmitted via Modbus protocol (CL) over RS-485 cable (CPL)

---

#### 7. DEVICE (D) — NEW IN CPSTRIDE
**Abbreviations:** CD (Cyber), PD (Physical), CPD (Cyber-Physical)

**Symbol:** Rectangle with rounded corners, dashed outline

**Definition:** An instantiation of computational capability and/or physical functionality for Processes and Stores; a virtually- and/or physically-embodied enabler of Processes and/or Storage in a cyber-physical system.

**Core Meaning:** "Enabler of processes and stores" — the infrastructure that makes computation, storage, and physical action possible

**New Element Rationale:**
STRIDE's "Process" conflates transformations with the software/hardware that performs them. In CPS, this distinction is critical:
- A 3D printer (Device) can be attacked without affecting the 3D printing process design
- A compromised hard drive (Device) can leak data from files (Stores) even if applications (Processes) are secure
- Physical machinery can fail or be sabotaged independently of the processes they perform

**Connectivity:**
- **Via Links:** Connects to other Devices and Interactors
- **Does NOT connect via Flows** (Flows represent content, not infrastructure)
- **Enables:** Processes (execution) and Stores (storage)
- **Supports:** Flows pass through/between Devices via the Links that connect them
- **Valid Example:** `[Workstation] (CPD) ← Link → [Network Switch] (CPD)`
- **Invalid Example:** `[Workstation] (CPD) → Flow → [Server] (CPD)`

**Cyber Device (CD) Examples:**
- **Virtualized Resources:**
  - Virtual machines (VMs)
  - Docker containers
  - Kubernetes pods
- **Cloud Resources:**
  - Cloud compute instances (EC2, Azure VM)
  - Cloud storage instances (S3, Azure Blob)
  - Content Delivery Networks (CDN)
  - Distributed ledgers (blockchain nodes)
- **Abstracted Digital Resources:**
  - Software agents
  - Virtual sensors
  - Digital controllers
  - Digital twins (virtual replicas of physical systems)
- **Remote Systems:**
  - Remote database servers
  - Application servers
  - Load balancers

**Physical Device (PD) Examples:**
- **Actuators:**
  - Mechanical actuators (linear, rotary)
  - Manual valves and switches
  - Hydraulic motors
  - Pneumatic cylinders
- **Instrumentation:**
  - Analog gauges and meters
  - Mechanical timers
  - Physical thermometers/barometers
- **Storage Containers:**
  - Material storage tanks
  - Pressure vessels
  - Chemical reagent containers
  - Physical key storage lockboxes
  - Filing cabinets
- **Mechanical Systems:**
  - Conveyor belts
  - Pulleys and levers
  - Manual tools (non-powered)

**Cyber-Physical Device (CPD) Examples:**
- **Manufacturing Equipment:**
  - **3D Printers:** Additive manufacturing machines
  - CNC machines
  - Industrial robots
  - Laser cutters
- **Computing Hardware:**
  - Desktop computers
  - Laptops
  - Servers (physical machines)
  - Network routers and switches
  - Embedded systems
- **IoT and Smart Devices:**
  - Smart thermostats
  - Smart home devices (locks, cameras, appliances)
  - Wearable devices
  - IoT-enabled medical implants
- **Industrial Control Systems:**
  - Programmable Logic Controllers (PLCs)
  - Supervisory Control and Data Acquisition (SCADA) systems
  - Distributed Control Systems (DCS)
- **Autonomous and Connected Vehicles:**
  - UAVs, UGVs, UUVs (aerial, ground, underwater unmanned vehicles)
  - Autonomous and connected cars, trucks, vessels
- **Smart Infrastructure:**
  - Smart inventory management systems
  - RFID-enabled storage cabinets
  - IoT-connected storage tanks with sensors
  - Automated warehouse systems

**Modeling Considerations:**
- Devices enable Processes and Stores; a single physical device may host multiple logical elements; devices can be compromised independently; consider supply chain attacks; assess physical location and access threats; device failures can cascade.

**Relationship to Other Elements:**
- **Processes run ON Devices:** CAD software (CP) runs on a workstation (CPD)
- **Stores exist IN/ON Devices:** CAD files (CS) stored on hard drive (CPD)
- **Devices CONNECT via Links:** Two servers (CPD) connected by Ethernet cable (CPL)

---

### CPFD Modeling Best Practices

1. **Start with Context:** Create high-level context diagrams before detailed breakdowns
2. **Avoid Magic:** No sources/sinks without Interactors; show Processes and Stores with enabling Devices and Links
3. **Collapse When Appropriate:** Combine similar elements within trust boundaries; balance detail with comprehensibility
4. **Distinguish "What" from "How":** Processes/Flows represent transformations/transfers; Devices/Links represent enablers/media
5. **Label Everything:** Use consistent, unique naming with element type prefixes (e.g., CPD3: AM Printer)

---

## CPSTRIDE Security Properties

Security properties define the positive security characteristics that systems should exhibit. CPSTRIDE threats violate these properties.

### 1. AUTHENTICITY
**Subsumes STRIDE's:** Authentication

**Definition:** System elements (users, processes, devices, materials, energy sources) are genuine and verifiable. This extends STRIDE's Authentication—focused on digital identity verification—to encompass genuineness of physical components, materials, and energy signatures in cyber-physical contexts.

**Cyber Context Examples:**
- User login credentials verified via password, MFA, biometrics
- Digital certificates validate server identity
- API keys authenticate calling applications
- Software signatures verify code provenance

**Physical Context Examples:**
- Verifying that parts came from authorized suppliers (not counterfeit)
- Authenticating material composition (e.g., metal alloy purity)
- Confirming genuine physical access credentials (not forged badges)
- Validating authenticity of physical keys

**Cyber-Physical Context Examples:**
- RFID tags that verify both digital identity and physical presence
- Biometric systems combining physical traits with digital authentication
- Blockchain-based supply chain tracking verifying material provenance
- GPS signals authenticating geographic location

**Why It Matters in CPS:**
Counterfeit parts, adulterated materials, and spoofed sensor readings can have safety-critical consequences in CPS. A fake aircraft component might catastrophically fail; contaminated pharmaceutical ingredients could harm patients.

---

### 2. INTEGRITY

**Definition:** System elements (data, software, firmware, hardware, materials, energy parameters) remain unaltered and uncorrupted by unauthorized means throughout their lifecycle. This extends STRIDE's data Integrity to include physical properties, e.g., material composition, structural integrity, and energy calibration.

**Cyber Context Examples:**
- CAD files protected from unauthorized modification via access controls
- Digital signatures or hashes detect file tampering
- Database transaction logs maintain data integrity
- Version control systems track changes
- Code signing prevents unauthorized software modification

**Physical Context Examples:**
- Material composition remains pure (not contaminated or substituted)
- Structural integrity of parts not compromised (no hidden voids or cracks)
- Mechanical calibration not altered (torque wrenches, scales maintain accuracy)
- Energy reserves not diluted (fuel not mixed with water)

**Cyber-Physical Context Examples:**
- Sensor calibration remains accurate (not manipulated to give false readings)
- 3D-printed parts maintain intended mechanical properties, do not contain hidden defects or vulnerabilities
- Embedded firmware in IoT devices not modified maliciously
- Smart materials retain their programmed behaviors

**Why It Matters in CPS:**
A tampered CAD file can propagate through the AM process chain to produce a part with hidden structural defects. Modified sensor calibration can cause incorrect control decisions, leading to equipment damage or safety hazards.

---

### 3. NON-REPUDIATION

**Definition:** Actions performed within the system cannot be denied by their initiator, through providing sufficient evidence across cyber and physical domains—extending beyond digital audit trails to include physical evidence trails, sensor data, surveillance records, and material verification techniques.

**Cyber Context Examples:**
- Digital signatures provide proof of who signed a document
- Audit logs with cryptographic protection prevent alteration
- Email headers and timestamps prove message sending
- Blockchain transactions are immutably recorded
- Database transaction logs capture all modifications

**Physical Context Examples:**
- Video surveillance provides physical evidence of actions
- Physical access logs, sign-in sheets
- Material chain-of-custody documentation
- Tamper-evident seals show if containers were opened
- Mechanical locks that log opening/closing

**Cyber-Physical Context Examples:**
- Smart card readers log both digital identity and physical presence
- IoT sensors create timestamped records of physical events
- Manufacturing systems log both digital commands and physical actions
- Biometric systems provide multi-factor proof of identity
- GPS tracking proves location at specific times

**Why It Matters in CPS:**
Without non-repudiation, malicious insiders can sabotage manufacturing processes or steal materials while denying responsibility. Quality issues in produced parts may be difficult to trace back to specific operators or process steps.

---

### 4. CONTAINMENT
**Subsumes STRIDE's:** Confidentiality

**Definition:** System elements (data, energy, material resources) remain within authorized boundaries and are accessible only to entities with appropriate privileges. This extends STRIDE's Confidentiality—focused on information disclosure—to encompass physical confinement of materials and energy, preventing unauthorized extraction, leakage, or diversion.

**Cyber Context Examples:**
- Encrypted files prevent unauthorized reading
- Access controls limit who can view sensitive data
- Network segmentation prevents lateral movement
- Data loss prevention (DLP) systems block exfiltration
- Encrypted communications protect data in transit

**Physical Context Examples:**
- Materials stored in secured, locked containers
- Precious metals kept in vaults
- Hazardous chemicals in controlled environments
- Waste materials properly contained (not leaked to environment)
- Energy contained within intended systems (no losses or theft)

**Cyber-Physical Context Examples:**
- Side-channel attacks contained (shielding against acoustic/EM emanations)
- Wireless power transmission only to authorized recipients
- Smart meters prevent unauthorized energy diversion
- RFID-protected inventory prevents unauthorized removal
- Manufacturing parameters kept confidential (contained in secure systems)

**Why It Matters in CPS:**
Intellectual property in the form of CAD files, manufacturing parameters, or material formulas can be stolen. Physical materials can be diverted or leaked. Energy can be siphoned from electrical grids or wireless charging systems.

---

### 5. AVAILABILITY / RELIABILITY

**Definition:** System functions, services, and resources are accessible and operational when needed, at expected performance levels. This extends digital Availability to include physical reliability of components, consistent energy supply, material accessibility, and operational continuity across the cyber-physical spectrum.

**Cyber Context Examples:**
- Web services maintain uptime (no denial of service)
- Redundant servers provide failover capability
- Backup systems enable recovery from failures
- Load balancing prevents resource exhaustion
- DDoS protections maintain service availability

**Physical Context Examples:**
- Manufacturing equipment operational when needed (minimal downtime)
- Material supplies available to meet production schedules
- Energy systems provide consistent power without interruptions
- Safety systems functional at all times
- Physical access paths remain clear (no blockages)

**Cyber-Physical Context Examples:**
- Sensor networks maintain continuous monitoring
- Automated manufacturing processes run to completion
- Control systems respond within required time constraints
- IoT devices maintain connectivity and function
- Smart grid maintains stable power delivery

**Why It Matters in CPS:**
Production delays from unavailable equipment or materials have economic costs. Safety-critical systems must maintain availability to prevent harm. Attackers may target availability through physical destruction, resource exhaustion, or cyber attacks.

---

### 6. AUTHORIZATION

**Definition:** Specific entities are explicitly granted or denied permission to access, control, or modify certain system elements. This extends digital access controls to include physical access rights, operational authority over equipment, material handling permissions, and energy distribution controls.

**Cyber Context Examples:**
- Role-based access control (RBAC) limits system permissions
- Access Control Lists (ACLs) specify who can access files/resources
- Privileged accounts restricted to authorized administrators
- API access tokens limit what applications can do
- Multi-factor authentication enforces authorization

**Physical Context Examples:**
- Physical key distribution controls who can enter areas
- Operator certifications authorize equipment use
- Material handling procedures specify who can access chemicals
- Security clearances determine access to sensitive areas
- Lockout/tagout procedures control equipment operation

**Cyber-Physical Context Examples:**
- Smart locks authorize access based on digital credentials and physical presence
- Manufacturing systems enforce operator permissions via badge and login
- Energy management systems control who can modify power distribution
- IoT devices restrict control to authorized applications and users
- Autonomous vehicles validate operator credentials before granting control

**Why It Matters in CPS:**
Unauthorized access to manufacturing equipment can lead to sabotage, IP theft, or safety incidents. Unauthorized personnel handling hazardous materials create risks. Equipment misuse by untrained operators can cause damage.

---

### Security Property Summary Table

| Property | Violating Threat | Cyber Focus | Physical Extension | Example Violation |
|----------|------------------|-------------|-------------------|-------------------|
| **Authenticity** | Spoofing | Verify user/process identity | Verify material/part genuineness | Counterfeit aircraft part installed |
| **Integrity** | Tampering | Prevent data modification | Prevent material contamination | CAD file altered to introduce defect |
| **Non-Repudiation** | Repudiation | Maintain audit trails | Maintain physical evidence | Operator denies modifying settings |
| **Containment** | Interception | Prevent data disclosure | Prevent material extraction | Material or energy diversion; Proprietary formula leaked via side-channel |
| **Availability/Reliability** | Denial of Service | Maintain system uptime | Ensure material/equipment availability | Production halted by equipment sabotage |
| **Authorization** | Elevation of Privilege | Enforce access controls | Control physical access | Unauthorized person operates machinery |

---

## CPSTRIDE Threats

Threats are the potential security violations that can occur in a system. Each CPSTRIDE threat category violates a corresponding security property.

### Threat Analysis Framework

For each element in a CPFD, consider how each threat category applies from three perspectives:
1. **Subject:** The element performs the threat action
2. **Object/Target:** The element is the victim of the threat
3. **Instrument:** The element is used as a means to threaten another target

This systematic approach ensures comprehensive threat identification.

---

### 1. SPOOFING
**Violates:** Authenticity

**Definition:** Falsification of identity, source, or authenticity of system elements (users, processes, signals, physical/cyber-physical stores), undermining trust mechanisms and authentication controls.

**Cyber-Only Examples:**
- **Phishing:** Emails pretending to be from trusted sources
- **Smishing:** SMS phishing attacks
- **Social Engineering:** Impersonating authorized personnel
- **WiFi SSID Spoofing:** Broadcasting trusted network names
- **Typosquatting:** Registering similar domain names
- **Deepfakes:** AI-generated audio/video impersonations
- **IP Address Spoofing:** Forging packet source addresses
- **DNS Spoofing:** Redirecting domain lookups to malicious servers

**Physical-Only Examples:**
- **Faking Physical Credentials:** Forging badges, uniforms, or documents
- **Counterfeit Parts:** Passing off fake components as genuine OEM parts
- **Forged Signatures:** Imitating authorized signatures on physical documents
- **Fake Materials:** Substituting inferior materials while claiming they're specification-grade
- **Impersonation:** Pretending to be authorized personnel for physical access

**Cyber-Physical Examples:**
- **GPS Spoofing:** Broadcasting fake GPS signals to misguide UAVs, UGVs, UUVs, or other autonomous vehicles
- **Sensor Reading Injection:** Injecting counterfeit sensor readings over OT networks (e.g., false temperature readings triggering incorrect control responses)
- **Counterfeit Smart Materials:** Materials with forged RFID tags claiming false properties
- **Badge Cloning:** Copying RFID access cards to impersonate authorized users
- **Biometric Spoofing:** Using fake fingerprints or facial masks to bypass biometric systems
- **Autonomous System Impersonation:** Spoofing identification transponders on UAVs or autonomous vehicles to masquerade as authorized units

**Additive Manufacturing-Specific Examples:**
- Substituting inferior material powders while claiming they meet specifications
- Providing counterfeit replacement parts for 3D printers
- Spoofing calibration certificates for manufacturing equipment

**Impact Assessment:**
- Loss of trust in system identity verification
- Unauthorized access to resources
- Downstream effects of accepting false data/materials as genuine
- Safety incidents from using counterfeit parts

---

### 2. TAMPERING
**Violates:** Integrity

**Definition:** Unauthorized modification, corruption, or alteration of legitimate cyber-physical entities (data, structures, energy flows, material compositions, control signals) that compromises system integrity.

**Cyber-Only Examples:**
- **File Modification:** Altering CAD files, configuration files, or executables
- **Database Tampering:** Unauthorized changes to database records
- **Configuration Changes:** Modifying system settings or registry keys
- **Code Injection:** Inserting malicious code into applications (SQL injection, XSS)
- **Firmware Modification:** Altering device firmware
- **Control Logic Tampering:** Modifying industrial automation software
- **Log Tampering:** Deleting or altering audit logs to hide activities

**Physical-Only Examples:**
- **Physical Adjustment:** Manually adjusting valve settings, calibration screws
- **Material Contamination:** Mixing impurities into raw materials
- **Component Sabotage:** Damaging mechanical parts
- **Document Alteration:** Changing physical records or specifications
- **Unauthorized Modifications:** Adding/removing components from machinery

**Cyber-Physical Examples:**
- **Sensor Manipulation via EMI:** Using electromagnetic interference to alter sensor readings
  - Causes system to respond to fabricated conditions
- **Toolpath Modification:** Altering G-code or manufacturing instructions
  - Results in incorrect dimensions, weakened structures, or equipment damage
- **Parameter Poisoning:** Changing manufacturing parameters (temperature, speed, pressure)
  - Introduces defects not detectable by standard inspection
- **3D Model Tampering:** Introducing hidden voids or weaknesses in digital models
  - Manifests as delayed failure in physical parts
- **Smart Material Alteration:** Modifying properties of materials with embedded electronics

**Additive Manufacturing-Specific Examples:**
- Tampering with slicing parameters to introduce porosity in parts
- Modifying laser power settings to weaken layer bonding
- Altering toolpath orientation to compromise part strength
- Introducing hidden internal structures that cause strategic failure
- Manipulating design history to propagate defects through process chain

**Impact Assessment:**
- Compromised part quality and safety
- Equipment damage from destructive operations
- Data integrity loss affecting decision-making
- Cascading failures through interconnected systems

---

### 3. REPUDIATION
**Violates:** Non-Repudiation

**Definition:** Denial of responsibility for actions within the system, through passive rejection of accountability or active measures to destroy, corrupt, or disable auditing mechanisms or evidence trails.

**Cyber-Only Examples:**
- **Log Deletion:** Erasing system logs, security logs, or audit trails
- **Timestamp Manipulation:** Altering timestamps to obscure when actions occurred
- **Disabling Logging:** Turning off audit mechanisms before performing actions
- **Covering Tracks:** Using tools to remove evidence of intrusion
- **Denying Digital Actions:** Claiming "I didn't send that email" when you did
- **Anti-Forensic Tools:** Using software to wipe evidence from systems

**Physical-Only Examples:**
- **Destroying Physical Records:** Shredding documents, burning logs
- **Tampering with Surveillance:** Disabling cameras, erasing footage
- **Removing Physical Evidence:** Cleaning up after physical intrusion
- **Claiming Ignorance:** "I didn't touch that valve" when you did
- **Falsifying Documentation:** Backdating or altering physical records

**Cyber-Physical Examples:**
- **Cross-Domain Log Corruption:** Manipulating both digital and physical audit systems
  - Example: Erasing both access badge logs and digital login records
- **Sensor Data Manipulation:** Altering sensor records to hide physical actions
- **Synchronized Evidence Destruction:** Simultaneously destroying physical and digital evidence
- **Timeline Obscuration:** Using both cyber and physical means to make reconstruction impossible
- **Badge Log Tampering:** Modifying both the physical access log and digital database

**Additive Manufacturing-Specific Examples:**
- Modifying toolpath execution logs to hide malicious instructions
- Deleting design revision history to obscure tampering
- Erasing quality control test records to hide defective parts
- Disabling printer operation logs before sabotage
- Claiming a part failure was due to design flaw rather than sabotage

**Impact Assessment:**
- Inability to hold actors accountable for malicious actions
- Difficulty in incident investigation and root cause analysis
- Loss of trust in accountability mechanisms
- Legal and compliance issues

---

### 4. INTERCEPTION
**Subsumes STRIDE's:** Information Disclosure

**Violates:** Containment

**Definition:** Unauthorized acquisition or monitoring of system resources (data, energy flows, physical materials), violating containment. This extends Information Disclosure to physical and energy contexts.

**Cyber-Only Examples:**
- **Network Sniffing:** Capturing network traffic to read unencrypted data
- **Database Breaches:** Unauthorized access to databases for data theft
- **Memory Dumping:** Reading sensitive data from RAM or process memory
- **Keylogging:** Recording keystrokes to capture passwords or data
- **Eavesdropping on Communications:** Intercepting phone calls, emails, messages
- **Intellectual Property Theft:** Stealing CAD files, source code, trade secrets
- **Configuration Data Theft:** Capturing system settings, credentials

**Physical-Only Examples:**
- **Material Theft:** Physically extracting materials from manufacturing processes
- **Product Diversion:** Stealing finished products from warehouses
- **Energy Theft:** Illegally tapping into power lines or fuel supplies
- **Physical Surveillance:** Observing operations through windows or hidden cameras
- **Document Theft:** Stealing physical plans, specifications, or records
- **Shoulder Surfing:** Watching someone enter PINs or passwords

**Cyber-Physical Examples:**
- **Side-Channel Attacks:**
  - **Acoustic:** Reconstructing 3D models from printer sounds
  - **Thermal:** Using thermal imaging to infer operations or extract data
  - **Electromagnetic:** Capturing EM emissions to read data (Van Eck phreaking)
  - **Power Analysis:** Monitoring power consumption to infer computation
- **Wireless Energy Harvesting:** Unauthorized coupling to wireless charging systems
- **Sensor Eavesdropping:** Intercepting sensor data streams
- **RFID Skimming:** Remotely reading RFID tags without authorization
- **Smart Meter Tampering:** Accessing consumption data or diverting energy

**Additive Manufacturing-Specific Examples:**
- Stealing CAD files containing proprietary designs
- Extracting manufacturing parameters from toolpath files
- Using acoustic emanations to replicate parts without accessing files
- Thermal imaging to determine material properties being used
- Side-channel reconstruction of 3D models from printer vibrations
- Stealing 3D-printed parts, material formulations or powder compositions

**Impact Assessment:**
- Loss of intellectual property and competitive advantage
- Privacy violations
- Theft of physical assets
- Compromise of trade secrets
- Regulatory compliance violations (GDPR, HIPAA, ITAR)

---

### 5. DENIAL OF SERVICE
**Violates:** Availability / Reliability

**Definition:** Impairment or prevention of system availability through any means that renders services, functions, or resources inaccessible or unreliable for legitimate users.

**Cyber-Only Examples:**
- **Network Flooding:** DDoS attacks overwhelming network bandwidth
- **Resource Exhaustion:** Consuming all CPU, memory, or disk space
- **Logic Bombs:** Triggered code that crashes or disables systems
- **Ransomware:** Encrypting data to make it inaccessible
- **Service Crashes:** Exploiting bugs to cause application failures
- **Database Locking:** Holding locks that prevent legitimate access
- **Communication Jamming (Digital):** Disrupting digital radio communications

**Physical-Only Examples:**
- **Physical Destruction:** Kinetically disabling or destroying physical plant; Smashing equipment with hammers
- **Blockage:** Blocking material flows, access paths, or ventilation
- **Component Sabotage:** Damaging critical components (cutting belts, breaking switches)
- **Material Contamination:** Rendering raw materials unusable
- **Energy Disruption:** Cutting power lines, depleting fuel
- **Environmental Manipulation:** Introducing extreme heat, cold, humidity
- **Irreversible Physical Alterations:** Permanently damaging machinery

**Cyber-Physical Examples:**
- **Electromagnetic Interference (EMI):** Disrupting wireless communications and sensors
- **Physical Obstruction of Sensors/Actuators:** Blocking sensor line-of-sight, jamming actuators
- **Induced Vibration:** Using vibration to disrupt precision equipment
- **Thermal Attacks:** Overheating components to cause shutdowns or failures
- **GPS Jamming:** Denying location services to UAVs, UGVs, UUVs, and other autonomous systems
- **Battery Depletion Attacks:** Draining IoT device or autonomous vehicle batteries rapidly
- **Destructive Toolpaths:** Running machinery in ways that damage it
- **Autonomous System Disruption:** Jamming communications or control signals to force emergency landings, shutdowns, or crashes

**Additive Manufacturing-Specific Examples:**
- Destructive toolpaths causing printer head crashes or collisions
- Overheating components by manipulating temperature controls
- Exhausting material supplies through wasteful operations
- Corrupting calibration causing repeated failed prints
- Filling disk space with malformed files
- Jamming material feed mechanisms
- Creating conditions that require emergency shutdown

**Impact Assessment:**
- Production halts and missed deadlines
- Equipment damage requiring expensive repairs
- Safety incidents from failed safety systems
- Financial losses from downtime
- Reputational damage

---

### 6. ELEVATION OF PRIVILEGE
**Violates:** Authorization

**Definition:** Exploitation of system vulnerabilities to gain unauthorized higher-level access rights beyond assigned permissions.

**Cyber-Only Examples:**
- **Software Vulnerability Exploitation:** Buffer overflows, race conditions
- **Password Attacks:** Brute force, credential stuffing, password cracking
- **Privilege Escalation Exploits:** Exploiting OS bugs to gain admin/root access
- **Session Hijacking:** Stealing authenticated sessions
- **Token Manipulation:** Modifying JWTs or access tokens
- **SQL Injection to Admin:** Using SQLi to gain DBA privileges
- **Exploiting Misconfigurations:** Leveraging overly permissive settings

**Physical-Only Examples:**
- **Physical Key Theft:** Stealing master keys or credentials
- **Unauthorized Entry:** Tailgating into restricted areas
- **Climbing/Bypassing:** Going over fences, through windows
- **Impersonation:** Posing as maintenance or emergency personnel
- **Lockpicking:** Defeating physical locks
- **Badge Duplication:** Cloning physical access badges

**Cyber-Physical Examples:**
- **Maintenance Port Exploitation:** Using physical access to install privileged software, bypassing normal authorization controls via direct hardware access
- **Badge + Software Attack:** Physical access card used with malware to escalate privileges
- **Firmware Manipulation via Physical Access:** Reflashing firmware from maintenance ports
- **Sensor Spoofing to Override Controls:** Faking emergency conditions to gain override access
- **Dual-Access Attacks:** Combining physical presence with cyber exploitation
- **Autonomous System Hijacking:** Exploiting physical access during maintenance or cyber vulnerabilities during operation to gain command authority over UAVs, UGVs, or UUVs

**Additive Manufacturing-Specific Examples:**
- Using physical access to printer maintenance port to install backdoor firmware
- Exploiting calibration mode to gain administrative control
- Using emergency override credentials to modify locked production settings
- Physical access to networked printer enabling pivot to broader network
- Maintenance account exploitation to modify locked design files

**Impact Assessment:**
- Complete system compromise
- Ability to perform any malicious action
- Long-term persistent access
- Potential for widespread damage across organization

---

### Threat Summary Table

| Threat | Violates | Cyber Example | Physical Example | Cyber-Physical Example |
|--------|----------|---------------|------------------|------------------------|
| **Spoofing** | Authenticity | Phishing email | Fake badge | GPS spoofing of UAV |
| **Tampering** | Integrity | Modifying CAD file | Contaminating material | Altering sensor via EMI |
| **Repudiation** | Non-Repudiation | Deleting logs | Destroying surveillance footage | Cross-domain log corruption |
| **Interception** | Containment | Network sniffing | Material theft | Acoustic side-channel attack |
| **Denial of Service** | Availability / Reliability | DDoS attack | Physical destruction | GPS jamming of autonomous system |
| **Elevation of Privilege** | Authorization | SQL injection | Stealing master key | Hijacking UAV command authority |

---

## Element-Threat Susceptibility Matrix

### STRIDE Susceptibility Matrix (Original)

In STRIDE, element susceptibility is assumed as follows:

| Element | S | T | R | I | D | E |
|---------|---|---|---|---|---|---|
| **Interactor** | ✓ | | ✓ | | | |
| **Data Flow** | | ✓ | | ✓ | ✓ | |
| **Data Store** | | ✓ | ✓ | ✓ | ✓ | |
| **Process** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

**STRIDE Assumptions:**
- **Interactors** assumed not susceptible to T, I, D
- **Data Flows** assumed not susceptible to S, R, E
- **Data Stores** assumed not susceptible to S, R, E
- **Processes** susceptible to all threats
- **Only Processes** susceptible to Elevation of Privilege

### CPSTRIDE Susceptibility Matrix (Expanded)

CPSTRIDE assumes **all elements are susceptible to all threats**:

| Element | S | T | R | I | D | E |
|---------|---|---|---|---|---|---|
| **Interactor (I)** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Trust Boundary (TB)** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Store (S)** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Flow (F)** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Process (P)** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Link (L)** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Device (D)** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

**Rationale for Broader Susceptibility:**
1. **Physical Dimensions:** Physical and cyber-physical elements introduce vulnerabilities not present in pure software
2. **Novel Attack Vectors:** CPS enable new attack types that violate STRIDE's assumptions
3. **Defense in Depth:** Assuming broader susceptibility encourages more thorough analysis
4. **Unknown Unknowns:** Conservative approach guards against unanticipated threats

**Examples Breaking STRIDE Assumptions:**

*Data Stores CAN be spoofed:*
- Counterfeit physical materials posing as genuine (spoofing a physical store)
- Substituted material cartridges with fake labeling

*Interactors CAN suffer Denial of Service:*
- Attacking supplier (physical interactor) to disrupt material delivery
- DDoS attack on cloud service provider (cyber interactor)

*Flows CAN be elevated:*
- Injecting privileged commands into data flows (SQL injection, command injection)
- Session hijacking: taking over authenticated data flows to gain elevated access
- Manipulating authentication tokens or credentials within data flows

---

## The CPSTRIDE Threat Modeling Process

CPSTRIDE follows STRIDE's four-step iterative process, with modifications to steps 1 and 2:

### Step 1: Create a Cyber-Physical Flow Diagram (CPFD)

**Objectives:**
- Decompose the system into relevant components
- Identify all cyber, physical, and cyber-physical elements
- Show interactions between elements
- Mark trust boundaries

**Activities:**
1. **Define System Scope:**
   - What's inside your system boundary?
   - What's outside (interactors)?
   - What level of detail is appropriate?

2. **Identify Elements:**
   - **Interactors:** External entities (users, suppliers, networks)
   - **Trust Boundaries:** Where privilege levels change
   - **Stores:** Data, materials, energy at rest
   - **Flows:** Data, materials, energy in motion
   - **Processes:** Transformations
   - **Links:** Communication paths, transport media
   - **Devices:** Enabling infrastructure

3. **Classify Each Element:**
   - Cyber (C): Purely informational
   - Physical (P): Purely material/energy
   - Cyber-Physical (CP): Integrated

4. **Connect Elements (Following Interconnection Rules):**
   
   **Flow Connections:**
   - Connect Stores ↔ Processes using Flows
   - Connect Processes ↔ Interactors using Flows
   - Connect Stores ↔ Interactors using Flows
   - Indicate directionality (arrows)
   
   **Link Connections:**
   - Connect Devices ↔ Devices using Links
   - Connect Devices ↔ Interactors using Links
   - Links enable/support Flows
   
   **Key Principle:** 
   - If you're modeling content moving (data/energy/material) → use Flow
   - If you're modeling infrastructure/medium → use Link
   
   **Common Pattern:** Device ← Link → Device, with Flows connecting Processes enabled by those Devices

5. **Review for Completeness:**
   - No magic sources or sinks
   - All important files, databases, materials represented
   - Trust boundaries clearly marked

**Deliverable:** CPFDs representing the system at appropriate detail levels (context diagram first, then detailed breakouts for complex subsystems)

---

### Step 2: Identify CPSTRIDE Threats

**Objectives:**
- Systematically consider all six threat categories
- Examine each CPFD element from multiple perspectives
- Generate comprehensive threat list

**Activities:**

1. **For Each Element in CPFD:**

2. **For Each CPSTRIDE Threat Category (S-T-R-I-D-E):**

3. **Consider Three Perspectives:**
   - **Subject:** Can this element perform the threat?
     - Example: Can Process X spoof identity of Process Y?
   - **Object/Target:** Can this element be victimized by the threat?
     - Example: Can Store X be tampered with?
   - **Instrument:** Can this element be used to threaten others?
     - Example: Can compromised Device X be used to intercept Flow Y?

4. **Use Prompting Questions:**
   - **Spoofing:** "Can the identity/authenticity of [element] be faked? If so, how?"
   - **Tampering:** "Can [element] be modified in unauthorized ways? If so, how?"
   - **Repudiation:** "Can actions involving [element] be denied plausibly? If so, how?"
   - **Interception:** "Can [element] be accessed/monitored without authorization? If so, how?"
   - **Denial of Service:** "Can [element] be made unavailable? If so, how?"
   - **Elevation of Privilege:** "Can [element] be exploited to gain higher privileges? If so, how?"

5. **Leverage Domain Knowledge:**
   - Consult attack pattern libraries (MITRE ATT&CK, CVE, CWE)
   - Review technology-specific vulnerabilities
   - Examine past security incidents in similar systems
   - Consider supply chain and insider threats

6. **Document Threats:** Description, affected element(s), category, potential impact, attack vector

**Deliverable:** Comprehensive threat list (use checklists and threat trees for consistent coverage)

---

### Step 3: Investigate Vulnerabilities

**Objective:** Determine how identified threats could be realized given the system's specific implementation

**Activities:**
1. Map threats to known vulnerabilities in technologies used
2. Assess exploitability of each vulnerability
3. Evaluate existing mitigations
4. Determine residual risk

**Deliverable:** Vulnerability assessment linking threats to implementation weaknesses

**Note:** CPSTRIDE specification focuses on Steps 1-2; Steps 3-4 follow standard security practices

---

### Step 4: Plan Mitigations

**Objective:** Design and implement controls to reduce risk to acceptable levels

**Activities:**
1. **Prioritize Threats:** Based on risk = likelihood × impact
2. **Select Mitigations:**
   - Eliminate: Remove vulnerable element
   - Mitigate: Reduce likelihood or impact
   - Transfer: Insurance, outsourcing
   - Accept: Acknowledge and document residual risk
3. **Design Controls:**
   - Technical: Encryption, access controls, hardening
   - Operational: Procedures, training, monitoring
   - Physical: Locks, cameras, guards
4. **Implement and Validate**
5. **Iterate:** Return to Step 1 with updated design

**Deliverable:** Mitigation plan and implemented security controls

---

### Iterative Refinement

Threat modeling is iterative:
- As design evolves, update CPFD and re-analyze
- New threats discovered → return to Step 2
- Mitigations change system → return to Step 1
- Continue until risk is acceptable

---

## Conclusion

CPSTRIDE extends STRIDE's proven threat modeling methodology to the cyber-physical domain, enabling security analysis of systems integrating digital and physical processes. Just as digital transformation lowered barriers for cyber adversaries, the proliferation of autonomous and unmanned systems (UAVs, UGVs, UUVs) is creating new cyber-physical attack surfaces accessible to nation-states, violent extremist organizations, and lone actors. By introducing the CPFD, expanding security properties and threats, and assuming broader element susceptibility, CPSTRIDE enables identification of threats that purely cyber-focused frameworks would miss.

**Key Takeaways:**

1. **CPFD is Essential:** Without proper representation of physical elements, threats to CPS cannot be modeled comprehensively

2. **Cyber ≠ Physical ≠ Cyber-Physical:** Each domain has unique characteristics and vulnerabilities requiring distinct analysis

3. **Assume Broad Susceptibility:** All elements should be considered for all threats to avoid blind spots

4. **Systematic Process:** Following the four-step process ensures thorough coverage

5. **Domain Expertise Required:** Effective CPS threat modeling requires understanding both cyber and physical domains

6. **Continuous Activity:** Threat modeling is not one-time but ongoing as systems and threats evolve

**Future Directions:**

While CPSTRIDE provides a solid foundation, areas for continued development include:
- Formalized mitigation catalogs for CPS threats
- Automated CPFD analysis tools
- Integration with CPS-specific vulnerability databases
- Quantitative risk assessment methodologies for CPS
- Cross-domain attack pattern libraries

By applying CPSTRIDE to cyber-physical systems like additive manufacturing facilities, industrial control systems, and IoT deployments, security professionals can identify and mitigate threats that would otherwise remain hidden, ultimately producing more resilient and secure systems.

---

*Document Version: 1.0*  
*Based on CPSTRIDE Specification by **redacted for anonymous submission***  
*STRIDE Framework by Microsoft Corporation*
