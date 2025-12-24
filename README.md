# CPSTRIDE: A Threat Modeling Framework for Cyber-Physical Systems

## Overview
CPSTRIDE extends the popular STRIDE threat modeling framework to address the unique security challenges of Cyber-Physical Systems (CPS). This framework introduces new threat categories and modeling abstractions specifically designed to capture the physical dimensionality and cyber-physical interactions that traditional STRIDE cannot adequately represent.

This branch contains materials for ICCWS 2026 conference submission, demonstrating CPSTRIDE application to water treatment facility security with emphasis on emerging UAV/UUV threat vectors.

## Repository Contents

```
CPSTRIDE/
├── README.md                                    # Repository overview and documentation
├── CPFD-specification-v3.pdf                    # Cyber-Physical Flow Diagram specification
├── CPSTRIDE-specification-v3.md                 # CPSTRIDE framework specification (markdown)
└── ICCWS2026-CPSTRIDE-W-WWS-UAV-UUV/           # ICCWS 2026 materials
    ├── methodology.md                           # LLM-assisted threat modeling methodology
    └── conversations/                           # Iterative human-AI collaboration sessions
        ├── 01/ - Initial CPFD refinement and agent prompt development
        ├── 02/ - CPFD vs DFD differential element identification
        ├── 03/ - CPFD element enumeration for water treatment facility
        ├── 04/ - Minimal CPFD JSON schema development
        ├── 05/ - Water treatment facility CPFD v1 (JSON creation)
        ├── 06/ - Water treatment facility CPFD v2 (JSON refinement)
        ├── 07/ - CPSTRIDE specification refinement to v3
        ├── 08/ - Water treatment facility CPFD v3 (final JSON)
        ├── 09/ - Threat matrix creation (initial)
        └── 10/ - Threat matrix cleanup and validation
```

## Case Study: Water Treatment Facility Security

This research applies CPSTRIDE to critical water infrastructure, focusing on:

### System Scope
- **Domain**: Drinking water treatment facilities
- **Treatment Processes**: Coagulation, flocculation, sedimentation, filtration, disinfection
- **Control Systems**: SCADA, PLCs, RTUs, HMIs, industrial networks
- **Physical Infrastructure**: Intake structures, treatment basins, chemical dosing, distribution

### Emerging Threat Vectors
- **UAV (Unmanned Aerial Vehicle) Threats**:
  - Reconnaissance and surveillance
  - Chemical/biological contamination delivery
  - Explosive payload delivery
  - Cyber-intrusion device deployment

- **UUV (Unmanned Underwater Vehicle) Threats**:
  - Submerged infrastructure targeting
  - Intake structure compromise
  - Pipeline and valve manipulation
  - Direct water supply contamination

## Research Methodology

This research employs **LLM-assisted threat modeling** through iterative human-AI collaboration:

1. **Context Engineering**: Equipping Claude Sonnet 4.5 with CPSTRIDE framework expertise
2. **Iterative Refinement**: 10 conversation cycles refining CPFD and threat identification
3. **CPFD Development**: Comprehensive cyber-physical flow diagram for water treatment
4. **Threat Enumeration**: Systematic identification of UAV/UUV attack vectors across all CPFD elements
5. **Validation**: Expert review and refinement of LLM-generated threat scenarios

### Conversation Flow
The 10 documented conversations demonstrate progressive refinement:
- **Conversations 01-03**: Agent prompt development and CPFD element identification
- **Conversations 04-06**: JSON schema creation and CPFD data structure development
- **Conversations 07-08**: CPSTRIDE specification refinement and final CPFD
- **Conversations 09-10**: Threat matrix generation and validation

## Key Contributions

1. **Framework Application**: CPSTRIDE demonstration for water infrastructure security
2. **CPFD for W/WWS**: Comprehensive cyber-physical flow diagram for water treatment facilities
3. **Novel Threat Vectors**: Systematic enumeration of UAV/UUV threats to critical water infrastructure
4. **LLM Integration**: Demonstrated methodology for AI-assisted CPS threat modeling
5. **Reproducible Artifacts**: Complete conversation history, schemas, and threat matrices

## Transparency and Reproducibility

All materials support full transparency and reproducibility:
- Complete LLM collaboration transcripts (10 conversation sessions)
- CPFD specification and JSON schema
- Agent prompts and context engineering artifacts
- Iterative CPFD refinements (v1 through v3)
- Threat matrix outputs with validation notes

This research demonstrates responsible AI collaboration with complete documentation of LLM contributions and human oversight.
