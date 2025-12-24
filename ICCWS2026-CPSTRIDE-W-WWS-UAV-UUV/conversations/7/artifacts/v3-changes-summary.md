# CPSTRIDE Specification v3 - Changes Summary

**Date:** 2025-12-23
**Updated by:** Claude Code (based on user requirements)
**Version:** v3.0 (from v2.0)

---

## Overview

CPSTRIDE Specification v3 updates the CPFD interconnection architecture to allow Flows to connect Devices. This change acknowledges the practical reality that many cyber-physical Devices (SCADA systems, PLCs, RTUs, sensors, actuators) serve as abstraction layers for the computational, sensing, or actuation Processes they perform.

---

## Key Changes

### 1. Flow Interconnection Rules (Section: CPSTRIDE vs. STRIDE, Item 5)

**v2.0 (Previous):**
```
- Flows interconnect: Stores ↔ Processes ↔ Interactors
- Links interconnect: Devices ↔ Interactors (and enable Flows)
```

**v3.0 (Updated):**
```
- Flows interconnect: Stores ↔ Processes ↔ Interactors ↔ Devices
- Links interconnect: Devices ↔ Interactors (and enable Flows)
```

---

### 2. CPFD Interconnection Architecture (Section 6)

**Flow Interconnections - Updated Rationale:**

**v2.0:**
> "Flows represent content in motion (data/energy/material) that is transformed by Processes, held in Stores, or exchanged with Interactors"

**v3.0:**
> "Flows represent content in motion (data/energy/material) that is transformed by Processes, held in Stores, exchanged with Interactors, or processed by Devices. Many cyber-physical Devices (PLCs, RTUs, SCADA systems, sensors, actuators) serve as abstraction layers for the computational or sensing/actuation Processes they perform. Allowing Flows to connect Devices acknowledges that threat modelers may not always decompose every Device into its constituent Processes, particularly when the Device functions as a cohesive unit."

**Device Role - Updated:**

Added to v3.0:
- Devices **may also connect via Flows** when they act as abstraction layers for computational, sensing, or actuation processes
- **Modeling Guidance:**
  - Use Device-to-Device Flows when the Device performs computation, sensing, or actuation that you're not decomposing into separate Processes
  - Use Process elements when you need to explicitly model the transformation logic separate from the enabling hardware
  - Both approaches are valid; choose based on the level of detail needed for threat analysis

---

### 3. Valid Connection Patterns

**Added to v3.0:**
```
Device → Flow → Device (when Device abstracts a Process)
Device → Flow → Process
Device → Flow → Store
Device → Flow → Interactor
```

**Connection Pattern Guidance (New):**
```
Process-centric modeling (explicit Processes):
  [Device A] ← Link → [Device B]
       ↓ enables          ↓ enables
  [Process A] → Flow → [Process B]

Device-centric modeling (abstracted Processes):
  [Device A] ← Link → [Device B]  (infrastructure)
  [Device A] → Flow → [Device B]  (data/control/material)

Both patterns are valid. Choose based on:
- Level of abstraction needed
- Whether Process details matter for threat analysis
- Complexity vs. clarity tradeoffs
```

---

### 4. Illustrative Examples

**Added SCADA System Examples:**

**Example 1 - SCADA System (Device-centric):**
```
[SCADA Computer] ← Link: Ethernet → [PLC Controller]
      (CPD14)           (CPL)             (CPD3)
          ↓              enables              ↓
          └─── Flow: Control Commands ───────┘
                       (CPF)
```

**Example 2 - SCADA System (Process-centric):**
```
[SCADA Computer] ← Link: Ethernet → [PLC Controller]
      (CPD14)           (CPL)             (CPD3)
         ↓ enables                          ↓ enables
         |                                  |
[Control Process] → Flow: Commands → [Actuation Process]
      (CPP)              (CPF)              (CPP)
```

---

### 5. Flow Element Specification (Section 4)

**Updated Connectivity:**

**v2.0:**
```
- Connects: Store ↔ Process ↔ Interactor
- Does NOT directly connect: Devices
```

**v3.0:**
```
- Connects: Store ↔ Process ↔ Interactor ↔ Device
- Enabled by: Links (which provide the path, channel, or medium)
```

**Added Modeling Guidance for Device Flows:**
- Devices that perform computation, sensing, or actuation may connect via Flows when you're treating the Device as an abstraction layer
- Examples: SCADA systems, PLCs, RTUs, sensors, actuators, smart devices
- If you need to model the internal transformation logic, decompose the Device and use explicit Process elements instead

**Added Cyber-Physical Flow Examples:**
- SCADA/ICS Communications: SCADA computer exchanging data with PLCs, RTUs, and field devices

---

### 6. Device Element Specification (Section 7)

**Updated Connectivity:**

**v2.0:**
```
- Via Links: Connects to other Devices and Interactors
- Does NOT connect via Flows (Flows represent content, not infrastructure)
- Valid Example: [Workstation] (CPD) ← Link → [Network Switch] (CPD)
- Invalid Example: [Workstation] (CPD) → Flow → [Server] (CPD)
```

**v3.0:**
```
- Via Links: Connects to other Devices and Interactors
- Via Flows: May connect to Processes, Stores, Interactors, and other Devices
- Modeling Guidance:
  - Use Device-to-Device Links to represent infrastructure (cables, pipes, wireless channels)
  - Use Device-to-Device Flows when the Device abstracts computational, sensing, or actuation processes
  - Many cyber-physical Devices (SCADA systems, PLCs, RTUs, sensors, actuators) combine hardware with embedded logic
- Valid Examples:
  - [Workstation] (CPD) ← Link → [Network Switch] (CPD) (infrastructure)
  - [SCADA Computer] (CPD) → Flow: Commands → [PLC] (CPD) (abstracted process)
  - [Workstation] (CPD) enables [Data Analysis Process] (CP) (explicit process)
```

**Added Abstraction Decision Guidance:**

Many cyber-physical Devices perform both computation/sensing/actuation AND physical functions. You may model them as:
1. **Device with Flows:** Treat the Device as an abstraction layer (simpler, appropriate when internal logic doesn't matter for threats)
2. **Device + Process:** Explicitly model the Device and the Process(es) it enables (more detailed, appropriate when transformation logic is threat-relevant)

**Updated Relationship to Other Elements:**
- Added: **Devices MAY CONNECT via Flows:** SCADA (CPD) sending commands to PLC (CPD) when not decomposing into explicit Processes

---

### 7. Modeling Best Practices (New Item #6)

**Added to v3.0:**

6. **Choose Appropriate Abstraction:**
   - Use Device-to-Device Flows when Devices abstract processes you're not decomposing
   - Use explicit Process elements when transformation logic is threat-relevant
   - Document your abstraction choices for consistency

---

### 8. Step 1: Create a CPFD (Connection Rules)

**Updated Flow Connections:**

**v2.0:**
```
- Connect Stores ↔ Processes using Flows
- Connect Processes ↔ Interactors using Flows
- Connect Stores ↔ Interactors using Flows
- Indicate directionality (arrows)
```

**v3.0:**
```
- Connect Stores ↔ Processes using Flows
- Connect Processes ↔ Interactors using Flows
- Connect Stores ↔ Interactors using Flows
- Connect Devices ↔ Processes using Flows (when Device abstracts a Process)
- Connect Devices ↔ Devices using Flows (when modeling abstracted computation/sensing/actuation)
- Indicate directionality (arrows)
```

**Updated Key Principles:**

Added to v3.0:
- If a Device performs computation/sensing/actuation you're not decomposing → Device-Flow connections are valid
- If transformation logic matters for threat analysis → use explicit Process elements

**Updated Common Patterns:**

Added to v3.0:
```
- Device ← Link → Device (infrastructure)
- Device → Flow → Device (abstracted process)
- Device → Flow → Process (explicit process enabled by device)
- Device enables Process; Process → Flow → another Process
```

---

### 9. Interactor Element Specification (Section 1)

**Updated Connectivity:**

**v2.0:**
```
- Via Flows: Connects to Stores, Processes, and other Interactors
```

**v3.0:**
```
- Via Flows: Connects to Stores, Processes, Devices, and other Interactors
```

---

### 10. Store Element Specification (Section 3)

**Updated Connectivity:**

**v2.0:**
```
- Via Flows: Connects to Processes, Interactors, and other Stores
```

**v3.0:**
```
- Via Flows: Connects to Processes, Interactors, Devices, and other Stores
```

---

### 11. Process Element Specification (Section 5)

**Updated Connectivity:**

**v2.0:**
```
- Via Flows: Connects to Stores, Interactors, and other Processes
```

**v3.0:**
```
- Via Flows: Connects to Stores, Interactors, Devices, and other Processes
```

**Added Modeling Considerations:**

**v3.0:**
- **Process vs Device Decision:** If the transformation logic matters for threat analysis, model it as a Process. If the Device functions as an abstraction layer and you don't need to decompose it, use Device-to-Device Flows.

---

### 12. Conclusion Section

**Added to Key Takeaways (v3.0):**

7. **Flexible Abstraction:** CPFD allows both Device-centric (abstracted) and Process-centric (explicit) modeling approaches—choose based on threat analysis needs

**Added to Future Directions (v3.0):**
- Guidance on abstraction level selection for different system types

---

### 13. Revision History

**Added:**
```
- v3.0 (2025-12-23): Updated Flow interconnection rules to allow Flows to connect Devices,
  acknowledging that cyber-physical Devices often serve as abstraction layers for computational,
  sensing, and actuation processes. Added guidance on Device-centric vs Process-centric modeling
  approaches.
```

---

## Rationale for Changes

### Problem Identified

The v2.0 specification prohibited Flows from connecting Devices, creating a modeling challenge for SCADA/ICS systems where:
- RTU sensors (Devices) collect and transmit data
- PLC controllers (Devices) receive commands and execute them
- SCADA computers (Devices) aggregate data and issue commands
- These Devices communicate with each other over networks

Under v2.0, modelers faced two unsatisfactory options:
1. **Violate the specification** by showing Device-Device flows (which accurately reflects system architecture)
2. **Decompose every Device** into explicit Processes (which creates overly complex diagrams)

### Solution in v3.0

v3.0 acknowledges that cyber-physical Devices often serve as **abstraction layers** for the Processes they perform. The specification now:
1. **Permits Device-Device Flows** when modeling abstracted computation/sensing/actuation
2. **Provides guidance** on when to use Device-centric vs Process-centric modeling
3. **Maintains backward compatibility** - Process-centric modeling (v2.0 approach) remains valid
4. **Adds flexibility** - modelers choose abstraction level based on threat analysis needs

### Benefits

1. **Practical:** Aligns specification with real-world SCADA/ICS architectures
2. **Flexible:** Supports both high-level (Device-centric) and detailed (Process-centric) modeling
3. **Clear:** Provides explicit guidance on abstraction decisions
4. **Backward compatible:** Existing v2.0-compliant models remain valid
5. **Comprehensive:** Enables accurate threat modeling without artificial constraints

---

## Impact on Existing CPFDs

### Existing v2.0 CPFDs

**Status:** Remain fully compliant with v3.0

Process-centric models that decompose Devices into explicit Processes are still valid and encouraged when transformation logic is threat-relevant.

### Models that Violated v2.0

**Status:** May now be compliant with v3.0

Device-centric models that connected Devices via Flows (previously violating v2.0) may now be valid under v3.0, provided:
- The Devices abstract computational, sensing, or actuation processes
- The abstraction level is documented
- The model is consistent in its abstraction choices

### Recommended Actions

1. **Review existing CPFDs** for Device-Device Flows that were modeled in violation of v2.0
2. **Document abstraction decisions** - clarify whether Devices abstract Processes or if explicit Processes are needed
3. **Update modeling documentation** to reference v3.0 guidance on Device-centric vs Process-centric approaches
4. **Consider refinement** - some Device-Device Flows may benefit from decomposition into explicit Processes if transformation logic matters for threat analysis

---

## Examples of Valid v3.0 Modeling Approaches

### SCADA System - Both Approaches Valid

**Device-centric (simpler):**
```
[SCADA] ← Link: Network → [PLC]
    ↓         enables        ↓
    └── Flow: Commands ─────┘
```
✓ Valid when internal command processing logic doesn't matter for threat analysis

**Process-centric (more detailed):**
```
[SCADA Device] ← Link: Network → [PLC Device]
    ↓ enables                      ↓ enables
    |                              |
[Command Gen] ── Flow ──→ [Command Execution]
  (Process)                  (Process)
```
✓ Valid when command transformation logic is threat-relevant

### Water Treatment Facility

**Device-centric:**
```
[RTU Sensors] → Flow: Telemetry → [SCADA Computer]
[SCADA Computer] → Flow: Control → [PLC Actuators]
```
✓ Valid for high-level threat model

**Process-centric:**
```
[RTU] enables [Sensor Reading Process] → Flow → [Data Aggregation Process]
[Control Logic Process] → Flow → [Actuation Process] ← enabled by [PLC]
```
✓ Valid for detailed threat model focused on process logic

---

## Conclusion

CPSTRIDE v3.0 resolves a significant practical limitation in v2.0 by allowing Flows to connect Devices when those Devices serve as abstraction layers for computational, sensing, or actuation processes. This change:
- Maintains the rigor of the CPFD specification
- Provides flexibility for different modeling needs
- Aligns the specification with real-world cyber-physical system architectures
- Supports threat modeling at multiple levels of abstraction

The update is backward compatible—existing v2.0 models remain valid, while new models gain the flexibility to choose the most appropriate abstraction level for their threat analysis objectives.
