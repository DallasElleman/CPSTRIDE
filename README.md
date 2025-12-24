# CPSTRIDE: A Threat Modeling Framework for Cyber-Physical Systems

## Overview
CPSTRIDE extends the popular STRIDE threat modeling framework to address the unique security challenges of Cyber-Physical Systems (CPS). This framework introduces new threat categories and modeling abstractions specifically designed to capture the physical dimensionality and cyber-physical interactions that traditional STRIDE cannot adequately represent.

## Repository Organization
This repository is organized by conference/publication, with each conference receiving its own directory containing all associated materials. This structure supports:
- Clear separation of materials for different publications
- Easy addition of future conference applications of CPSTRIDE
- Organized archival of research artifacts by venue and date

## Anonymous Repository

For conference submissions requiring anonymous review, an anonymized version of this repository is available at:
**https://anonymous.4open.science/r/CPSTRIDE-CE67/**

The anonymized repository (ICCWS branch) contains only materials relevant to specific submissions with author identities redacted.

## Repository Contents

```
CPSTRIDE/
├── README.md                                    # Repository overview and documentation
├── CPFD-specification-v3.pdf                    # Cyber-Physical Flow Diagram specification
├── CPSTRIDE-specification-v3.md                 # CPSTRIDE framework specification (markdown)
├── CRITIS2025-CPSTRIDE-Additive-Manufacturing/  # CRITIS 2025 conference materials
│   ├── cpstride-critis-2025.pdf                 # Published CRITIS 2025 conference paper
│   ├── claude-3-7-threat-modeling-conversation.md # Complete human-AI collaboration dialogue
│   ├── llm-generated-cpstride-threat-matrix-output.csv # Threat analysis results
│   ├── sora-diagram-prompts.txt                 # Prompts used for diagram generation
│   └── MaterialsProvidedToLLM/                  # Reference materials provided to AI assistant
│       ├── am-cpfd.pdf                          # Additive Manufacturing CPFD
│       ├── am-dfd.pdf                           # Additive Manufacturing DFD
│       ├── claude-3-7-agent-prompt.md           # AI agent initialization prompt
│       ├── cpstride-spec.pdf                    # CPSTRIDE framework specification
│       ├── stride-spec.pdf                      # Original STRIDE specification (PDF)
│       ├── stride-spec.txt                      # Original STRIDE specification (text)
│       └── susceptibility-matrix-comparison.pdf # Cyber-Physical susceptibility matrix
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

### File Descriptions

#### CRITIS 2025 Conference Materials
All materials related to the CRITIS 2025 conference presentation are organized under `CRITIS2025-CPSTRIDE-Additive-Manufacturing/`:

#### Core Publication
- **`cpstride-critis-2025.pdf`** - The peer-reviewed conference paper presenting the CPSTRIDE framework, accepted and presented at CRITIS 2025 (Jönköping, Sweden, October 21-23, 2025)

#### Human-AI Collaboration Documentation
- **`claude-3-7-threat-modeling-conversation.md`** - Complete transcript of the human-AI collaborative threat modeling session
- **`llm-generated-cpstride-threat-matrix-output.csv`** - Structured output from AI-assisted threat identification and analysis
- **`sora-diagram-prompts.txt`** - Prompts used for generating visual diagrams and illustrations

#### Reference Materials
- **`MaterialsProvidedToLLM/`** - All supporting materials provided to the AI assistant for context and analysis
  - **Case Study Materials**: Additive manufacturing flow diagrams and data models
  - **Framework Specifications**: Both CPSTRIDE and original STRIDE documentation
  - **Analysis Tools**: Susceptibility matrices and comparison frameworks
  - **Agent Configuration**: Initialization prompts for AI collaboration

## Research Methodology

This research employed a novel **human-AI collaborative approach** for threat modeling:

1. **Framework Development**: Systematic extension of STRIDE for cyber-physical systems
2. **AI-Assisted Analysis**: Collaborative threat identification using Anthropic's Claude 3.7 Sonnet
3. **Human Validation**: Expert review and refinement of AI-generated threat scenarios
4. **Case Study Application**: Demonstration through additive manufacturing security analysis

## Key Contributions

1. **Framework Extension**: Systematic extension of STRIDE for CPS domains
2. **New Abstractions**: Introduction of Link and Device concepts for CPS modeling  
3. **Validation**: Demonstrated effectiveness through additive manufacturing case study
4. **AI Integration**: Novel methodology for LLM-assisted threat modeling workflows

## Transparency and Reproducibility

All materials in this repository support full transparency and reproducibility of the research:
- Complete AI collaboration transcripts
- All reference materials provided to the AI system
- Structured outputs and analysis results
- Configuration details for AI agent collaboration

This research demonstrates responsible AI collaboration in academic research with complete documentation of AI contributions and human oversight.
