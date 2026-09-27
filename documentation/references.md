# ATLANTIS — References & Research

## AI-Powered Underwater Debris & Subsea Infrastructure Intelligence

**Smart India Hackathon 2026 | Problem Statement 26057 | Team The Beatables**

---

# 1. Purpose

This document records the major datasets, research references, technical resources and external sources considered during the development of ATLANTIS.

The references are grouped according to their relevance to:

- Side-Scan Sonar
- Marine debris detection
- Underwater object detection
- Pipeline detection
- AUV / ROV inspection
- Geospatial analysis
- Subsea infrastructure intelligence

---

# 2. Side-Scan Sonar Background

## NOAA Ocean Exploration — Side-Scan Sonar

NOAA Ocean Exploration provides an overview of Side-Scan Sonar technology and its use for imaging and mapping the seafloor.

Side-Scan Sonar can be used to identify and characterize underwater objects and seabed features.

Source:

https://oceanexplorer.noaa.gov/technology/sonar-side-scan/

Relevance to ATLANTIS:

- Side-Scan Sonar fundamentals
- Seafloor mapping
- Underwater object identification
- Acoustic shadows
- Marine survey applications

---

# 3. Subsea Pipeline Dataset

## SubPipe Dataset

The SubPipe dataset is used as a reference and development dataset for the pipeline-detection component of ATLANTIS.

The dataset contains Side-Scan Sonar imagery from real pipeline inspection activities and includes annotated pipeline targets.

Dataset:

**SubPipe — Side-Scan Sonar Pipeline Dataset**

Zenodo:

https://zenodo.org/records/10808161

GitHub:

https://github.com/remaro-network/SubPipe-dataset

Relevance to ATLANTIS:

- Pipeline detection
- Side-Scan Sonar object detection
- AUV-based inspection
- Pipeline bounding-box annotations
- Infrastructure-aware sonar analysis

---

# 4. Pipeline & Subsea Asset Inspection

## EIVA — Cable, Pipe & Asset Inspections

EIVA provides commercial subsea inspection and data-processing solutions involving underwater assets, sonar, navigation and automated analysis.

Source:

https://www.eiva.com/about/what-we-do/cable-pipe-asset-inspections

Relevance to ATLANTIS:

- Subsea pipeline inspection
- Cable inspection
- AUV / ROV workflows
- Sonar-based asset analysis
- Automated inspection workflows
- Geospatial outputs

This reference is used to understand the existing subsea inspection ecosystem and the type of workflows ATLANTIS could complement.

---

# 5. Autonomous Pipeline Inspection

## EIVA — Autonomous Pipeline Inspection Software Development

This case study describes development of autonomous pipeline inspection capabilities involving underwater vehicles, navigation and automated processing.

Source:

https://www.eiva.com/about/case-studies/cable-pipe-and-asset-inspections/autonomous-pipeline-inspection-software-development-project

Relevance to ATLANTIS:

- Autonomous inspection
- AUV-based processing
- Pipeline inspection
- Automated event detection
- Navigation integration

This provides context for the future edge and AUV/ROV deployment direction of ATLANTIS.

---

# 6. Offshore Wind & Marine Survey Requirements

## National Institute of Wind Energy — Offshore Wind Development

NIWE is India's nodal organization for offshore wind development and conducts or supports offshore studies and surveys.

Source:

https://niwe.res.in/department/department_owd/

Relevance to ATLANTIS:

- Offshore survey ecosystem
- Seabed studies
- Offshore wind development
- Marine survey requirements
- Potential Indian deployment environment

---

# 7. NIWE Offshore Wind Portal

NIWE's offshore wind portal provides information related to offshore wind studies, surveys and development activities.

Source:

https://offshore.niwe.res.in/

Relevance to ATLANTIS:

- Offshore survey activities
- Seabed information
- Offshore wind development
- Indian marine infrastructure context

---

# 8. NIWE Survey Documentation

NIWE survey documentation references geophysical examination of seabed and subsoil and includes Side-Scan Sonar among survey data sources.

Source:

https://niwe.res.in/assets/Docu/Circular%20draft%20tender%20document.pdf

Relevance to ATLANTIS:

- Geophysical seabed surveys
- Side-Scan Sonar data
- Offshore survey workflows
- Indian offshore wind context

---

# 9. POWERGRID — Offshore Transmission

POWERGRID's annual reporting documents its involvement in offshore wind-related transmission infrastructure and undersea export power cables.

Source:

https://www.powergrid.in/sites/default/files/annual_reports/Powergrid_Annual_Report_2024-25-1.pdf

Relevance to ATLANTIS:

- Subsea power cables
- Offshore transmission
- Marine infrastructure
- Infrastructure inspection context

---

# 10. L&T — Offshore Engineering

Larsen & Toubro has documented offshore engineering and EPC activities involving offshore infrastructure and subsea systems.

Relevant source:

https://www.larsentoubro.com/pressreleases/2026/2026-08-07-lt-wins-offshore-orders-major-from-ongc

Additional source:

https://www.larsentoubro.com/pressreleases/2026/2026-09-09-lt-wins-large-offshore-order-from-ongc

Relevance to ATLANTIS:

- Offshore EPC
- Subsea infrastructure
- Offshore platforms
- Pipeline and cable-related engineering context

---

# 11. Fugro — Offshore Survey & Pipeline Inspection

Fugro provides offshore site characterization, geophysical survey and subsea inspection services.

A relevant 2026 example includes pipeline survey activities in Timor-Leste.

Source:

https://www.fugro.com/news/business-news/2026/fugro-signed-contract-for-greater-sunrise-and-bayu-undan-pipeline-survey-programme-in-timor-leste

Relevance to ATLANTIS:

- Offshore geophysical surveys
- AUV surveys
- Pipeline routing
- Geohazard assessment
- Subsea inspection

---

# 12. Underwater Object Detection Research

ATLANTIS builds on research in deep-learning-based Side-Scan Sonar object detection.

Relevant research areas include:

- YOLO-based sonar target detection
- Transformer-enhanced object detection
- AUV sonar target detection
- Underwater object recognition
- Real-time sonar detection

These studies provide technical context for the selection and development of lightweight object-detection approaches.

---

# 13. Transformer-YOLOv5 Research

Research involving Transformer-enhanced YOLOv5 approaches has demonstrated the use of deep-learning object detection for Side-Scan Sonar target detection and localization.

Reported research results include metrics such as:

- mAP
- Macro-F2
- Detection speed

The work provides context for deep-learning-based SSS target detection.

ATLANTIS does not directly reproduce the reported research model.

---

# 14. MA-YOLOv7 Research

Research involving MA-YOLOv7 has investigated real-time Side-Scan Sonar target detection for AUV applications.

The research is relevant to:

- AUV deployment
- Real-time detection
- Side-Scan Sonar imagery
- Lightweight inference

The research provides supporting context for the future onboard-deployment direction of ATLANTIS.

---

# 15. Pipeline Detection Research

Research in deep-learning-based pipeline detection demonstrates the application of computer vision and object detection to subsea pipeline imagery.

Relevant research directions include:

- Pipeline target detection
- Sonar-based pipeline recognition
- YOLO-based detection
- Pipeline and cable segmentation
- High-resolution sonar analysis

These studies provide technical context for the separate infrastructure-detection module in ATLANTIS.

---

# 16. Product & Technology Landscape

ATLANTIS was also compared conceptually with existing commercial sonar-processing and subsea inspection solutions.

The comparison considered publicly documented capabilities from:

- SonarWiz
- EIVA NaviSuite
- Klein MIND SpectralAi

The purpose of the comparison is not to claim identical functionality or direct equivalence.

Instead, it identifies areas where ATLANTIS combines multiple capabilities into a single prototype workflow.

---

# 17. SonarWiz

SonarWiz provides Side-Scan Sonar processing and survey-analysis capabilities.

Relevant publicly documented areas include:

- Side-Scan Sonar processing
- Target identification
- Classification
- Contact capture
- Mosaicing
- Reporting
- Survey workflow support

Source:

https://chesapeaketech.com/sonarwiz/

Relevance to ATLANTIS:

Provides context for conventional sonar-processing workflows that ATLANTIS aims to augment with AI-based automated screening.

---

# 18. EIVA NaviSuite

EIVA NaviSuite provides subsea inspection and asset-analysis capabilities involving pipelines, cables and other underwater infrastructure.

Relevant capabilities include:

- Pipeline inspection
- Cable inspection
- AUV / ROV workflows
- Automated eventing
- Deep-learning-based analysis
- Geospatial outputs

Source:

https://www.eiva.com/

Relevance to ATLANTIS:

Provides context for infrastructure-aware underwater inspection workflows.

---

# 19. Klein MIND SpectralAi

Klein Marine Systems has developed sonar-related technologies involving automated target recognition and AI-based analysis.

Relevant areas include:

- Sonar-based target recognition
- Automated classification
- AI-assisted analysis
- Near-real-time processing

Source:

https://www.kleinmarinesystems.com/

Relevance to ATLANTIS:

Provides context for AI-assisted sonar target recognition.

---

# 20. Comparison Scope

The ATLANTIS comparison considers the following capability areas:

| Capability | ATLANTIS Focus |
|---|---|
| Side-Scan Sonar Processing | Yes |
| Marine Debris Detection | Core capability |
| Automated Target Detection | Core capability |
| Pipeline Detection | Prototype / Integration |
| Cable Detection | Future scope |
| Acoustic Evidence | Prototype capability |
| Explainable Detection | Prototype capability |
| Georeferenced Output | Core workflow |
| Infrastructure + Debris Relationship | Prototype / Integration |
| Lightweight Custom AI | Core design principle |
| Risk Prioritization | Prototype capability |

Commercial product capabilities can vary by product version, sensor configuration and deployment environment.

---

# 21. Research-to-Implementation Mapping

The following mapping shows how external research and technical references relate to ATLANTIS.

| Research / Reference Area | ATLANTIS Component |
|---|---|
| Side-Scan Sonar | Input data |
| SSS Object Detection | YOLOv8n marine-debris detector |
| Underwater Target Recognition | Object classification |
| Acoustic Shadows | Evidence analysis |
| Pipeline Detection | Infrastructure detector |
| AUV Inspection | Future deployment |
| Geospatial Surveying | Detection geolocation |
| Subsea Asset Inspection | Infrastructure awareness |
| Automated Event Detection | Risk / review prioritization |

---

# 22. What Is Implemented vs Referenced

External research is used as technical context and does not imply that every referenced capability has been implemented in ATLANTIS.

### Implemented / Validated

- Marine-debris detection
- YOLOv8n inference
- Detection visualization
- Acoustic evidence analysis
- Geolocation workflow
- Structured JSON / CSV output
- Dashboard prototype

### Prototyped / Integrating

- Pipeline detection
- Infrastructure proximity analysis
- Risk prioritization
- Infrastructure-aware analysis

### Future

- Cable detection
- Pipeline condition analysis
- Change detection
- Edge-GPU deployment
- AUV / ROV onboard inference

---

# 23. Reference Usage Policy

The project uses external datasets and research for development and technical understanding.

Where external datasets, images, code or research are used, the project should:

- Preserve attribution
- Follow the applicable license
- Follow redistribution requirements
- Avoid claiming external work as original
- Clearly distinguish project results from published results

---

# 24. Important Evaluation Note

Published research results and commercial product capabilities should not be directly interpreted as performance guarantees for ATLANTIS.

ATLANTIS performance is represented by its own measured validation results:

**Precision:** 80.5%

**Recall:** 80.4%

**mAP@50:** 82.2%

**mAP@50–95:** 68.9%

These values correspond to the current marine-debris model validation setup described in the project documentation.

---

# 25. Primary Reference List

1. NOAA Ocean Exploration — Side-Scan Sonar  
   https://oceanexplorer.noaa.gov/technology/sonar-side-scan/

2. SubPipe Dataset — Zenodo  
   https://zenodo.org/records/10808161

3. SubPipe Dataset — GitHub  
   https://github.com/remaro-network/SubPipe-dataset

4. EIVA — Cable, Pipe & Asset Inspections  
   https://www.eiva.com/about/what-we-do/cable-pipe-asset-inspections

5. EIVA — Autonomous Pipeline Inspection  
   https://www.eiva.com/about/case-studies/cable-pipe-and-asset-inspections/autonomous-pipeline-inspection-software-development-project

6. NIWE — Offshore Wind Development  
   https://niwe.res.in/department/department_owd/

7. NIWE — Offshore Wind Portal  
   https://offshore.niwe.res.in/

8. NIWE — Survey Documentation  
   https://niwe.res.in/assets/Docu/Circular%20draft%20tender%20document.pdf

9. POWERGRID — Annual Report 2024–25  
   https://www.powergrid.in/sites/default/files/annual_reports/Powergrid_Annual_Report_2024-25-1.pdf

10. L&T — Offshore Engineering Activities  
    https://www.larsentoubro.com/

11. Fugro — Offshore Pipeline Survey Programme  
    https://www.fugro.com/news/business-news/2026/fugro-signed-contract-for-greater-sunrise-and-bayu-undan-pipeline-survey-programme-in-timor-leste

12. SonarWiz  
    https://chesapeaketech.com/sonarwiz/

13. EIVA  
    https://www.eiva.com/

14. Klein Marine Systems  
    https://www.kleinmarinesystems.com/

---

# 26. Conclusion

ATLANTIS combines established Side-Scan Sonar techniques, modern object detection and geospatial analysis into a modular underwater intelligence workflow.

The external references documented here provide the technical and application context for:

- Marine debris detection
- Sonar-based target recognition
- Pipeline inspection
- Infrastructure monitoring
- AUV / ROV deployment
- Geospatial survey analysis

The project distinguishes between capabilities that have been **built and validated**, capabilities that are **prototyped and integrating**, and capabilities that remain **future development areas**.

---

## Project

**ATLANTIS — AI-Powered Underwater Debris & Subsea Infrastructure Intelligence**

**Smart India Hackathon 2026**

**Problem Statement:** 26057

**Team:** The Beatables
