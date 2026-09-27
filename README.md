# ATLANTIS

## AI-Powered Underwater Debris & Subsea Infrastructure Intelligence

**Smart India Hackathon 2026 | Problem Statement 26057 | Team The Beatables**

> **From raw Side-Scan Sonar imagery to explainable, georeferenced and actionable underwater intelligence.**

---

## 🌊 Overview

**ATLANTIS** is an AI-powered Side-Scan Sonar (SSS) analysis system designed to automate the initial screening of underwater sonar imagery.

It combines:

- 🤖 AI-based object detection
- 🔊 Acoustic evidence analysis
- 📍 Geospatial intelligence
- 🔗 Subsea infrastructure awareness
- ⚠️ Risk-based inspection prioritization

The goal is to help survey teams identify **what is underwater, where it is located, and which detections may require further inspection.**

---

## 🚨 Problem

Side-Scan Sonar surveys can generate thousands of images that require manual interpretation.

Important targets may include:

- Shipwrecks
- Pipes
- Ghost nets
- Seafloor clutter
- Subsea pipelines
- Cables
- Other underwater structures

Manual review can become time-consuming when large survey areas are involved.

**ATLANTIS provides an automated first-pass screening layer over existing sonar survey workflows.**

---

## 💡 Our Approach

ATLANTIS combines AI-based object detection with acoustic and spatial analysis.

```text
RAW SIDE-SCAN SONAR
        ↓
AI DETECTION
        ↓
EVIDENCE ANALYSIS
        ↓
SPATIAL ANALYSIS
        ↓
RISK PRIORITIZATION
        ↓
GEOREFERENCED OUTPUT
```

ATLANTIS is designed as a **modular intelligence pipeline**, allowing additional detection and analysis modules to be integrated without redesigning the entire system.

---

# 🧠 Key Capabilities

## 01. Marine Debris Detection

The core **YOLOv8n** model detects four classes:

| Class | Description |
|---|---|
| 🚢 Shipwreck | Man-made underwater wrecks |
| 🔧 Pipe | Pipe-like underwater objects |
| 🕸️ Ghost Net | Abandoned fishing nets |
| 🪨 Rock / Seafloor Clutter | Natural seabed objects |

---

## 02. Pipeline & Infrastructure Detection

A separate infrastructure detection module is being developed to identify:

- Subsea pipelines
- Cables
- Anchors
- Large underwater structures

This allows marine-debris detections to be analysed in relation to nearby infrastructure.

---

## 03. Acoustic Evidence

ATLANTIS goes beyond simply drawing a bounding box.

Detected objects can be analysed using:

- Detection confidence
- Object geometry
- Acoustic-shadow information
- Detection-specific visual evidence

This provides additional evidence that can support human review.

---

## 04. Geospatial Intelligence

When suitable AUV / ROV navigation metadata is available, detections can be associated with geographic locations.

Possible output information includes:

```text
Latitude
Longitude
Timestamp
Detection Class
Confidence
```

---

## 05. Infrastructure Awareness

ATLANTIS can analyse the spatial relationship between detected debris and subsea infrastructure.

For example:

```text
Marine Debris
      +
Nearby Pipeline
      ↓
Potential Inspection Priority
```

This helps move from **object detection** toward **infrastructure-aware inspection support**.

---

## 06. Risk Prioritization

The prototype can categorize detected locations for further review using available detection and spatial information.

```text
NORMAL
   ↓
REVIEW
   ↓
POTENTIAL ANOMALY
```

These classifications are intended to support inspection prioritization and do not replace expert survey interpretation.

---

# 🤖 AI Model

The core marine-debris detector uses **YOLOv8n**.

YOLOv8n was selected because its lightweight architecture is suitable for future edge-GPU and AUV/ROV deployment.

## Training Configuration

| Parameter | Value |
|---|---:|
| Model | YOLOv8n |
| Total Images | 7,756 |
| Training Images | 5,429 |
| Validation Images | 1,163 |
| Test Images | 1,164 |
| Image Size | 640 × 640 |
| Epochs | 75 |
| Batch Size | 32 |
| Model Size | ~5.95 MB |

---

# 📊 Model Performance

Current validation results:

| Metric | Result |
|---|---:|
| Precision | **80.5%** |
| Recall | **80.4%** |
| mAP@50 | **82.2%** |
| mAP@50–95 | **68.9%** |

> **Note:** mAP@50 is used as the primary detection performance metric and is not referred to as overall accuracy.

---

# 🏗️ System Architecture

```text
┌─────────────────────────────────────┐
│        CORE AI DETECTION            │
│ YOLOv8n — Marine Debris Detection   │
└──────────────────┬──────────────────┘
                   ↓
┌─────────────────────────────────────┐
│   PIPELINE / INFRASTRUCTURE AI      │
│ Pipelines • Cables • Structures     │
└──────────────────┬──────────────────┘
                   ↓
┌─────────────────────────────────────┐
│    SPATIAL & CONTEXTUAL ANALYSIS    │
│ Geolocation • Proximity • Geometry  │
└──────────────────┬──────────────────┘
                   ↓
┌─────────────────────────────────────┐
│       RISK & IMPACT ANALYSIS        │
│ Review Priority • Potential Hazard  │
└──────────────────┬──────────────────┘
                   ↓
┌─────────────────────────────────────┐
│        ACTIONABLE OUTPUT            │
│ Dashboard • JSON • CSV • Reports    │
└─────────────────────────────────────┘
```

---

# ⚙️ Technical Workflow

## 1️⃣ Input

Side-Scan Sonar imagery with available survey/navigation metadata.

## 2️⃣ Preprocessing

- Image validation
- Formatting
- Normalization
- Optional tiling

## 3️⃣ AI Detection

- Marine debris detection
- Pipeline / infrastructure detection

## 4️⃣ Evidence Analysis

- Confidence
- Geometry
- Acoustic shadow
- Visual evidence

## 5️⃣ Spatial Analysis

- Detection geolocation
- Infrastructure proximity
- Spatial relationships

## 6️⃣ Risk Prioritization

Potential inspection priorities are generated from available detection and spatial information.

## 7️⃣ Output

- Annotated sonar images
- Detection labels
- Confidence values
- Geographic coordinates
- JSON / CSV
- Dashboard visualizations

---

# 🛠️ Technology Stack

| Layer | Technologies |
|---|---|
| AI / ML | Python, PyTorch, YOLOv8 |
| Computer Vision | OpenCV |
| Backend | FastAPI |
| Frontend | React, JavaScript |
| Database | MongoDB |
| Geospatial | QGIS |
| Training | Google Colab |
| Deployment | Cloud GPU → Edge GPU → AUV/ROV |

---

# 🚀 Current Development Status

| Component | Status |
|---|---|
| Marine Debris Detection | ✅ Built & Validated |
| YOLOv8n Inference | ✅ Built & Validated |
| Detection Visualization | ✅ Built & Validated |
| Acoustic Evidence Analysis | ✅ Built & Validated |
| Geolocation Workflow | ✅ Built & Validated |
| JSON / CSV Output | ✅ Built & Validated |
| Dashboard Prototype | ✅ Built & Validated |
| Pipeline Detection | 🟡 Prototyped / Integrating |
| Infrastructure Proximity | 🟡 Prototyped / Integrating |
| Risk Prioritization | 🟡 Prototyped / Integrating |
| Cable Detection | ⚪ Next Stage |
| Pipeline Condition Analysis | ⚪ Next Stage |
| Change Detection | ⚪ Next Stage |
| Edge / AUV Deployment | ⚪ Next Stage |

---

# 🖥️ Prototype

The current prototype demonstrates:

- Multi-image sonar inference
- AI-based object detection
- Annotated sonar outputs
- Acoustic evidence analysis
- Structured JSON results
- Geospatial workflow
- Dashboard visualization

## 🎥 Prototype Demo

**[Watch the ATLANTIS Prototype](YOUR_YOUTUBE_LINK_HERE)**

---

# 📦 Example Output

A typical structured result can contain information such as:

```json
{
  "image": "sample_sonar_001.jpg",
  "detections": [
    {
      "class": "ghost_net",
      "confidence": 0.87,
      "bbox": [412, 185, 563, 294]
    }
  ],
  "location": {
    "latitude": 0.0,
    "longitude": 0.0
  },
  "status": "review"
}
```

> The coordinates above are example values and do not represent real survey locations.

---

# 🔬 Research Foundation

ATLANTIS builds on research and datasets related to:

- Side-Scan Sonar target detection
- Underwater object detection
- Marine debris detection
- Subsea pipeline detection
- Acoustic-shadow analysis
- AUV / ROV inspection
- Geospatial sonar analysis

Relevant dataset and research references are documented in the project documentation.

---

# 📁 Repository Structure

```text
ATLANTIS/
│
├── README.md
│
├── architecture/
│   └── system-architecture.png
│
├── documentation/
│   ├── methodology.md
│   ├── dataset.md
│   └── deployment.md
│
├── results/
│   ├── model-performance.png
│   ├── training-validation.png
│   └── sample-output.json
│
├── demo/
│   └── demo-link.md
│
└── .gitignore
```

---

# 🔮 Future Scope

ATLANTIS is designed to expand beyond initial marine-debris detection.

```text
MARINE DEBRIS
      ↓
PIPELINE DETECTION
      ↓
CABLE DETECTION
      ↓
CONDITION ANALYSIS
      ↓
CHANGE DETECTION
      ↓
AUTONOMOUS RETASKING
```

Future development areas include:

- Cable detection
- Pipeline condition analysis
- Change detection across repeat surveys
- Larger-scale survey processing
- Edge-GPU optimization
- AUV / ROV onboard inference

---

# 👥 Team

## The Beatables

**Smart India Hackathon 2026**

**Problem Statement:** 26057  
**Theme:** Disaster Management  
**Category:** Software

---

# ⚠️ Disclaimer

ATLANTIS is a research and prototype system developed for Smart India Hackathon 2026.

The system is intended to support **initial sonar screening and inspection prioritization**. Its outputs should not be treated as a replacement for expert survey interpretation, physical inspection, or certified subsea asset assessment.
