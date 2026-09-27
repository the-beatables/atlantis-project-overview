# ATLANTIS — Methodology

## AI-Powered Underwater Debris & Subsea Infrastructure Intelligence

**Smart India Hackathon 2026 | Problem Statement 26057 | Team The Beatables**

---

## 1. Objective

ATLANTIS is designed as a software-based intelligence layer for automated analysis of Side-Scan Sonar (SSS) imagery.

The methodology combines:

- Side-Scan Sonar image processing
- AI-based object detection
- Acoustic evidence analysis
- Geospatial localization
- Subsea infrastructure detection
- Spatial proximity analysis
- Risk prioritization
- Structured result generation

The primary objective is to reduce the amount of manual effort required for the initial screening of large sonar datasets and help identify locations that may require further inspection.

---

# 2. Overall Methodology

The ATLANTIS pipeline follows the following sequence:

```text
Side-Scan Sonar Imagery
          ↓
Image Validation & Preprocessing
          ↓
Marine Debris Detection
          ↓
Infrastructure Detection
          ↓
Evidence Analysis
          ↓
Geospatial Localization
          ↓
Debris–Infrastructure Spatial Analysis
          ↓
Risk Prioritization
          ↓
Dashboard / JSON / CSV / Report
```

The architecture is modular. Individual detection and analysis modules can be improved or replaced without changing the complete processing pipeline.

---

# 3. Input Data

ATLANTIS primarily operates on Side-Scan Sonar imagery.

The system can also use available survey and navigation metadata for geospatial processing.

Potential navigation information includes:

- Latitude
- Longitude
- Timestamp
- Heading
- Vehicle position
- Altitude / depth information
- Survey metadata

The availability and quality of this metadata directly affects the accuracy of geolocation.

---

# 4. Dataset

## 4.1 Marine Debris Dataset

The core marine-debris model was trained using a dataset containing:

| Parameter | Value |
|---|---:|
| Total Images | 7,756 |
| Training Images | 5,429 |
| Validation Images | 1,163 |
| Test Images | 1,164 |
| Split | 70 / 15 / 15 |
| Classes | 4 |

The four object classes are:

1. Shipwreck
2. Pipe
3. Ghost Net
4. Rock / Seafloor Clutter

The dataset contains both annotated images and images without target annotations.

---

# 5. Data Preprocessing

Before inference or training, sonar imagery is prepared for the detection pipeline.

The preprocessing stage includes:

- Image validation
- Image format handling
- Resolution standardization
- Normalization where required
- Annotation validation
- Dataset split verification

The YOLO-based detector uses an input size of:

**640 × 640 pixels**

Preprocessing is designed to maintain the visual structures present in sonar imagery while converting the data into a format suitable for the detection model.

---

# 6. Marine Debris Detection

## 6.1 Model Selection

ATLANTIS uses **YOLOv8n** as the core marine-debris detection model.

YOLOv8n was selected because:

- It is lightweight
- It provides real-time object-detection capability
- It has a relatively small model footprint
- It is suitable for future edge-GPU optimization
- It provides bounding-box based object localization

The trained model is approximately:

**5.95 MB**

---

## 6.2 Detection Classes

The core detector predicts four classes:

```text
0 → Shipwreck
1 → Pipe
2 → Ghost Net
3 → Rock / Seafloor Clutter
```

For every detected object, the model provides:

- Class label
- Confidence score
- Bounding-box coordinates

Example:

```text
Class: Ghost Net
Confidence: 0.87
Bounding Box: [x1, y1, x2, y2]
```

---

# 7. Model Training

The marine-debris detector was trained using a pretrained YOLOv8n model.

### Training configuration

| Parameter | Value |
|---|---:|
| Base Model | YOLOv8n |
| Epochs | 75 |
| Image Size | 640 |
| Batch Size | 32 |
| Training Images | 5,429 |
| Validation Images | 1,163 |
| Test Images | 1,164 |

The model was trained using GPU acceleration when available.

The objective of training was to learn visual patterns corresponding to the four defined sonar object classes.

---

# 8. Model Evaluation

The model is evaluated using standard object-detection metrics.

## 8.1 Precision

Precision measures the proportion of predicted detections that are correct.

```text
Precision = True Positives / (True Positives + False Positives)
```

Higher precision indicates fewer false-positive detections.

---

## 8.2 Recall

Recall measures how many of the relevant objects present in the dataset were successfully detected.

```text
Recall = True Positives / (True Positives + False Negatives)
```

Higher recall indicates that fewer relevant objects are missed.

---

## 8.3 mAP@50

Mean Average Precision at IoU threshold 0.50 is used to evaluate object-detection performance.

Current validation result:

**mAP@50 = 82.2%**

---

## 8.4 mAP@50–95

The stricter mAP@50–95 metric evaluates performance across multiple IoU thresholds.

Current validation result:

**mAP@50–95 = 68.9%**

---

## 8.5 Current Validation Results

| Metric | Result |
|---|---:|
| Precision | 80.5% |
| Recall | 80.4% |
| mAP@50 | 82.2% |
| mAP@50–95 | 68.9% |

These values represent the current validation results of the trained marine-debris detection model.

---

# 9. Detection Evidence Analysis

ATLANTIS does not rely only on the raw bounding-box prediction.

Additional information can be extracted from the detected region to provide supporting evidence.

The evidence-analysis layer considers:

- Detection confidence
- Object geometry
- Bounding-box characteristics
- Acoustic-shadow information
- Detection-specific visual evidence

This layer is intended to make the system more interpretable and useful for human inspection.

---

# 10. Acoustic-Shadow Analysis

Side-Scan Sonar imagery can contain acoustic shadows created when an object blocks the transmitted acoustic signal.

ATLANTIS uses this information as an additional source of evidence.

A simplified workflow is:

```text
Detected Object
      ↓
Identify Potential Shadow Region
      ↓
Measure Shadow Geometry
      ↓
Compare Object–Shadow Relationship
      ↓
Generate Supporting Evidence
```

The presence, size and geometry of a shadow can provide contextual information about a detected object.

However, acoustic-shadow analysis depends on sonar geometry, object orientation, sensor configuration and seabed conditions.

Therefore, the current implementation should be treated as an **evidence-analysis / prototype layer**, not as a calibrated physical measurement system.

---

# 11. Detection-Specific Explainability

ATLANTIS includes detection-specific visual evidence to help users understand why a detection may be important.

The system can generate visual representations around detected regions and analyse how the detection responds to localized image perturbations.

The intended workflow is:

```text
Original Sonar Image
        ↓
Target Detection
        ↓
Local Region Analysis
        ↓
Detection Response Measurement
        ↓
Heatmap Generation
```

The resulting visualization highlights image regions that contribute to the detection response.

This provides an additional visual interpretation layer alongside the model's confidence score.

---

# 12. Infrastructure Detection

Marine debris does not always exist in isolation.

A debris object located near a subsea pipeline or other critical infrastructure may require different attention from an isolated object.

ATLANTIS therefore uses a separate infrastructure-detection module.

The planned infrastructure layer includes:

- Pipeline detection
- Cable detection
- Large subsea structure detection

The pipeline detector is developed independently from the core marine-debris detector.

This separation allows the marine-debris model to remain unchanged while infrastructure intelligence is added around it.

---

# 13. Pipeline Detection

The pipeline module is based on a dedicated pipeline-detection dataset and model.

The current pipeline detection work uses Side-Scan Sonar imagery containing pipeline targets.

The infrastructure detector follows the same general object-detection principle:

```text
Pipeline SSS Image
        ↓
Image Preprocessing
        ↓
Pipeline Detection Model
        ↓
Pipeline Bounding Box
        ↓
Spatial / Condition Analysis
```

The pipeline detector is currently classified as:

**Prototyped / Integrating**

It is therefore treated as an extension of the core system rather than part of the fully validated marine-debris benchmark.

---

# 14. Infrastructure Proximity Analysis

After detecting both marine debris and infrastructure, ATLANTIS can analyse their spatial relationship.

Conceptually:

```text
Marine Debris Detection
          +
Pipeline / Infrastructure Detection
          ↓
Distance / Spatial Relationship
          ↓
Inspection Priority
```

If a detected debris object lies close to a detected infrastructure segment, the system can flag the location for further review.

The current implementation is a prototype and uses available image and spatial information.

It should not be interpreted as a certified structural-risk assessment.

---

# 15. Potential Pipeline Anomaly Analysis

A pipeline fault cannot reliably be confirmed from a single sonar image without suitable training labels, calibration and inspection evidence.

Therefore, ATLANTIS uses the term:

**Potential Pipeline Anomaly**

rather than claiming that a pipeline is definitively broken or damaged.

The prototype considers factors such as:

- Pipeline geometry
- Local continuity
- Acoustic-shadow behaviour
- Apparent deviations
- Spatial context

Conceptually:

```text
Pipeline Detection
       ↓
Local Pipeline Geometry
       ↓
Shadow / Geometry Analysis
       ↓
Deviation from Local Pattern
       ↓
Potential Anomaly
```

This component is currently a prototype and requires further validation using appropriately labelled inspection data.

---

# 16. Geolocation Methodology

ATLANTIS can associate detected objects with geographic coordinates when suitable navigation information is available.

The general process is:

```text
Image Detection
      ↓
Pixel Location
      ↓
Image / Sonar Geometry
      ↓
Range Estimation
      ↓
Vehicle Navigation Data
      ↓
Geographic Coordinate
```

Available information may include:

- Sonar image dimensions
- Detection pixel coordinates
- Sonar range
- AUV / ROV position
- Heading
- Timestamp
- Altitude or depth
- Survey geometry

The image-space detection is transformed into a survey-space location using the available sonar and navigation information.

---

# 17. Geolocation Considerations

Geolocation accuracy depends on the quality of the available navigation and sonar metadata.

Factors that may affect accuracy include:

- GPS / GNSS accuracy
- Navigation drift
- Vehicle heading
- Sonar range
- Image geometry
- Sensor mounting configuration
- Timing synchronization
- Water depth
- Slant-range / ground-range assumptions

Therefore, the system should be calibrated and validated against known survey reference points before being used for operational surveying.

---

# 18. Risk Prioritization

The risk layer combines available detection and spatial information.

A simplified conceptual model is:

```text
Object Type
     +
Detection Confidence
     +
Infrastructure Proximity
     +
Acoustic / Geometric Evidence
     ↓
Inspection Priority
```

The current prototype can categorize detections into:

```text
NORMAL
REVIEW
POTENTIAL ANOMALY
```

The purpose is to help direct human attention toward locations that may require additional inspection.

This is a prioritization mechanism rather than a replacement for expert assessment.

---

# 19. Multi-Image Processing

ATLANTIS supports processing multiple sonar images as part of the automated inference workflow.

The general process is:

```text
Multiple SSS Images
        ↓
Batch Upload
        ↓
Model Inference
        ↓
Detection Results
        ↓
Annotated Images
        ↓
Structured Results
```

For each processed image, the system can generate detection information and corresponding visual outputs.

This allows larger collections of sonar images to be screened without manually running the model on every image individually.

---

# 20. Output Generation

ATLANTIS produces structured and visual outputs.

### Visual Outputs

- Annotated sonar images
- Bounding boxes
- Detection labels
- Confidence values
- Explainability / evidence visualizations

### Structured Outputs

- JSON
- CSV
- Detection metadata
- Geographic coordinates where available
- Inspection status / priority

### Dashboard Outputs

The dashboard is intended to provide:

- Image visualization
- Detection information
- Evidence visualization
- Geographic information
- Structured results
- Inspection-oriented summaries

---

# 21. Software Architecture

The overall system can be represented as:

```text
┌──────────────────────────────┐
│     SIDE-SCAN SONAR DATA     │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│    DATA PREPROCESSING        │
│ Validation • Formatting      │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│       AI DETECTION           │
│ YOLOv8n + Pipeline Detector  │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│     EVIDENCE ANALYSIS        │
│ Confidence • Geometry        │
│ Acoustic Shadow • Heatmap    │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│   SPATIAL INTELLIGENCE       │
│ Geolocation • Proximity      │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│      RISK PRIORITIZATION     │
│ Normal • Review • Anomaly    │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│       ACTIONABLE OUTPUT      │
│ Dashboard • JSON • CSV       │
│ Images • Reports             │
└──────────────────────────────┘
```

---

# 22. Technology Stack

| Component | Technology |
|---|---|
| Programming | Python |
| Deep Learning | PyTorch |
| Object Detection | Ultralytics YOLOv8 |
| Computer Vision | OpenCV |
| Backend | FastAPI |
| Frontend | React / JavaScript |
| Database | MongoDB |
| Geospatial Processing | QGIS |
| Model Training | Google Colab |
| Deployment Target | Cloud GPU / Edge GPU / AUV / ROV |

---

# 23. Explainability Strategy

Explainability is implemented at multiple levels.

### Level 1 — Detection Confidence

The model provides confidence scores for predicted objects.

### Level 2 — Bounding-Box Geometry

The location and dimensions of the detected object provide spatial context.

### Level 3 — Acoustic Evidence

Potential acoustic shadows and related sonar structures provide additional evidence.

### Level 4 — Visual Explanation

Detection-specific visualizations can highlight regions associated with the model response.

### Level 5 — Spatial Context

The relationship between detected objects and subsea infrastructure provides additional operational context.

Together, these layers aim to make the system more interpretable than a simple object-detection output.

---

# 24. Current System Maturity

ATLANTIS is being developed in multiple stages.

## Built & Validated

The current validated components include:

- Core marine-debris detection
- YOLOv8n inference
- Detection visualization
- Acoustic evidence analysis
- Geolocation workflow
- Structured JSON / CSV generation
- Dashboard prototype

## Prototyped / Integrating

Current integration work includes:

- Pipeline detection
- Infrastructure proximity analysis
- Risk prioritization
- Infrastructure-aware analysis

## Next Stage

Planned development includes:

- Cable detection
- Pipeline condition analysis
- Change detection
- Larger-scale survey processing
- Edge-GPU optimization
- AUV / ROV integration

---

# 25. Deployment Concept

ATLANTIS is designed as a software intelligence layer over existing underwater survey infrastructure.

The deployment path is:

```text
Existing Sonar Hardware
        ↓
AUV / ROV / Survey Vessel
        ↓
ATLANTIS AI Processing
        ↓
Detection + Evidence Analysis
        ↓
Geolocation + Spatial Analysis
        ↓
Dashboard / Reports
```

The lightweight YOLOv8n model provides a basis for future edge deployment.

Actual onboard deployment would require hardware-specific optimization, benchmarking and field validation.

---

# 26. Future Methodology Extensions

The architecture is intentionally modular.

Future modules can extend the system toward:

```text
Marine Debris Detection
        ↓
Pipeline Detection
        ↓
Cable Detection
        ↓
Condition Analysis
        ↓
Change Detection
        ↓
Autonomous Retasking
```

Potential future improvements include:

- Improved cable detection
- Larger and more diverse sonar datasets
- Pipeline condition datasets
- Repeat-survey change detection
- More robust acoustic-shadow modelling
- Sensor-specific calibration
- Edge-GPU optimization
- AUV / ROV onboard inference
- Large-scale survey batch processing

---

# 27. Limitations

The current prototype has several important limitations.

### Dataset Limitations

Model performance depends on the distribution and quality of the training data.

### Class Imbalance

The marine-debris dataset contains an uneven distribution of object classes.

### Rock-Clutter Class

The rock-clutter class does not currently have annotated validation instances in the reported validation metrics.

### Geolocation

Geolocation accuracy depends on available navigation and sonar metadata.

### Acoustic Shadow

Shadow-based analysis is influenced by sonar configuration, object orientation and seabed conditions.

### Pipeline Condition

A single sonar image cannot reliably prove that a pipeline is broken or structurally damaged.

### Risk Assessment

The current risk layer is intended for inspection prioritization and should not be considered a certified engineering or structural-risk assessment.

### Field Validation

Operational deployment requires testing on real survey data across different sonar systems, seabed conditions and survey environments.

---

# 28. Summary

ATLANTIS combines multiple layers of underwater intelligence:

```text
DETECT
  ↓
EXPLAIN
  ↓
GEOLOCATE
  ↓
CONTEXTUALIZE
  ↓
PRIORITIZE
```

The core system provides AI-based marine-debris detection using a lightweight YOLOv8n model.

Additional modules extend the system toward:

- Subsea pipeline detection
- Infrastructure awareness
- Acoustic evidence
- Geospatial intelligence
- Inspection prioritization

The overall objective is to transform raw Side-Scan Sonar imagery into structured and actionable information that can support human survey and inspection workflows.

---

## Project

**ATLANTIS — AI-Powered Underwater Debris & Subsea Infrastructure Intelligence**

**Smart India Hackathon 2026**

**Problem Statement:** 26057

**Team:** The Beatables
