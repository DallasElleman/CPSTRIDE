Our methodology for LLM-assisted CPSTRIDE analysis is informed by principles and practices of context engineering. Mei et al. note in their 2025 survey the fundamental asymmetry that exists between the remarkable proficiency of LLMs in understanding complex contexts and their pronounced limitations in generating equally sophisticated, long-form outputs. They emphasize that the performance of Large Language Models (LLMs) is in large part determined by the contextual information provided during inference, and that the quality of an LLMs outputs can be improved considerably by improving the quality of its inputs, i.e., its context. Further, they observe that context length and coherence are critical factors in determining the quality of LLM outputs, and that overly long context inputs as well as contradictions in the context can lead to inconsistent or incorrect outputs.

Through 10 rounds of conversation with Claude 4.5 Sonnet, using Anthropic's Claude Desktop and Claude Code applications, we systematically and iteratively refine the context provided to the LLM and progressively mitigate hallucinations and inaccuracies in output through the identification and resolution of contradictory and incoherent contextual inputs. The methodology follows a deliberate pattern: conversations 1-4 establish the foundation by refining visual diagrams, enumerating elements, and developing JSON schemas; conversations 5-6 attempt to apply these schemas but reveal critical specification violations; conversation 7 performs deep root cause analysis that leads to fundamental specification improvements; and conversations 8-10 successfully apply the refined specifications to produce accurate system models and comprehensive threat matrices. Each round of conversation produces progressively more detailed, concise, and coherent outputs, which are then fed into a clean context window during the next round of conversation.

The most significant challenge emerged during conversations 5-7, when two independent attempts to generate JSON representations of the drinking water treatment facility CPFD both produced errors—6 violations in version 1 and 21 violations in version 2. Initial analysis suggested these were LLM generation failures, but deeper investigation revealed that Claude 4.5 Sonnet had faithfully reproduced specification violations present in the source materials themselves. The root cause was identified as a fundamental mismatch between the CPSTRIDE v2.0 specification and the reality of SCADA/ICS architectures: the specification prohibited Flows from connecting Devices directly, yet SCADA systems inherently require Device-to-Device communications where devices (RTUs, PLCs, HMI systems) serve as abstraction layers for computational, sensing, and actuation processes. This insight led to a critical refinement of the CPSTRIDE specification to v3.0, which now explicitly allows Flows to connect Devices when those Devices abstract Processes, and updates the Device definition to reflect this dual role as both enabler and abstraction layer.

The ultimate results of 10 rounds of conversation with Claude 4.5 Sonnet demonstrate the value of iterative context refinement and specification-aware validation. The methodology produced: (1) updated CPSTRIDE and CPFD specification documents (v3.0) that provide a more coherent and realistic threat modeling framework for cyber-physical systems, particularly those involving SCADA/ICS architectures; (2) progressively refined drinking water treatment facility cyber-physical flow diagrams (v1 through v4) that accurately capture the complex interactions between physical and digital systems; (3) specification-compliant JSON representations of the facility's 91+ elements and their relationships, enabling machine-readable threat modeling and automated analysis; and (4) a comprehensive CPSTRIDE threat matrix documenting realistic threats from adversarial UAVs and UUVs to the 53 system elements (58% of total) that would be completely invisible in traditional STRIDE analysis. Importantly, the iterative process revealed that LLM errors often propagate from inconsistencies in source materials rather than model limitations, underscoring the need for specification-aware validation tools and the value of LLMs in identifying contradictions between formal specifications and practical system implementations.

We begin Conversation 1 by providing 3 sources of context: an initial CPSTRIDE specification document, an initial cyber-physical flow diagram (CPFD) for a representative drinking water treatment facility, and background information related to the water treatment processes and potential UAV and UUV threats faced by critical infrastructure. During this conversation we direct Claude to modify an Additive Manufacturing CPSTRIDE threat modeling prompt for use in a Drinking Water Treatment Facility context; this prompt is fed into Conversation 2. 


# Conversation 1: Initial Prompt and CPFD Refinement

This conversation was held with Claude Sonnet 4.5 using Anthropic's 'Claude Desktop' application in November / December 2025. Claude 4.5 Sonnet was given the new agent prompt and provided with two documents:

- CPSTRIDE-specification.md
- dwtf-cpfd-v1.pdf (image)

Claude 4.5 Sonnet was provided with two additional resources via copy/paste into the conversation input:

- ICCWS-context.md
- claude-3-7-agent-prompt-CPSTRIDE-am.md

## Purpose of Conversation 1

- Test the model's understanding of the CPSTRIDE specification and CPFD
- Refine a previous prompt (which related to CPSTRIDE threat modeling in an additive manufacturing context) for CPSTRIDE threat modeling within the context of water treatment facilities and UAV / UUV threats.
- Test the unprompted model's ability to help refine the initial CPFD by identifying mislabeled or redundantly-named elements in the CPFD, as well as any missing elements that should be included.

## Results of Conversation 1

- Claude 4.5 Sonnet demonstrated high understanding of the CPSTRIDE specification and CPFD
- Claude 4.5 Sonnet generated a refined agent prompt, which was then modified by the human research team as follows:
  - Removed hallucinations regarding Threat Landscape Awareness, specifically an unrelated incident: "Aliquippa PA attack"
  - Removed irrelevant information about COTS affordability but retained operating depths information in UUV Operational Characteristics section: "Operating depths: 100-300 meters for affordable models ($2,000-$10,000)"
- The edited agent prompt was then given to Claude 4.5 Sonnet in its 'Claude Desktop' Project Instructions for subsequent conversations, and can be found in each of the other LLM/conversations/materials-provided/ folders.
- Claude 4.5 Sonnet identified several mislabeling and name redundancy issues in the CPFD, which were acted upon to refine dwtf-cpfd-v1.pdf and produce dwtf-cpfd-v2.pdf, which was then included in the project files for Conversation 2.

The contents of Conversation 1 can be found in /LLM/conversations/1/conversation-1-initial-prompt-cpfd-refinement.md

# Conversation 2: Differential CPFD / DFD element identification

This conversation was held with Claude Sonnet 4.5 using Anthropic's 'Claude Desktop' application in November / December 2025. Claude 4.5 Sonnet was given the new agent prompt and provided with two documents:

- CPSTRIDE-specification.md
- dwtf-cpfd-v2.pdf (image)

## Purpose of Conversation 2

- Test the newly-promptedLLM's behavior and understanding of the visual Cyber-Physical Flow Diagram and the CPSTRIDE framework specification,
- Test the newly-prompted LLM's ability to identify elements in the WWS CPFD for which there would be no corresponding elements in a STRIDE DFD of the same system,
- Test the newly-prompted LLM's ability to identify potentially mislabeled or redundantly-named elements in the CPFD, as well as any missing elements that should be included. The conversation includes two rounds of input from the User and response from Claude.

## Results of Conversation 2

- Claude 4.5 Sonnet demonstrated a high understanding of the CPSTRIDE specification and dwtf-cpfd-v2.pdf. 
- Claude 4.5 Sonnet identified several elements that would have no corresponding elements in a traditional STRIDE DFD of the same system. Claude's response was analyzed and reviewed by the researchers to ensure accuracy and clarity. The results of this analysis are as follows:

1. Claude accurately identified 6/6 Link and 18/18 Device elements in the CPFD. 
2. Claude accurately identified 10/10 physical interactors (PI), trust boundaries (PTB), and stores (PS) in the CPFD.
3. Claude accurately identified 19/21 physical flows (PF). However, the two flows that Claude missed were found to be mislabeled (redundantly named) in the CPFD: PF2: Mechanical and PF18: Plant Waste.
4. Claude accurately identified 27/27 cyber-physical interactors (CPI), trust boundaries, flows, and processes in the CPFD.
5. Claude accurately identified 6/6 cyber-only interactors (CI), devices (CD), and flows (CF) in the CPFD. Claude further suggested that a STRIDE analysis might capture several of the system elements as cyber-only: human operators as External Entities (but only with regard to their cyber interactions), a SCADA computer (conflated with its processes), SCADA systems as a single process, and configuration databases or logs as cyber stores.
6. Claude correctly summarized that a STRIDE analysis would miss roughly 89% of the system's elements - approximately 81 out of 91 total elements, including all physical water treatment processes, physical infrastructure, ICS/OT devices, and materials, all cyber-physical integrations, and all physical security boundaries.
7. When the human researcher checked Claude's responses against the CPFD, they identified **missing Link elements** in the WWS CPFD for several flows in the CPFD, as well as two mislabeled (redundantly named) elements. This led to a further interaction wherein Claude was prompted to identify all potentially mislabeled or redundantly-named elements in the CPFD, as well as any missing elements that should be included.

- Claude 4.5 Sonnet identified several additional opportunities to refine dwtf-cpfd-v2.pdf including mislabeled and redundantly-named elements.
1. Claude identified an additional duplicate element missed during the first pass: two elements labeled "CPD11" - CPD11: SCADA Computer / HMI (in the control area) and CPD11: PLC Actuators (Feed pumps, dosing valves) (near the post-treatment process) - and correctly suggested that one should be named CPD14 to maintain unique identifiers.
2. Claude correctly identified the PF2 duplicate, and gave detailed advice for renaming to maintain unique identifiers. However, Claude missed the duplicate PF18 Treated Water / Plant Waste issue.
3. Claude identified a potential Link / Device conflation in the CPFD related to CD1: Internet Link / Firewall
4. Claude suggested several additional improvements for the CPFD, including
- adding chemical storage container Devices for physical stores PS1-PS5,
- adding cyber links such as communication protocols and network infrastructure,
- adding a backup power system, which the water treatment plant would undoubtedly have,
- renaming each of the generically-named "Mechanical" flows for clarification,
- specifying PS4's chemical type,
- adding an engineering workstation and a data historian / database,
- differentiating all 3 "Treated Water" flows for clarity,
- specifying "Telemetry" and "SCADA" flow directions,
- adding physical security devices, surveillance system components, supply chain interactors, HVAC systems, fire suppression, sample collection points, and more detailed waste flows.

Duplicated names were corrected for CPD11, PF2, and PF18 in the CPFD v2, and Claude 4.5 Sonnet was provided with an updated copy of the CPFD for Conversation 3 (dwtf-cpfd-v3.pdf)

The contents of Conversation 2 can be found in LLM/conversations/2/conversation-2-cpfd-dfd-differential-element-identification.md

# Conversation 3: CPFD Element Enumeration

This conversation was held with Claude Sonnet 4.5 using Anthropic's 'Claude Desktop' application in November / December 2025. Claude 4.5 Sonnet was given the claude-4-5-agent-prompt-CPSTRIDE-WWS.md  agent prompt and provided with two documents:

- CPSTRIDE-specification-v1.md
- dwtf-cpfd-v3.pdf (image)

## Purpose of Conversation 3
- Test the LLM's ability to create a structured list of all elements in the CPFD.
- Test the LLM's understanding of the elements in the CPFD which would not be represented in a STRIDE DFD.
- Create a numbered list of all elements in the CPFD which would not be represented in a STRIDE DFD.
- Use this list to create a minimal JSON representation of the CPFD elements and their immediate connections, in preparation for CPSTRIDE threat modeling.

## Results of Conversation 3
- Claude 4.5 Sonnet enumerated all elements individually with 100% accuracy.
- Claude accurately identified that 38 of the CPFD's 91 elements would be represented as cyber-Interactors, Trust Boundaries, Stores, Flows, and Processes in a conventional STRIDE DFD, and that 53 of 91 elements (58%) representing physical infrastructure, materials, and energy would be completely invisible in a traditional STRIDE DFD.

The contents of Conversation 3 can be found in LLM/conversations/3/conversation-3-cpfd-element-enumeration.md

# Conversation 4: Minimal CPFD JSON Schema

This conversation was held with Claude Sonnet 4.5 using Anthropic's 'Claude Desktop' application in November / December 2025. Claude 4.5 Sonnet was given the claude-4-5-agent-prompt-CPSTRIDE-WWS.md  agent prompt and provided with two documents:

- CPSTRIDE-specification-v2.md
- dwtf-cpfd-v3.pdf (image)

## Purpose of Conversation 4
- Draft a minimal CPFD JSON schema that captures essential metadata and relationships for each element type.
- Generate sample CPFD JSON documents and validate them against the CPFD JSON schema.

## Results of Conversation 4
- Claude 4.5 Sonnet helped draft a minimal JSON schema for each type of CPFD element.
- Claude 4.5 Sonnet generated sample JSON documents, which the human research then successfully validated against the CPFD JSON schema.

The contents of Conversation 4 can be found in LLM/conversations/4/conversation-4-minimal-cpfd-json-schema.md

# Conversation 5: DWTF CPFD JSON V1 Creation

This conversation was held with Claude Sonnet 4.5 using Anthropic's 'Claude Desktop' application in November / December 2025. Claude 4.5 Sonnet was given the claude-4-5-agent-prompt-CPSTRIDE-WWS.md agent prompt and provided with five documents:

- dwtf-cpfd-v3.pdf (image)
- dwtf-cpfd-list.md
- CPSTRIDE_specification-v2.md
- cpfd-schema.json
- CPFD_specification-v2.pdf (image)

## Purpose of Conversation 5
- Produce a JSON document that captures essential metadata and relationships for each element in the Water Treatment Facility (WTF) CPFD.
- Apply the minimal JSON schema developed in Conversation 4 to create a machine-readable representation of the DWTF CPFD.

## Results of Conversation 5
- Claude 4.5 Sonnet produced dwtf-cpfd-v1.json with comprehensive coverage of 91 total elements (8 Interactors, 3 Trust Boundaries, 5 Stores, 7 Processes, 14 Devices, 48 Flows, 6 Links).
- The JSON document captured the complete treatment process flow chain and SCADA architecture with bidirectional communications.
- All relationships between elements (flow connectivity, device enablement, trust boundary crossings) were properly mapped.
- However, errors were identified in this version that would be analyzed in subsequent conversations.

The contents of Conversation 5 can be found in LLM/conversations/5/conversation-5-dwtf-cpfd-json-v1-creation.md

# Conversation 6: DWTF CPFD JSON V2 Creation

This conversation was held with Claude Sonnet 4.5 using Anthropic's 'Claude Desktop' application in November / December 2025. Claude 4.5 Sonnet was given the claude-4-5-agent-prompt-CPSTRIDE-WWS.md agent prompt and provided with five documents:

- dwtf-cpfd-v3.pdf (image)
- dwtf-cpfd-list.md
- CPSTRIDE_specification-v2.md
- cpfd-schema.json
- CPFD_specification-v2.pdf (image)

## Purpose of Conversation 6
- Produce a second version of the JSON document that captures essential metadata and relationships for each element in the Water Treatment Facility (WTF) CPFD.
- Attempt to address potential issues from the first version through a fresh generation.

## Results of Conversation 6
- Claude 4.5 Sonnet produced dwtf-cpfd-v2.json with all 91 elements properly classified by domain.
- The JSON included proper domain classification, detailed descriptions, complete relationship mappings, and directional flow specifications.
- Each element type was comprehensively modeled (8 Interactors, 3 Trust Boundaries, 5 Physical Stores, 7 Cyber-Physical Processes, 21 Devices, 48 Flows, 6 Physical Links).
- However, errors were identified in this version as well, requiring deeper analysis of root causes.

The contents of Conversation 6 can be found in LLM/conversations/6/conversation-6-dwtf-cpfd-json-v2.md

# Conversation 7: CPSTRIDE Specification Refinement

This conversation was held with Claude Sonnet 4.5 using Anthropic's 'Claude Code' application in November / December 2025. Claude 4.5 Sonnet was provided with a minimal prompt and the following documents:

- dwtf-cpfd-list.md
- CPFD_specification-v2.pdf (image)
- CPSTRIDE_specification-v2.md
- claude-4-5-agent-prompt-CPSTRIDE-WWS.md
- cpfd-schema.json
- dwtf-cpfd-v3.pdf (image)
- dwtf-cpfd-v1.json
- dwtf-cpfd-v2.json

## Purpose of Conversation 7
- Compare the dwtf-cpfd-v1.json and dwtf-cpfd-v2.json documents to determine root causes of the mistakes and differences between them.
- Resolve the inconsistencies between the CPSTRIDE specification documents and the WTF CPFD.
- Identify whether errors originated from the JSON generation or from the source materials themselves.

## Results of Conversation 7
- Claude 4.5 Sonnet identified critical errors and inconsistencies in both JSON versions (6 errors in V1, 21 errors in V2).
- Root cause analysis revealed that the source PDF diagram (dwtf-cpfd-v3.pdf) violated the CPFD specification in fundamental ways, particularly regarding SCADA communications connecting Devices directly via Flows.
- The core problem identified: CPSTRIDE specification v2.0 prohibited Flows from connecting Devices, but SCADA/ICS systems inherently require Device-to-Device communications where Devices serve as abstraction layers for Processes.
- CPSTRIDE-specification.md was updated to v3.0 to allow Flows to connect Devices when those Devices serve as abstraction layers for computational, sensing, or actuation Processes.
- CPFD-specification.pdf Device definition was updated to: "An instantiation of computational capability and/or physical functionality that enables or abstracts Processes and Stores; a virtually- and/or physically-embodied enabler of Processes and/or Storage in a cyber-physical system."
- Two detailed analysis reports were produced documenting the errors and their root causes.

The contents of Conversation 7 can be found in LLM/conversations/7/conversation-7-cpstride-spec-refinement.md

# Conversation 8: DWTF CPFD JSON V3 Creation

This conversation was held with Claude Sonnet 4.5 using Anthropic's 'Claude Desktop' application in December 2025. Claude 4.5 Sonnet was given the claude-4-5-agent-prompt-CPSTRIDE-WWS-v2.md agent prompt and provided with the following documents:

- dwtf-cpfd-v4.pdf (image)
- dwtf-cpfd-list.md
- CPSTRIDE-specification-v3.md
- cpfd-schema.json
- CPFD-specification-v3.pdf (image)

## Purpose of Conversation 8
- Create a JSON document for the DWTF CPFD that complies with the updated CPSTRIDE specification v3.0.
- Apply the new specification allowing Flows to connect Devices (as abstraction layers for Processes).
- Model the DWTF based on the updated dwtf-cpfd-v4.pdf diagram.

## Results of Conversation 8
- Claude 4.5 Sonnet produced dwtf-cpfd-v3.json, a comprehensive and specification-compliant JSON representation with 91+ elements.
- The JSON document properly implemented v3.0 specification changes, particularly Device-Flow-Device connections for SCADA telemetry and control paths.
- SCADA architecture was properly modeled with telemetry flows from RTU sensors to SCADA computer and control flows from SCADA computer to PLC actuators.
- Human operators were modeled as Cyber-Physical Interactors with proper flow connections to SCADA systems.
- The device-centric modeling approach successfully abstracted internal computational/sensing/actuation Processes within SCADA components.
- All relationship mappings (flow connectivity, device enablement, trust boundary crossings, bi-directional communications) were accurately represented.

The contents of Conversation 8 can be found in LLM/conversations/8/conversation-8-dwtf-cpfd-json-v3.md

# Conversation 9: Threat Matrix Creation

This conversation was held with Claude Sonnet 4.5 using Anthropic's 'Claude Desktop' application in November / December 2025. Claude 4.5 Sonnet was prompted with claude-4-5-agent-prompt-CPSTRIDE-WWS-v2.md and provided with the following documents:

- dwtf-cpfd-only.md
- CPFD_specification-v3.pdf (image)
- CPSTRIDE_specification-v3.md
- cpfd-schema.json
- dwtf-cpfd-v3.pdf (image)

## Purpose of Conversation 9
- Create an initial CPSTRIDE threat identification matrix for the WTF CPFD.
- Focus exclusively on elements identified in the dwtf-cpfd-only.md document, which captures the 53 elements (58% of total) that would not be present in a conventional STRIDE DFD.
- Identify realistic threats from adversarial UAVs and UUVs across all CPSTRIDE threat categories (Spoofing, Tampering, Repudiation, Interception, Denial of Service, Elevation of Privilege).

## Results of Conversation 9
- Claude 4.5 Sonnet created threat-matrix-table-v1.md, an extensive threat identification matrix.
- The matrix was formatted as a readable table with rows representing CPFD elements and columns representing CPSTRIDE threat categories.
- However, the threat matrix included additional elements beyond those specified in the dwtf-cpfd-only.md document, requiring cleanup in Conversation 10.

The contents of Conversation 9 can be found in LLM/conversations/9/conversation-9-threat-matrix-creation.md

# Conversation 10: Threat Matrix Cleanup

This conversation was held with Claude Sonnet 4.5 using Anthropic's 'Claude Code' application in November / December 2025. Claude 4.5 Sonnet was provided with a minimal prompt and the following documents:

- dwtf-cpfd-only.md
- threat-matrix-table-v1.md

## Purpose of Conversation 10
- Remove rows from the threat matrix table that are not indicated by the CPFD Only list of elements.
- Ensure the final threat matrix contains exactly the 53 elements that differentiate CPSTRIDE from traditional STRIDE analysis.

## Results of Conversation 10
- Claude 4.5 Sonnet successfully removed extraneous elements from threat-matrix-table-v1.md and produced threat-matrix-table-v2.md.
- Entire sections deleted: Cyber-Physical Devices (RTU Sensors - 6 elements), Cyber-Physical Devices (PLC Actuators - 6 elements), Cyber Devices & Interactors (3 elements), Human Interactors (2 elements), and Cyber Flows/Remote Access (5 elements).
- Individual rows removed: CPD14 (SCADA Computer/HMI) and most cyber-physical flows (CPF1-CPF6, CPF8-CPF15), retaining only CPF7: Electricity.
- The cleaned threat matrix contains exactly the 53 elements specified in dwtf-cpfd-only.md, representing physical infrastructure, materials, energy flows, cyber-physical integrations, and physical security boundaries invisible to traditional STRIDE analysis.

The contents of Conversation 10 can be found in LLM/conversations/10/conversation-10-threat-matrix-cleanup.md
