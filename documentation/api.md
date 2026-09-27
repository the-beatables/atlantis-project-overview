# ATLANTIS — API Documentation

## AI-Powered Underwater Debris & Subsea Infrastructure Intelligence

**Smart India Hackathon 2026 | Problem Statement 26057 | Team The Beatables**

---

# 1. Overview

ATLANTIS uses an API-based architecture to connect the user interface with the AI inference and analysis pipeline.

The API layer is responsible for:

- Receiving sonar images
- Validating uploaded files
- Running AI inference
- Processing detections
- Generating annotated outputs
- Returning structured detection results
- Providing output files to the dashboard

The current backend architecture is based on **FastAPI**.

---

# 2. High-Level Architecture

The API workflow is:

Client
  ↓
FastAPI Backend
  ↓
Input Validation
  ↓
AI Model
  ↓
Post-Processing
  ↓
Evidence Analysis
  ↓
Geospatial Analysis
  ↓
Structured Response
  ↓
Dashboard

---

# 3. API Components

The API can be conceptually divided into the following components:

| Component | Responsibility |
|---|---|
| Upload Layer | Receives sonar images |
| Validation Layer | Checks input files |
| Inference Layer | Runs YOLO models |
| Evidence Layer | Performs additional image analysis |
| Geospatial Layer | Associates detections with locations |
| Output Layer | Generates JSON / images |
| Dashboard Layer | Presents results |

---

# 4. Image Upload

The upload endpoint accepts Side-Scan Sonar imagery for processing.

### Conceptual Endpoint

POST /predict

### Input

The request contains one or more image files.

Supported input should be limited to the formats configured by the deployment.

Typical formats include:

- JPG
- JPEG
- PNG
- BMP

The exact supported formats depend on the deployment configuration.

---

# 5. Single Image Request

A single-image request follows:

Image
  ↓
POST /predict
  ↓
Validation
  ↓
YOLO Inference
  ↓
Post-Processing
  ↓
JSON Response

The response contains the detected objects and associated metadata.

---

# 6. Multi-Image Processing

ATLANTIS is designed to support multiple sonar images.

Conceptually:

Multiple Images
  ↓
Upload
  ↓
Validation
  ↓
Batch Processing
  ↓
AI Inference
  ↓
Result Generation
  ↓
Multiple Detection Results

Each input image maintains its own detection results.

---

# 7. Detection Response

A simplified response structure is:

{
  "image": "sample_sonar_001.jpg",
  "detections": [
    {
      "class": "ghost_net",
      "confidence": 0.87,
      "bbox": [412, 185, 563, 294]
    }
  ]
}

The exact response structure may change as additional modules are integrated.

---

# 8. Detection Object

Each detection can contain:

| Field | Description |
|---|---|
| class | Predicted object category |
| confidence | Model confidence score |
| bbox | Bounding-box coordinates |
| image | Associated source image |

The bounding-box format is:

[x1, y1, x2, y2]

where:

- x1 = left coordinate
- y1 = top coordinate
- x2 = right coordinate
- y2 = bottom coordinate

---

# 9. Marine Debris Classes

The core YOLOv8n model supports:

| Class ID | Class |
|---:|---|
| 0 | Shipwreck |
| 1 | Pipe |
| 2 | Ghost Net |
| 3 | Rock / Seafloor Clutter |

The class names returned by the API should match the model configuration.

---

# 10. Pipeline Detection

Pipeline detection is implemented as a separate infrastructure-detection component.

Conceptually:

SSS Image
  ↓
Marine Debris Model
  +
Pipeline Model
  ↓
Combined Detection Context

A pipeline detection may contain:

- Pipeline class
- Confidence
- Bounding box
- Image identifier

The pipeline component is currently classified as:

**Prototyped / Integrating**

---

# 11. Evidence Analysis Response

Additional evidence can be associated with a detection.

Possible fields include:

- Detection confidence
- Object geometry
- Acoustic-shadow information
- Evidence image
- Explainability heatmap

A conceptual response may contain:

{
  "evidence": {
    "shadow_detected": true,
    "geometry_available": true,
    "heatmap": "outputs/heatmap_001.png"
  }
}

The exact evidence schema may evolve during development.

---

# 12. Geolocation Response

When navigation metadata is available, the API can associate detections with geographic coordinates.

Possible fields include:

{
  "location": {
    "latitude": 0.0,
    "longitude": 0.0
  }
}

Additional metadata may include:

- Timestamp
- Heading
- Vehicle position
- Sonar range
- Survey identifier

The coordinate output depends on the availability and quality of navigation and sonar metadata.

---

# 13. Infrastructure Proximity

When both debris and infrastructure detections are available, the API can provide spatial context.

Conceptually:

{
  "infrastructure_context": {
    "near_pipeline": true,
    "distance": 0.0,
    "review_priority": "review"
  }
}

The exact implementation and risk logic are still under development.

Therefore, proximity and risk values should be treated as prototype outputs until fully validated.

---

# 14. Risk / Review Status

The prototype can associate detections with a review status.

Possible statuses include:

- normal
- review
- potential_anomaly

These statuses are intended to support inspection prioritization.

They do not represent certified engineering or structural-risk assessments.

---

# 15. Annotated Image Output

The inference pipeline can generate an annotated image containing:

- Bounding boxes
- Class labels
- Confidence values

Example output:

sample_sonar_001_annotated.jpg

The dashboard can display this image alongside the structured detection response.

---

# 16. Explainability Output

The system can generate detection-specific visual evidence.

Possible output:

sample_sonar_001_heatmap.jpg

The dashboard can associate the heatmap with the corresponding detection.

Conceptually:

Detection
  ↓
Evidence Analysis
  ↓
Heatmap
  ↓
Dashboard Visualization

---

# 17. JSON Output

A complete conceptual response can contain:

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
  "infrastructure_context": {
    "near_pipeline": false
  },
  "status": "review"
}

The values shown above are illustrative.

---

# 18. Error Handling

The API should return structured errors for invalid requests.

Possible errors include:

| Error | Meaning |
|---|---|
| 400 | Invalid input |
| 404 | Resource not found |
| 413 | File too large |
| 422 | Validation error |
| 500 | Internal processing error |
| 503 | Model / processing service unavailable |

The exact status codes depend on the deployed FastAPI implementation.

---

# 19. Input Validation

The backend should validate:

- File type
- File size
- Image readability
- Image dimensions
- Required metadata
- Request structure

Invalid files should be rejected before model inference.

This prevents unnecessary GPU processing and reduces application errors.

---

# 20. Model Loading

The trained model should be loaded when the backend starts.

Recommended lifecycle:

Application Startup
  ↓
Load YOLOv8n
  ↓
Initialize Inference Environment
  ↓
Accept Requests
  ↓
Run Inference

The model should not be loaded from disk separately for every request unless required by the deployment architecture.

---

# 21. Output File Management

Generated files may include:

- Annotated images
- Heatmaps
- JSON files
- CSV files
- Reports

A conceptual output structure is:

outputs/
  |
  +-- annotated/
  |
  +-- heatmaps/
  |
  +-- json/
  |
  +-- csv/
  |
  +-- reports/

The exact storage system can be changed depending on deployment requirements.

---

# 22. API Security

A production API should implement appropriate security controls.

Recommended controls include:

- Authentication
- Authorization
- HTTPS
- Request validation
- File-size limits
- Rate limiting
- Secure credentials
- Access-controlled output storage

API keys and database credentials must not be stored directly in source code.

---

# 23. Environment Configuration

Sensitive configuration should be provided through environment variables.

Examples include:

DATABASE_URL

SECRET_KEY

API_KEY

MODEL_PATH

STORAGE_PATH

Actual credentials should never be committed to the public repository.

A `.env.example` file can be used to document required configuration without exposing real credentials.

---

# 24. API and Dashboard Integration

The dashboard communicates with the backend through API requests.

Conceptual flow:

React Dashboard
      ↓
API Request
      ↓
FastAPI
      ↓
YOLO / Analysis Pipeline
      ↓
JSON + Output URLs
      ↓
React Dashboard
      ↓
Visual Results

The frontend can use the returned URLs to display annotated images and evidence visualizations.

---

# 25. Asynchronous Processing

For large sonar surveys, synchronous API processing may not be sufficient.

A future production architecture can use:

API Request
    ↓
Create Processing Job
    ↓
Job Queue
    ↓
GPU Worker
    ↓
Inference
    ↓
Result Storage
    ↓
Job Status
    ↓
Dashboard

This allows large survey datasets to be processed without keeping a single HTTP request open for the complete processing duration.

---

# 26. Future API Extensions

Future versions may expose endpoints for:

- Survey creation
- Batch processing
- Pipeline analysis
- Cable detection
- Change detection
- Geospatial search
- Risk filtering
- Report generation
- Model version selection
- Processing-job monitoring

Possible conceptual routes include:

POST /surveys

POST /predict

POST /batch

GET /results/{id}

GET /surveys/{id}

GET /reports/{id}

These are architectural examples and may differ from the final implementation.

---

# 27. API Development Status

| Component | Status |
|---|---|
| Model Inference | Built |
| Image Processing | Built |
| Detection Output | Built |
| Multi-image Workflow | Built |
| JSON Output | Built |
| Annotated Images | Built |
| Evidence Output | Prototype |
| Geolocation | Prototype / Integration |
| Pipeline API Integration | Prototype / Integration |
| Infrastructure Proximity API | Next Integration |
| Authentication | Production Requirement |
| Async Job Queue | Future |
| Production Scaling | Future |

---

# 28. Example End-to-End Request

The intended end-to-end interaction is:

1. User uploads a Side-Scan Sonar image.
2. Frontend sends the image to the FastAPI backend.
3. Backend validates the input.
4. YOLOv8n performs marine-debris detection.
5. Pipeline detection can run independently.
6. Evidence analysis processes relevant detections.
7. Geolocation is performed when suitable metadata exists.
8. Infrastructure proximity can be calculated where applicable.
9. Results are converted into structured JSON.
10. Annotated images and visual evidence are generated.
11. The dashboard receives and displays the results.

---

# 29. Example End-to-End Output

A final conceptual result can contain:

Image

Detection:
  Class → Ghost Net
  Confidence → 0.87
  Bounding Box → [412, 185, 563, 294]

Evidence:
  Acoustic Shadow → Available
  Explainability → Available

Location:
  Latitude → Available
  Longitude → Available

Infrastructure:
  Nearby Pipeline → Yes / No

Review:
  Status → Normal / Review / Potential Anomaly

Outputs:
  Annotated Image
  Evidence Heatmap
  JSON
  CSV
  Dashboard Record

---

# 30. API Design Principles

ATLANTIS follows several API design principles:

### Modular

Each AI and analysis component can evolve independently.

### Lightweight

The core inference model is relatively small and suitable for optimization.

### Structured

Results are returned in machine-readable formats.

### Explainable

Detection results can be accompanied by visual evidence.

### Geospatial

Where metadata allows, detections can be associated with geographic locations.

### Scalable

The API can evolve from individual image inference toward large survey processing.

---

# 31. Final Architecture

The complete application flow is:

User
  ↓
React Dashboard
  ↓
FastAPI
  ↓
Input Validation
  ↓
YOLOv8n + Infrastructure Detector
  ↓
Evidence Analysis
  ↓
Geolocation
  ↓
Infrastructure Proximity
  ↓
Risk Prioritization
  ↓
JSON / CSV / Images
  ↓
Dashboard

This architecture provides the software foundation for transforming Side-Scan Sonar imagery into structured and actionable underwater intelligence.

---

## Project

**ATLANTIS — AI-Powered Underwater Debris & Subsea Infrastructure Intelligence**

**Smart India Hackathon 2026**

**Problem Statement:** 26057

**Team:** The Beatables
