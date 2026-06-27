# CivicLens — AI-Powered Civic Issue Detection System

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-2.x-lightgrey?logo=flask&logoColor=white)
![YOLOv5](https://img.shields.io/badge/YOLOv5-PyTorch-orange?logo=pytorch&logoColor=white)
![License](https://img.shields.io/badge/License-AGPL--3.0-green)

> A full-stack web application that uses YOLOv5 object detection to automatically identify and classify civic infrastructure issues from uploaded images, enabling citizens to report problems and administrators to manage resolutions.

![CivicLens App Screenshot](Images/Screenshot%202026-03-17%20225103.png)

---

## Overview

CivicLens bridges the gap between citizen reporting and municipal response by combining computer vision with a complaint management portal. Users upload photos of civic issues; the YOLOv5 model detects and classifies the problem in real time, and the result is logged for admin review and action.

---

## Features

- **AI-Powered Detection** — Custom-trained YOLOv5 model (`best.pt`) identifies 6 civic issue categories directly from uploaded images
- **Citizen Portal** — Register, log in, submit complaints with photos, and track status
- **Admin Dashboard** — View all complaints, update status, manage users, and delete records
- **Image Upload & Storage** — Secure file handling with extension validation and size limits (16 MB)
- **Role-Based Access** — Separate citizen and admin views with session-based authentication
- **Responsive UI** — Flask-rendered templates with mobile-friendly session handling

---

## Detected Issue Classes

| Class ID | Label |
|----------|-------|
| 0 | Broken Streetlight |
| 1 | Damaged Footpath / Sidewalk |
| 2 | Flood |
| 3 | Garbage |
| 4 | Open Manhole |
| 5 | Sewage Leak |
| 6 | Water Leakage |

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Computer Vision | YOLOv5 (Ultralytics), PyTorch |
| Backend | Python, Flask |
| Database | SQLite |
| Auth | Werkzeug password hashing, Flask sessions |
| Training | Google Colab, custom dataset (640×640, 250 epochs) |
| Frontend | HTML/CSS (Jinja2 templates) |

---

## Project Structure

```
CivicLens/
├── app.py                  # Flask application & routes
├── best.pt                 # Trained YOLOv5 weights
├── data.yaml               # Dataset config (classes & paths)
├── classes.py              # Class name extraction utility
├── benchmarks.py           # Model benchmarking script
├── detect.py               # Detection runner script
├── export.py               # Model export utility
├── database.db             # SQLite database
├── Images/                 # App screenshots
├── models/                 # YOLOv5 model architecture files
├── runs/                   # Training & inference output logs
├── segment/                # Segmentation utilities
├── static/                 # CSS, JS, uploaded files
├── templates/              # Jinja2 HTML templates
├── utils/                  # Helper utilities
├── classify/
│   ├── predict.py          # Inference script
│   ├── train.py            # Training script
│   ├── val.py              # Validation script
│   └── tutorial.ipynb      # Training walkthrough notebook
└── dataset/
    └── train/img/          # Labelled training images
```

---

## Setup & Installation

```bash
# Clone the repository
git clone https://github.com/Srushti857/Major-Project.git
cd Major-Project

# Install dependencies
pip install flask werkzeug torch torchvision

# Run the application
python app.py
```

Visit `http://localhost:5000` in your browser.

---

## Model Training

The YOLOv5 model was trained on a custom dataset of civic infrastructure images using Google Colab:

```bash
python train.py --img 640 --batch 16 --epochs 250 \
    --data data.yaml --weights yolov5s.pt
```

The trained weights (`best.pt`) are included in the repository for direct inference.

---

## Key Learnings

- Custom object detection pipeline from data collection to deployment
- Flask full-stack development with role-based access control
- SQLite schema design for complaint tracking workflows
- YOLOv5 fine-tuning on domain-specific image datasets

---

## Acknowledgements

YOLOv5 architecture by [Ultralytics](https://github.com/ultralytics/yolov5) — Glenn Jocher et al., 2020. DOI: [10.5281/zenodo.3908559](https://doi.org/10.5281/zenodo.3908559)