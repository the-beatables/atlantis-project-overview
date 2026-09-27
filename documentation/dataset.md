# ATLANTIS — Dataset Documentation

## AI-Powered Underwater Debris & Subsea Infrastructure Intelligence

**Smart India Hackathon 2026 | Problem Statement 26057 | Team The Beatables**

---

## 1. Dataset Overview

ATLANTIS uses Side-Scan Sonar (SSS) imagery for underwater object detection and analysis.

The project currently uses two major dataset components:

| Dataset Component | Purpose | Status |
|---|---|---|
| Marine Debris Dataset | Shipwreck, Pipe, Ghost Net, Rock / Seafloor Clutter detection | Built & Validated |
| SubPipe Dataset | Subsea pipeline detection | Prototyped / Integrating |

The datasets are used independently because marine-debris detection and infrastructure detection represent different detection tasks.

---

## 2. Marine Debris Dataset

The core ATLANTIS detection model was trained on a Side-Scan Sonar dataset containing:

| Parameter | Value |
|---|---:|
| Total Images | 7,756 |
| Training Images | 5,429 |
| Validation Images | 1,163 |
| Test Images | 1,164 |
| Dataset Split | 70 / 15 / 15 |
| Number of Classes | 4 |

The dataset was split into training, validation and test subsets for model development and evaluation.

---

## 3. Marine Debris Classes

The core YOLOv8n model contains four classes.

| Class ID | Class |
|---:|---|
| 0 | Shipwreck |
| 1 | Pipe |
| 2 | Ghost Net |
| 3 | Rock / Seafloor Clutter |

### Shipwreck

Represents man-made wreckage or shipwreck-like objects visible in Side-Scan Sonar imagery.

### Pipe

Represents pipe-like objects identified in the sonar dataset.

### Ghost Net

Represents abandoned or lost fishing-net structures.

### Rock / Seafloor Clutter

Represents natural seabed structures that may produce sonar signatures similar to potential targets.

This class is important because distinguishing natural seafloor clutter from man-made objects is part of reducing unnecessary false positives.

---

## 4. Dataset Distribution

The training dataset contains an uneven distribution of object annotations.

The recorded training annotation counts are:

| Class | Training Boxes |
|---|---:|
| Shipwreck | 573 |
| Pipe | 302 |
| Ghost Net | 6,452 |
| Rock / Seafloor Clutter | 0 |

The dataset also contains images without object annotations.

Approximately **1,297 training images** were recorded with empty labels in the training set.

This class imbalance is an important consideration when interpreting model performance.

---

## 5. Dataset Splits

The dataset uses the following split:

    7,756 Images
         |
    +----+----+
    |    |    |
    ↓    ↓    ↓
   TRAIN VAL TEST
   5429 1163 1164
    70%  15%  15%

The validation set is used for model evaluation during development.

The test set is kept separate for final evaluation and future benchmarking.

---

## 6. Data Quality Checks

The dataset preparation process included validation of image and annotation files.

The following checks were considered:

- Image availability
- Label availability
- Annotation format
- Bounding-box validity
- Class IDs
- Dataset split consistency
- Empty-label identification

Invalid annotation records were removed or excluded from the final training workflow where applicable.

---

## 7. YOLO Annotation Format

The marine-debris dataset uses YOLO-style object-detection annotations.

Each object annotation follows the structure:

    class_id x_center y_center width height

The coordinates are normalized relative to the image dimensions.

Example:

    2 0.534 0.421 0.184 0.216

This represents:

    Class ID  → 2
    X Center  → 0.534
    Y Center  → 0.421
    Width     → 0.184
    Height    → 0.216

---

## 8. Marine Debris Model

The marine-debris dataset is used to train the core:

**YOLOv8n detector**

Training configuration:

| Parameter | Value |
|---|---:|
| Model | YOLOv8n |
| Input Size | 640 × 640 |
| Epochs | 75 |
| Batch Size | 32 |
| Total Images | 7,756 |
| Model Size | ~5.95 MB |

The resulting model is designed to provide a lightweight first-stage detector.

---

## 9. Marine Debris Model Results

The current validation results are:

| Metric | Result |
|---|---:|
| Precision | 80.5% |
| Recall | 80.4% |
| mAP@50 | 82.2% |
| mAP@50–95 | 68.9% |

These values represent the current validation performance of the trained marine-debris model.

The values should not be interpreted as general performance across all Side-Scan Sonar systems or operating environments.

---

## 10. SubPipe Dataset

A separate dataset is used for the pipeline-detection component.

The project uses the **SubPipe** dataset for developing the subsea pipeline detection module.

The dataset is based on real pipeline inspection data collected using an autonomous underwater vehicle and Side-Scan Sonar.

The dataset provides annotated pipeline targets suitable for object-detection research.

---

## 11. SubPipe Dataset Overview

The full SubPipe dataset contains approximately:

| Parameter | Value |
|---|---:|
| Total SSS Images | 10,030 |
| Total Annotations | 6,335 |
| Low Frequency Images | 5,000 |
| High Frequency Images | 5,030 |
| Annotation Type | Object Detection |
| Target | Subsea Pipeline |

The project also used a smaller subset for development and experimentation.

---

## 12. SubPipe Development Subset

The extracted development subset used in the project contains approximately:

| Parameter | Value |
|---|---:|
| Total Images | 2,066 |
| Label Files | 1,365 |
| Bounding Boxes | 1,422 |

The subset contains both low-frequency and high-frequency Side-Scan Sonar imagery.

The pipeline target is represented using bounding-box annotations.

---

## 13. Pipeline Dataset Structure

The processed pipeline dataset follows a YOLO-compatible directory structure.

    pipeline_dataset/
    |
    +-- images/
    |   +-- train/
    |   +-- val/
    |   +-- test/
    |   +-- extra_test/
    |
    +-- labels/
    |   +-- train/
    |   +-- val/
    |   +-- test/
    |   +-- extra_test/
    |
    +-- data.yaml

The pipeline dataset contains a single primary object class:

    0 → pipeline

---

## 14. Pipeline Dataset Split

The development subset was separated into training, validation and test groups.

Approximate distribution:

| Split | Images | Label Files |
|---|---:|---:|
| Train | 1,413 | 976 |
| Validation | 302 | 60 |
| Test | 301 | 301 |
| Extra Test | 50 | 28 |

The split was designed to preserve temporal separation between survey segments where applicable.

This reduces the risk of evaluating visually adjacent frames from the same survey segment as completely independent observations.

---

## 15. Why Separate Models Are Used

The marine-debris detector and pipeline detector are maintained as separate modules.

The architecture is:

    SSS IMAGE
        |
        +-----------------------------+
        |                             |
        ↓                             ↓
    MARINE DEBRIS AI          INFRASTRUCTURE AI
       YOLOv8n                   Pipeline Model
        |                             |
        ↓                             ↓
    Shipwreck / Pipe /          Pipeline / Structure
    Ghost Net / Clutter
        |                             |
        +-------------+---------------+
                      |
                      ↓
              SPATIAL ANALYSIS
                      |
                      ↓
               RISK PRIORITY

This modular design allows each model to be trained on task-specific data.

It also allows future infrastructure models, such as cable detection, to be added independently.

---

## 16. Dataset Limitations

### Class Imbalance

The marine-debris dataset has a strong imbalance between object classes.

Ghost-net annotations form the largest portion of the annotated training objects.

### Rock-Clutter Annotations

The rock-clutter class does not currently have annotated instances in the validation metrics used for the reported model results.

Therefore, its real-world detection performance cannot be inferred from the reported validation metrics.

### Dataset Diversity

Performance can vary depending on:

- Sonar frequency
- Sensor configuration
- Seabed type
- Water conditions
- Object orientation
- Object size
- Imaging geometry
- Survey environment

A model trained on one dataset should therefore be validated on representative operational data before deployment.

---

## 17. Data Leakage Considerations

Side-Scan Sonar surveys can contain temporally adjacent images that are visually correlated.

For infrastructure datasets, splitting data randomly can result in highly similar frames appearing in both training and validation sets.

Where possible, ATLANTIS uses temporal or survey-segment-based separation for infrastructure data to reduce this issue.

Future evaluation should continue to prioritize:

- Survey-level separation
- Location-level separation
- Temporal separation
- Independent external test datasets

---

## 18. Dataset Expansion

Future dataset development will focus on increasing diversity and reducing class imbalance.

Potential additions include:

- More shipwreck examples
- More pipeline examples
- More ghost-net examples
- More natural seafloor clutter
- Cable targets
- Different sonar frequencies
- Different seabed environments
- Different object orientations
- Different survey platforms

The objective is to improve generalization across different sonar systems and marine environments.

---

## 19. Future Dataset Requirements

For future pipeline and cable condition analysis, additional labelled data would be required.

Potential labels could include:

    Pipeline
    Cable
    Exposed Pipeline
    Buried Pipeline
    Free Span
    Potential Anomaly
    Damaged / Irregular Segment
    Debris Near Infrastructure

These classes are part of the proposed future dataset structure and are not currently claimed as fully trained classes in ATLANTIS.

---

## 20. Dataset Sources

### Marine Debris Dataset

The marine-debris dataset used for the core ATLANTIS model is maintained as part of the project development environment.

The trained model and raw dataset are not included in the public repository.

### SubPipe Dataset

SubPipe is an external research dataset used for pipeline-detection development.

**Dataset:** SubPipe — Side-Scan Sonar Pipeline Dataset

**Zenodo:**  
https://zenodo.org/records/10808161

**GitHub:**  
https://github.com/remaro-network/SubPipe-dataset

The project should follow the dataset's applicable attribution, licensing and redistribution requirements.

---

## 21. Data Privacy & Repository Policy

Large datasets and trained model weights are not included in the public ATLANTIS repository.

The public repository contains:

- Dataset descriptions
- Methodology
- Model configuration
- Performance summaries
- Sample outputs
- Documentation

The following should remain outside the public repository unless their redistribution is explicitly permitted:

- Raw proprietary survey data
- Sensitive geographic coordinates
- Private datasets
- API keys
- Database credentials
- Trained model weights
- Private infrastructure data

---

## 22. Reproducibility

The project documentation records the main dataset and training parameters required to understand the current model.

For reproducible experiments, future releases should record:

- Dataset version
- Dataset split
- Model version
- Training configuration
- Random seed
- Software versions
- Hardware configuration
- Evaluation metrics

This helps ensure that future model versions can be compared against previous experiments.

---

## 23. Recommended Future Benchmarking

Future evaluation should include independent test sets collected from:

- Different survey locations
- Different sonar systems
- Different seabed conditions
- Different object orientations
- Different sonar frequencies

Evaluation should include:

- Precision
- Recall
- mAP@50
- mAP@50–95
- False-positive rate
- False-negative rate
- Inference latency
- Model size
- Edge-device performance

For operational deployment, field validation should be performed using representative survey data.

---

## 24. Summary

ATLANTIS currently uses two complementary dataset tracks:

    MARINE DEBRIS DATASET
            |
          YOLOv8n
            |
    Shipwreck • Pipe • Ghost Net • Rock / Clutter

and:

    SUBPIPE DATASET
            |
    PIPELINE DETECTION MODEL
            |
      Subsea Pipeline Detection

These components are combined at the system level to enable future infrastructure-aware analysis.

The dataset architecture is intentionally modular so that additional classes, survey environments and infrastructure types can be incorporated as the project develops.

---

## Project

**ATLANTIS — AI-Powered Underwater Debris & Subsea Infrastructure Intelligence**

**Smart India Hackathon 2026**

**Problem Statement:** 26057

**Team:** The Beatables
