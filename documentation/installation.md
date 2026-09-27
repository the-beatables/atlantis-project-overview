# ATLANTIS — Installation & Setup

## AI-Powered Underwater Debris & Subsea Infrastructure Intelligence

**Smart India Hackathon 2026 | Problem Statement 26057 | Team The Beatables**

---

# 1. Overview

This document describes the setup requirements and development workflow for ATLANTIS.

ATLANTIS consists of several components:

- AI / ML inference
- Image processing
- Backend API
- Frontend dashboard
- Structured output generation
- Optional geospatial processing
- Infrastructure detection modules

The public repository is intended primarily for documentation, reproducibility and demonstration.

The complete private development environment may contain additional components that are not included in the public repository.

---

# 2. System Requirements

## Minimum Development Environment

Recommended:

- Python 3.10+
- 8 GB RAM or more
- Modern CPU
- 10 GB+ available storage
- Internet connection

## Recommended AI Development Environment

For model training or GPU inference:

- NVIDIA GPU
- CUDA-compatible environment
- 8 GB+ GPU memory recommended
- 16 GB+ system RAM recommended

The exact GPU requirement depends on image resolution, batch size and model configuration.

---

# 3. Software Requirements

The core development stack includes:

| Component | Technology |
|---|---|
| Language | Python |
| Deep Learning | PyTorch |
| Object Detection | Ultralytics YOLOv8 |
| Computer Vision | OpenCV |
| Backend | FastAPI |
| Frontend | React |
| Frontend Language | JavaScript |
| Database | MongoDB |
| Geospatial | QGIS |
| Development Environment | Google Colab / Local Machine |

---

# 4. Repository Structure

The public repository follows a documentation-oriented structure.

    ATLANTIS/
    |
    +-- README.md
    |
    +-- architecture/
    |   +-- system-architecture.png
    |
    +-- documentation/
    |   +-- methodology.md
    |   +-- dataset.md
    |   +-- deployment.md
    |   +-- references.md
    |   +-- api.md
    |   +-- installation.md
    |
    +-- results/
    |   +-- model-performance.png
    |   +-- training-validation.png
    |   +-- sample-output.json
    |
    +-- demo/
    |   +-- demo-link.md
    |
    +-- examples/
    |
    +-- .gitignore

The exact structure may evolve as the project develops.

---

# 5. Clone the Repository

Clone the public repository using Git:

    git clone YOUR_PUBLIC_REPOSITORY_URL

Move into the project directory:

    cd ATLANTIS

Replace `YOUR_PUBLIC_REPOSITORY_URL` with the actual public GitHub repository URL.

---

# 6. Python Environment

Creating a virtual environment is recommended.

On Windows:

    python -m venv venv

    venv\Scripts\activate

On Linux / macOS:

    python3 -m venv venv

    source venv/bin/activate

Using a virtual environment prevents project dependencies from interfering with system-wide Python packages.

---

# 7. Install Python Dependencies

Install the required Python packages using the project's dependency file if one is provided.

Recommended command:

    pip install -r requirements.txt

If the public repository does not contain a requirements file yet, the main AI dependencies include:

- ultralytics
- torch
- torchvision
- opencv-python
- numpy
- pandas
- fastapi
- uvicorn
- python-multipart

Additional packages may be required depending on the enabled modules.

---

# 8. Verify Python Installation

Check the installed Python version:

    python --version

A compatible Python environment should be used consistently across development and deployment.

---

# 9. Verify PyTorch

PyTorch can be checked using:

    python -c "import torch; print(torch.__version__)"

For GPU-enabled environments:

    python -c "import torch; print(torch.cuda.is_available())"

If the output is:

    True

PyTorch can access a CUDA-enabled GPU.

If the output is:

    False

the system will use CPU execution unless another compatible accelerator configuration is available.

---

# 10. Verify Ultralytics

Check the YOLO installation:

    python -c "import ultralytics; print(ultralytics.__version__)"

The YOLO runtime should be available before attempting inference.

---

# 11. Model Weights

The trained marine-debris model is approximately:

**5.95 MB**

The private trained weights are not included in the public repository.

The expected model file is:

    best.pt

If model weights are provided separately, place the file in the configured model directory.

Example:

    models/
    |
    +-- best.pt

The exact model path should be configured through the application settings rather than hard-coded where possible.

---

# 12. Model Security

The following files should not be committed to the public repository unless intentionally released:

- best.pt
- Other `.pt` files
- `.pth` files
- `.onnx` model files
- TensorRT engine files
- API keys
- Database credentials
- Private survey data
- Sensitive geographic coordinates

The `.gitignore` file should prevent accidental commits.

---

# 13. Environment Configuration

Sensitive configuration should be stored using environment variables.

Example variables include:

    MODEL_PATH
    DATABASE_URL
    SECRET_KEY
    API_KEY
    STORAGE_PATH

A public repository can contain:

    .env.example

with placeholder values.

Actual credentials should remain local or inside the deployment environment.

---

# 14. Running the Inference Pipeline

The inference workflow is conceptually:

    Input SSS Image
          ↓
    Image Validation
          ↓
    YOLOv8n
          ↓
    Detection
          ↓
    Post-Processing
          ↓
    Annotated Output
          ↓
    JSON / CSV

The exact inference command depends on the implementation included in the active project version.

---

# 15. Running the Backend

The ATLANTIS backend is designed around FastAPI.

A typical development command is:

    uvicorn main:app --reload

The exact Python module name may differ depending on the backend structure.

When successfully started, FastAPI normally exposes interactive API documentation through:

    /docs

and alternative API documentation through:

    /redoc

These endpoints are intended for development and API testing.

---

# 16. Running the Frontend

The frontend is based on React.

Install frontend dependencies from the frontend directory:

    npm install

Start the development server:

    npm run dev

The exact command may vary depending on whether the project uses Vite or another React configuration.

---

# 17. Backend–Frontend Connection

The frontend communicates with the backend through HTTP requests.

The general workflow is:

    React Dashboard
          ↓
    FastAPI Endpoint
          ↓
    Image Upload
          ↓
    AI Inference
          ↓
    JSON Response
          ↓
    Dashboard Update

The frontend should use an environment variable for the backend URL where possible.

Example:

    VITE_API_URL=http://localhost:8000

The actual variable name depends on the frontend implementation.

---

# 18. Running the Complete Local System

A typical local development setup consists of two processes.

### Terminal 1 — Backend

    uvicorn main:app --reload

### Terminal 2 — Frontend

    npm run dev

The frontend then communicates with the FastAPI backend.

---

# 19. API Testing

The backend can be tested using:

- Browser API documentation
- Postman
- cURL
- Frontend requests

The API should first be tested independently before connecting the complete dashboard.

Recommended testing sequence:

    Backend Startup
          ↓
    API Health Check
          ↓
    Single Image Test
          ↓
    Multi-image Test
          ↓
    Output Verification
          ↓
    Frontend Integration

---

# 20. Sample Input

A suitable test image should be a Side-Scan Sonar image compatible with the trained model.

The test image should contain:

- Valid image format
- Readable image data
- Appropriate sonar imagery
- No corrupted file data

If a test image contains sensitive survey information, it should not be uploaded to a public repository.

---

# 21. Sample Output

A successful inference may produce:

- Annotated image
- Detection class
- Confidence
- Bounding-box coordinates
- JSON result
- Optional CSV result
- Evidence visualization

Example conceptual result:

    Image:
    sample_sonar_001.jpg

    Detection:
    Ghost Net

    Confidence:
    0.87

    Bounding Box:
    [412, 185, 563, 294]

---

# 22. Pipeline Detection Setup

The pipeline detector is maintained as a separate module from the marine-debris model.

Conceptually:

    SSS Image
       |
       +-------------------+
       |                   |
       ↓                   ↓
    YOLOv8n          Pipeline Detector
       |                   |
       +---------+---------+
                 ↓
          Spatial Analysis

The pipeline component is currently:

**Prototyped / Integrating**

The exact pipeline model and weights are not included in the public repository unless intentionally released.

---

# 23. Dataset Setup

The complete training datasets are not included in the public repository.

The public repository contains dataset documentation describing:

- Dataset size
- Classes
- Dataset splits
- Annotation format
- Training configuration
- Dataset sources

For external datasets such as SubPipe, users should obtain the dataset directly from the original source and comply with its license and attribution requirements.

---

# 24. Google Colab Development

Google Colab was used during model development and experimentation.

A typical development workflow is:

    Upload / Mount Dataset
            ↓
    Install Dependencies
            ↓
    Validate Dataset
            ↓
    Train Model
            ↓
    Validate Model
            ↓
    Save best.pt
            ↓
    Backup Model
            ↓
    Run Inference

GPU availability should always be checked before training.

---

# 25. GPU Training

When a CUDA-enabled GPU is available, PyTorch can use GPU acceleration.

Check GPU availability:

    python -c "import torch; print(torch.cuda.is_available())"

The exact training speed depends on:

- GPU model
- Batch size
- Image resolution
- Number of workers
- Dataset size
- Augmentation
- Storage speed

---

# 26. CPU Inference

ATLANTIS can also run inference on CPU-compatible systems, although processing speed may be lower.

CPU execution can be useful for:

- Testing
- Debugging
- API development
- Small inference jobs
- Environments without CUDA

For large-scale inference, GPU acceleration is recommended where available.

---

# 27. Output Directory

A typical application may use:

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

Generated outputs should be excluded from version control if they contain sensitive survey information or large files.

---

# 28. Troubleshooting

## Python package not found

If an import error occurs, verify that the virtual environment is activated.

Then run:

    pip install -r requirements.txt

---

## Ultralytics not found

Install the package:

    pip install ultralytics

Then verify:

    python -c "import ultralytics; print(ultralytics.__version__)"

---

## PyTorch cannot access GPU

Check:

    python -c "import torch; print(torch.cuda.is_available())"

If the result is `False`, verify:

- NVIDIA driver
- CUDA-compatible PyTorch installation
- GPU availability
- Runtime configuration

---

## Model file not found

Verify that the configured model path points to:

    best.pt

Do not assume that a model file exists simply because the repository contains the code.

The trained model may need to be obtained separately.

---

## Backend does not start

Check:

- Python environment
- Installed packages
- Correct module name
- Port availability
- Environment variables

Run the backend from the project directory.

---

## Frontend cannot reach backend

Check:

- Backend is running
- Backend URL is correct
- API endpoint is correct
- CORS configuration
- Frontend environment variables
- Firewall settings

---

# 29. Production Deployment

The development setup is not automatically equivalent to a production deployment.

A production deployment should additionally consider:

- HTTPS
- Authentication
- Authorization
- Secure secrets
- Database security
- File-upload limits
- Logging
- Monitoring
- Backup
- GPU resource management
- Rate limiting
- Error handling

---

# 30. Docker Deployment

A future production version can package the backend using Docker.

Conceptual structure:

    Docker Container
        |
        +-- Python Runtime
        +-- FastAPI
        +-- PyTorch
        +-- YOLOv8
        +-- OpenCV
        +-- Application Code

Docker can simplify deployment across compatible cloud, workstation and edge environments.

---

# 31. Edge Deployment

The lightweight YOLOv8n model provides a basis for future edge deployment.

Potential optimization methods include:

- ONNX
- TensorRT
- FP16
- Hardware-specific acceleration
- Image-size optimization

These optimizations require benchmarking on the target hardware before operational deployment.

---

# 32. AUV / ROV Deployment

The long-term deployment concept is:

    Side-Scan Sonar
          ↓
       AUV / ROV
          ↓
     Edge Compute
          ↓
      ATLANTIS AI
          ↓
       Detection
          ↓
    Evidence Analysis
          ↓
    Geospatial Context
          ↓
    Inspection Support

AUV / ROV onboard deployment is a future stage and requires hardware integration, field testing and validation.

---

# 33. Public Repository Policy

The public repository is intended to demonstrate the architecture and methodology of ATLANTIS.

It should contain:

- README
- Documentation
- Architecture diagrams
- Model performance summaries
- Sample outputs
- Non-sensitive examples
- Demo information

It should not contain:

- API keys
- Passwords
- Database credentials
- Private survey data
- Sensitive coordinates
- Proprietary datasets
- Private model weights
- Personal credentials

---

# 34. Recommended .gitignore

The repository should ignore sensitive and generated files such as:

    .env
    *.env
    *.key
    *.pem
    credentials.json
    service-account.json

    best.pt
    *.pt
    *.pth
    *.onnx
    *.engine

    __pycache__/
    *.pyc

    node_modules/
    .venv/
    venv/

    .ipynb_checkpoints/
    .DS_Store

Generated survey outputs should also be excluded where appropriate.

---

# 35. Development Status

| Component | Status |
|---|---|
| Model Development | Built & Validated |
| YOLOv8n Inference | Built & Validated |
| Multi-image Processing | Built & Validated |
| Detection Visualization | Built & Validated |
| Evidence Analysis | Built & Validated |
| JSON / CSV Output | Built & Validated |
| Dashboard Prototype | Built & Validated |
| Pipeline Detection | Prototyped / Integrating |
| Infrastructure Proximity | Prototyped / Integrating |
| Production API | Integration Stage |
| Edge Deployment | Next Stage |
| AUV / ROV Deployment | Next Stage |

---

# 36. Recommended Setup Workflow

For a new developer:

1. Clone the repository.
2. Create a Python virtual environment.
3. Install Python dependencies.
4. Configure environment variables.
5. Obtain model weights separately if authorized.
6. Verify the model environment.
7. Start the backend.
8. Test the API.
9. Install frontend dependencies.
10. Start the React frontend.
11. Connect the frontend to the backend.
12. Test a sample sonar image.
13. Verify annotated outputs.
14. Verify JSON results.
15. Test multi-image processing.

---

# 37. Important Note

The public repository represents the documented and shareable portion of ATLANTIS.

The complete private development environment may contain additional source code, model weights, datasets, deployment configuration and infrastructure that are intentionally not published.

The public repository should therefore be treated as a project showcase and technical documentation resource rather than a complete release of every private development asset.

---

## Project

**ATLANTIS — AI-Powered Underwater Debris & Subsea Infrastructure Intelligence**

**Smart India Hackathon 2026**

**Problem Statement:** 26057

**Team:** The Beatables
