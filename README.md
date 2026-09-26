# SONARX — AI-Based Debris Detection in Sonar Images

SONARX is a Streamlit prototype for detecting objects in sonar imagery using a YOLO object-detection model.

## Current prototype

- **Application:** Streamlit
- **Computer vision:** Ultralytics YOLO
- **Model:** `models/debris.pt`
- **Current classes:** `ship`, `plane`
- **Input:** JPG/JPEG/PNG images
- **Output:** annotated image, detected class, confidence, bounding-box coordinates, width, height, and area

> **Important:** The current model is a closed-set prototype. It should not be interpreted as a general-purpose detector for every type of marine debris or as a safety-critical autonomous decision system.

## Repository structure

```text
SONARX/
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
├── models/
│   └── debris.pt
└── notebooks/
    └── training.ipynb
```

## Run locally

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd SONARX
```

### 2. Create a virtual environment (recommended)

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Start the application

```bash
streamlit run app.py
```

The app will open in your browser. Upload a sonar image and adjust the detection-confidence threshold.

## Model training

The included notebook documents the current YOLO training workflow. The prototype training configuration uses:

- YOLOv8 nano (`yolov8n.pt`)
- 50 epochs
- image size: 416
- batch size: 16
- GPU training

The original dataset is **not included** in this repository. Add the dataset separately if you have permission to redistribute it.

## Roadmap

1. Expand beyond the current `ship` and `plane` classes.
2. Add unknown-object / anomaly detection for previously unseen sonar objects.
3. Add input-domain/OOD validation so non-sonar images are rejected.
4. Investigate segmentation for precise object boundaries.
5. Associate detections with location, depth and timestamp in a future AUV/ROV deployment.
6. Add human verification for uncertain or high-risk detections.
7. Explore edge deployment on suitable embedded hardware.

## Safety and research note

A high confidence score is not proof that a prediction is correct, especially for out-of-distribution inputs. SONARX is intended as an AI-assisted research prototype and decision-support concept. Critical operational actions should require independent verification.
