# ATLANTIS — Deployment Documentation

## AI-Powered Underwater Debris & Subsea Infrastructure Intelligence

**Smart India Hackathon 2026 | Problem Statement 26057 | Team The Beatables**

---

## 1. Deployment Overview

ATLANTIS is designed as a software intelligence layer that can operate on top of existing Side-Scan Sonar survey infrastructure.

The system does not require a new sonar sensor for its core functionality.

The deployment concept is:

Existing Side-Scan Sonar
        ↓
AUV / ROV / Survey Vessel
        ↓
ATLANTIS AI Processing
        ↓
Detection & Evidence Analysis
        ↓
Geospatial & Infrastructure Analysis
        ↓
Dashboard / JSON / CSV / Reports

The current prototype is primarily developed and tested in a cloud/development environment.

Future versions can be optimized for workstation, edge-GPU and AUV/ROV deployment.

---

# 2. Current Development Environment

The current model-development workflow uses:

- Python
- PyTorch
- Ultralytics YOLOv8
- OpenCV
- Google Colab
- NVIDIA GPU when available

The trained marine-debris model is approximately:

**5.95 MB**

The relatively small model size provides a basis for future edge deployment.

---

# 3. Deployment Architecture

ATLANTIS can be viewed as several deployment layers.

### Layer 1 — Sonar Data Source

The system receives:

- Side-Scan Sonar images
- Survey metadata
- Navigation metadata where available

Possible sources include:

- AUV
- ROV
- Survey vessel
- Existing sonar-processing workflow

---

### Layer 2 — AI Processing

The AI processing layer performs:

- Marine-debris detection
- Pipeline detection
- Object classification
- Confidence estimation
- Bounding-box generation

The core marine-debris model uses YOLOv8n.

---

### Layer 3 — Evidence Analysis

The system can perform additional analysis using:

- Object geometry
- Acoustic-shadow information
- Detection-specific visual evidence
- Local image characteristics

This layer provides supporting information beyond the initial detection.

---

### Layer 4 — Spatial Intelligence

Where suitable metadata is available, ATLANTIS can perform:

- Detection geolocation
- Infrastructure proximity analysis
- Spatial relationship analysis
- Survey-location association

---

### Layer 5 — Application Layer

The application layer presents:

- Annotated sonar images
- Detection information
- Evidence visualizations
- Geographic information
- JSON / CSV results
- Inspection priorities

---

# 4. Current Prototype Deployment

The current prototype follows a workflow similar to:

User / Survey Data
        ↓
Image Upload
        ↓
ATLANTIS Backend
        ↓
YOLOv8n Inference
        ↓
Evidence Analysis
        ↓
Structured Results
        ↓
Dashboard

The prototype supports multi-image inference rather than requiring users to process each sonar image manually.

---

# 5. Backend Deployment

The planned backend uses **FastAPI**.

The backend is responsible for:

- Receiving uploaded sonar images
- Validating input
- Loading the trained model
- Running inference
- Processing detections
- Generating output files
- Returning structured results
- Serving generated visual outputs

The model should be loaded once when the backend starts rather than reloaded for every image.

Conceptually:

Backend Startup
        ↓
Load Model
        ↓
Wait for Requests
        ↓
Receive Image
        ↓
Run Inference
        ↓
Generate Results
        ↓
Return Response

This reduces unnecessary model-loading overhead.

---

# 6. Frontend Deployment

The planned dashboard uses:

- React
- JavaScript

The frontend provides an interface for:

- Uploading sonar imagery
- Starting inference
- Viewing detections
- Viewing annotated images
- Viewing evidence visualizations
- Viewing geospatial information
- Reviewing structured results

The frontend communicates with the FastAPI backend through API requests.

---

# 7. API Workflow

A simplified request flow is:

Client
  ↓
POST /upload
  ↓
Backend receives image
  ↓
Image validation
  ↓
Model inference
  ↓
Post-processing
  ↓
Output generation
  ↓
JSON response
  ↓
Dashboard visualization

A typical response can contain:

- Image identifier
- Detection class
- Confidence
- Bounding box
- Output image location
- Geographic information where available
- Review status

---

# 8. Model Loading

The trained marine-debris model should be loaded once during backend initialization.

Recommended architecture:

Application Start
        ↓
Load best.pt
        ↓
Initialize YOLO Model
        ↓
Keep Model in Memory
        ↓
Process Incoming Requests

This avoids repeatedly loading the model from disk.

The trained model file should not be committed to the public GitHub repository unless its distribution is explicitly intended.

---

# 9. Multi-Image Processing

ATLANTIS is designed to process multiple sonar images.

A simplified workflow is:

Multiple Images
        ↓
Upload / Batch Input
        ↓
Input Validation
        ↓
Batch Inference
        ↓
Detection Results
        ↓
Annotated Images
        ↓
JSON / CSV
        ↓
Dashboard

For larger deployments, a job queue or worker-based architecture can be introduced.

---

# 10. Large-Scale Processing

For large sonar surveys, processing every image synchronously through a single web request may not be suitable.

A scalable architecture can use:

Survey Dataset
        ↓
Job Creation
        ↓
Processing Queue
        ↓
GPU Worker
        ↓
Inference
        ↓
Result Storage
        ↓
Dashboard

This allows large survey datasets to be processed without keeping a browser request open for the entire operation.

---

# 11. GPU Deployment

The model can be deployed on a GPU-enabled system for faster inference.

Possible environments include:

- Cloud GPU
- Local workstation GPU
- Edge GPU
- AUV / ROV compute hardware

The current project has been developed using Google Colab during model development.

The actual inference speed depends on:

- GPU hardware
- Image resolution
- Batch size
- Preprocessing
- Post-processing
- Number of images
- Model configuration

Therefore, deployment-specific benchmarking should be performed before operational use.

---

# 12. Edge Deployment

The lightweight YOLOv8n model provides a basis for future edge deployment.

The intended architecture is:

Side-Scan Sonar
        ↓
Edge Compute Device
        ↓
YOLOv8n
        ↓
Detection
        ↓
Evidence Analysis
        ↓
Local Storage / Transmission

Potential benefits include:

- Reduced dependence on continuous cloud connectivity
- Lower data-transfer requirements
- Faster local screening
- Onboard preliminary analysis

However, actual edge deployment requires hardware-specific testing and optimization.

---

# 13. AUV / ROV Deployment

Future ATLANTIS versions may be integrated with AUV or ROV systems.

A conceptual onboard workflow is:

AUV / ROV
        ↓
Side-Scan Sonar
        ↓
Onboard Compute
        ↓
ATLANTIS AI
        ↓
Detection
        ↓
Geospatial Context
        ↓
Inspection Decision Support

The current project should not be considered a fully operational onboard AUV/ROV deployment.

Hardware integration, communication interfaces, compute limitations and field validation would be required.

---

# 14. Cloud-to-Edge Deployment Path

ATLANTIS is designed to support progressive deployment.

The proposed development path is:

Development Environment
        ↓
Cloud GPU
        ↓
Survey Workstation
        ↓
Edge GPU
        ↓
AUV / ROV

This allows the system to be developed and validated before moving toward more constrained hardware environments.

---

# 15. Storage

ATLANTIS can generate several types of output data.

### Image Outputs

- Original sonar image
- Annotated sonar image
- Evidence visualization
- Heatmap

### Structured Outputs

- JSON
- CSV
- Detection metadata
- Coordinates
- Confidence values
- Review status

### Database Records

A future production system can store:

- Survey ID
- Image ID
- Detection ID
- Object class
- Confidence
- Bounding box
- Coordinates
- Timestamp
- Infrastructure relationship
- Review status

---

# 16. Suggested Production Storage Architecture

A scalable deployment can separate raw data, processed images and structured metadata.

Survey Data
     |
     +--------------------+
     |                    |
     ↓                    ↓
Object Storage        Database
     |                    |
     ↓                    ↓
Images / Heatmaps     Detection Metadata
     |                    |
     +----------+---------+
                ↓
            Dashboard

This prevents large image files from being stored directly inside a relational or document database when object storage is more appropriate.

---

# 17. Security Considerations

A production deployment should protect:

- Survey data
- Geographic coordinates
- Infrastructure locations
- User accounts
- API credentials
- Database credentials
- Model files

Recommended controls include:

- Authentication
- Authorization
- HTTPS
- Secure environment variables
- Access-controlled storage
- Input validation
- API rate limiting
- Logging
- Backup procedures

Sensitive survey coordinates should not be included in public repositories or demonstration files.

---

# 18. Environment Variables

Production credentials should be stored outside the source code.

Example configuration variables may include:

    DATABASE_URL
    API_KEY
    SECRET_KEY
    STORAGE_BUCKET
    MODEL_PATH

Actual credentials must never be committed to GitHub.

The public repository should contain only an example configuration file such as:

    .env.example

with placeholder values.

---

# 19. Containerization

A future deployment can use Docker to package the application and its dependencies.

Conceptually:

Docker Container
    |
    +-- FastAPI Backend
    +-- YOLOv8 Runtime
    +-- OpenCV
    +-- Python Dependencies

This can simplify deployment across:

- Cloud servers
- Local workstations
- GPU servers
- Edge devices

---

# 20. Model Optimization

Before deployment on constrained hardware, the model can be optimized.

Potential optimization methods include:

- FP16 inference
- ONNX export
- TensorRT optimization
- Batch-size tuning
- Image-size optimization
- Hardware-specific acceleration

These optimizations are considered future deployment work unless separately validated on the target hardware.

---

# 21. Monitoring

A production deployment should monitor both software and model performance.

### Infrastructure Metrics

- CPU usage
- GPU usage
- Memory usage
- Storage
- API latency
- Processing throughput

### Model Metrics

- Detection count
- Confidence distribution
- False-positive reports
- False-negative reports
- Class distribution
- Processing time per image

### Operational Metrics

- Images processed
- Survey jobs completed
- Failed jobs
- Processing duration
- Output generation failures

---

# 22. Failure Handling

The system should gracefully handle invalid or incomplete inputs.

Potential failures include:

- Unsupported image format
- Corrupted image
- Missing file
- Missing metadata
- Invalid coordinates
- Model loading failure
- GPU unavailability
- Processing timeout

The backend should return structured error responses rather than terminating the complete application.

---

# 23. Deployment Status

| Component | Status |
|---|---|
| Model Training Environment | Built & Validated |
| YOLOv8n Inference | Built & Validated |
| Multi-image Processing | Built & Validated |
| Detection Visualization | Built & Validated |
| Evidence Analysis | Built & Validated |
| JSON / CSV Output | Built & Validated |
| Dashboard Prototype | Built & Validated |
| FastAPI Integration | Development / Integration |
| Pipeline Detection | Prototyped / Integrating |
| Infrastructure Proximity | Prototyped / Integrating |
| Edge Deployment | Next Stage |
| AUV / ROV Onboard Deployment | Next Stage |

---

# 24. Deployment Roadmap

The deployment roadmap is:

### Stage 1 — Development

- Train models
- Validate datasets
- Test inference
- Build dashboard

### Stage 2 — Integrated Application

- FastAPI backend
- React frontend
- Persistent result storage
- Batch processing

### Stage 3 — Survey Workstation

- Local GPU inference
- Large survey processing
- Geospatial visualization
- Automated reporting

### Stage 4 — Edge Deployment

- Model optimization
- Edge-GPU benchmarking
- Reduced data transfer
- Local inference

### Stage 5 — AUV / ROV Integration

- Hardware integration
- Navigation-data integration
- Onboard inference
- Field testing
- Autonomous inspection support

---

# 25. Deployment Principles

ATLANTIS follows four main deployment principles:

**Software-first**

The system is designed to work as an intelligence layer over existing sonar infrastructure.

**Modular**

Detection, evidence, geolocation and risk modules can evolve independently.

**Lightweight**

The core YOLOv8n model has a small model footprint suitable for future edge optimization.

**Scalable**

The architecture can progress from individual image analysis to large survey processing and eventually onboard inference.

---

# 26. Final Deployment Concept

The long-term ATLANTIS deployment architecture is:

Existing Sonar
        ↓
AUV / ROV / Survey Vessel
        ↓
ATLANTIS AI Layer
        ↓
Marine Debris + Infrastructure Detection
        ↓
Evidence Analysis
        ↓
Geolocation + Spatial Intelligence
        ↓
Risk Prioritization
        ↓
Dashboard / Reports / API
        ↓
Human Inspection Decision

ATLANTIS is intended to support underwater survey teams by converting large volumes of sonar imagery into structured, explainable and location-aware information.

The system is designed to assist human decision-making rather than replace certified survey, inspection or engineering processes.

---

## Project

**ATLANTIS — AI-Powered Underwater Debris & Subsea Infrastructure Intelligence**

**Smart India Hackathon 2026**

**Problem Statement:** 26057

**Team:** The Beatables
