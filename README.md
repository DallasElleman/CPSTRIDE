# CPSTRIDE: A Threat Modeling Framework for Cyber-Physical Systems

## Overview
CPSTRIDE extends the popular STRIDE threat modeling framework to address the unique security challenges of Cyber-Physical Systems (CPS). This framework introduces new threat categories and modeling abstractions specifically designed to capture the physical dimensionality and cyber-physical interactions that traditional STRIDE cannot adequately represent.

## Repository Contents

```
CPSTRIDE/
├── README.md                                           # This file - repository overview and documentation
├── cpstride-critis-2025.pdf                          # Published CRITIS 2025 conference paper
├── claude-3-7-threat-modeling-conversation.md        # Complete human-AI collaboration dialogue
├── llm-generated-cpstride-threat-matrix-output.csv   # Threat analysis results from AI collaboration
├── sora-diagram-prompts.txt                           # Prompts used for diagram generation
└── MaterialsProvidedToLLM/                           # Reference materials provided to AI assistant
    ├── am-cpfd.pdf                                    # Additive Manufacturing Cyber-Physical Flow Diagram
    ├── am-dfd.pdf                                     # Additive Manufacturing Data Flow Diagram  
    ├── claude-3-7-agent-prompt.md                    # AI agent initialization prompt
    ├── cpstride-spec.pdf                             # CPSTRIDE framework specification
    ├── stride-spec.pdf                               # Original STRIDE specification (PDF)
    ├── stride-spec.txt                               # Original STRIDE specification (text)
    └── susceptibility-matrix-comparison.pdf          # Cyber-Physical susceptibility analysis matrix
```

### File Descriptions

#### Core Publication
- **`cpstride-critis-2025.pdf`** - The peer-reviewed conference paper presenting the CPSTRIDE framework, accepted and presented at CRITIS 2025

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
