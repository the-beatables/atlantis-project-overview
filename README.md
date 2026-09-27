ATLANTIS

AI-Powered Underwater Debris & Subsea Infrastructure Intelligence
Smart India Hackathon 2026 | Problem Statement 26057 | Team The Beatables

ATLANTIS is an AI-based Side-Scan Sonar (SSS) analysis system designed to automate the initial screening of underwater sonar imagery. It detects marine debris, provides supporting acoustic evidence, associates detections with geographic locations, and adds context from nearby subsea infrastructure.

The goal is to turn large volumes of raw sonar imagery into structured information that can help survey teams identify locations requiring further inspection.

Problem:

Side-Scan Sonar surveys can generate large amounts of underwater imagery that must often be reviewed manually.

The important objects that may need to be identified include:

• Shipwrecks
• Pipes
• Ghost nets
• Natural seafloor clutter
• Subsea infrastructure

ATLANTIS addresses the first stage of this process by automatically screening sonar imagery and producing location-linked detection results.

Our Approach

ATLANTIS combines AI-based object detection with acoustic and spatial analysis.

Side-Scan Sonar Imagery
↓
AI Detection
↓
Evidence Analysis
↓
Spatial Analysis
↓
Risk Prioritization
↓
Georeferenced Output

The system is designed as a modular pipeline so that additional detection and analysis modules can be added without redesigning the complete system.

Key Capabilities
Marine Debris Detection

The core YOLOv8n detector identifies four classes:

• Shipwreck
• Pipe
• Ghost Net
• Rock / Seafloor Clutter

Pipeline & Infrastructure Detection

A separate detection module is being developed for subsea infrastructure, including:

• Pipelines
• Cables
• Anchors
• Other large subsea structures

Acoustic Evidence

Detected objects can be analysed using:

• Detection confidence
• Object geometry
• Acoustic-shadow information
• Detection-specific visual evidence

This provides additional context beyond the bounding box prediction.

Geolocation

Where suitable survey and navigation metadata is available, detections can be associated with geographic coordinates.

The system is designed to generate structured location-linked results such as:

• Latitude
• Longitude
• Timestamp
• Detection class
• Confidence

Infrastructure Awareness

ATLANTIS considers the spatial relationship between marine debris and subsea infrastructure.

For example, debris detected close to a pipeline can be flagged for further inspection.

Risk Prioritization

The current prototype uses detection and spatial information to categorize locations for review.

Possible outputs include:

• Normal
• Review
• Potential Anomaly

These classifications are intended to support inspection prioritization and do not replace expert inspection.

Model

The core marine-debris detector uses YOLOv8n.

The model was selected because of its relatively small size and suitability for future edge deployment.

Training Configuration

Model: YOLOv8n
Training Images: 5,429
Validation Images: 1,163
Test Images: 1,164
Total Images: 7,756
Image Size: 640
Epochs: 75
Batch Size: 32
Model Size: ~5.95 MB

Model Performance

The current validation results are:

Precision: 80.5%
Recall: 80.4%
mAP@50: 82.2%
mAP@50–95: 68.9%

Note: mAP@50 is used as the detection performance metric and is not referred to as overall accuracy.

System Architecture

ATLANTIS follows a layered architecture:

Core Model
↓
Pipeline / Infrastructure Detection
↓
Spatial & Contextual Analysis
↓
Risk & Impact Analysis
↓
Actionable Output

Technical Workflow
1. Input

Side-Scan Sonar imagery is provided along with available navigation metadata.

Possible metadata includes:

• GPS position
• Timestamp
• Heading
• Depth
• Survey information

2. Preprocessing

The input data can undergo:

• Image validation
• Formatting
• Noise reduction
• Normalization
• Tiling where required

3. AI Detection

YOLOv8n performs the initial marine-debris detection.

The infrastructure detection module can separately identify pipeline and other large subsea structures.

4. Evidence Analysis

The system analyses the detection using confidence, geometry and acoustic-shadow information.

5. Spatial Analysis

Navigation metadata can be used to associate image detections with survey locations.

The system can also examine the spatial relationship between debris and infrastructure.

6. Risk Prioritization

Detected locations can be assigned a review priority based on available detection and spatial information.

7. Output

The system produces:

• Annotated sonar images
• Bounding boxes
• Class labels
• Confidence values
• Geographic coordinates
• JSON / CSV results
• Dashboard visualizations

Technology Stack
AI / Machine Learning

• Python
• PyTorch
• Ultralytics YOLOv8
• OpenCV

Backend

• FastAPI

Frontend

• React
• JavaScript

Database

• MongoDB

Geospatial Processing

• QGIS

Development & Training

• Google Colab

Current Development Status
Built & Validated

The following components have been developed and tested:

• Core marine-debris detection model
• YOLOv8n inference
• Detection visualization
• Acoustic evidence analysis
• Geolocation workflow
• Structured JSON / CSV output
• Dashboard prototype

Prototyped / Integrating

The following components are under integration:

• Pipeline detection
• Infrastructure proximity analysis
• Risk prioritization
• Infrastructure-aware analysis

Next Stage

Planned extensions include:

• Cable detection
• Pipeline condition analysis
• Change detection
• Larger-scale survey processing
• Edge GPU deployment
• AUV / ROV integration

Deployment Concept

ATLANTIS is designed as a software intelligence layer that can work with existing survey infrastructure.

Side-Scan Sonar
↓
AUV / ROV / Survey Vessel
↓
ATLANTIS AI Layer
↓
Detection & Evidence Analysis
↓
Geolocation & Infrastructure Context
↓
Dashboard / JSON / CSV / Reports

The lightweight model provides a starting point for future deployment on edge GPU systems. Actual onboard AUV/ROV deployment would require hardware-specific optimization and benchmarking.

Output Example

A typical structured result can contain information such as:

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

The coordinates shown above are example values and are not real survey coordinates.

Prototype

A working prototype demonstrates the sonar detection workflow, model outputs and dashboard functionality.

Prototype Demonstration

Watch the ATLANTIS Prototype: YOUR_YOUTUBE_LINK_HERE

Research & Dataset References

ATLANTIS builds on existing research in:

• Side-Scan Sonar target detection
• Underwater object detection
• Marine debris detection
• Subsea pipeline detection
• Acoustic-shadow analysis
• AUV / ROV-based underwater inspection

Dataset sources and relevant research references are documented separately in the documentation/ directory.

Repository Structure

ATLANTIS/
│
├── README.md
│
├── architecture/
│ └── system-architecture.png
│
├── documentation/
│ ├── methodology.md
│ ├── dataset.md
│ └── deployment.md
│
├── results/
│ ├── model-performance.png
│ ├── training-validation.png
│ └── sample-output.json
│
├── demo/
│ └── demo-link.md
│
└── .gitignore

Project Team
The Beatables

Smart India Hackathon 2026

Problem Statement: 26057
Theme: Disaster Management
Category: Software

Disclaimer

ATLANTIS is a research and prototype system developed for Smart India Hackathon 2026.

Detection results are intended to support initial sonar screening and inspection prioritization. They should not be treated as a replacement for expert survey interpretation, physical inspection or certified subsea asset assessment.
