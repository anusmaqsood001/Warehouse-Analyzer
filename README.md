# Warehouse Forklift Safety Intelligence System

This project analyzes a warehouse video to detect workers and forklifts, track movement, and flag safety risks such as near-misses, high-risk proximity, and zone intrusions...

## Features

- Detects people and vehicles using YOLOv8
- Tracks workers and forklifts across frames
- Identifies potential safety hazards in real time
- Generates:
  - an annotated output video
  - a safety event log in JSON
  - a dashboard image with analytics

## Requirements

The script will try to install missing dependencies automatically, but a working Python environment is still required.

Required packages include:
- opencv-python
- numpy
- matplotlib
- ultralytics
- torch
- torchvision
- Pillow
- scipy
- tqdm

## Project Files

- `warehouse.py` — main processing script
- `input1.mp4` — example input video
- `yolov8n.pt` — YOLO model weights
- `warehouse_output/` — generated output files

## Usage

1. Place your video file in the project folder.
2. Run the script:

```bash
python warehouse.py
```

If you want to use a specific video file, pass it as an argument:

```bash
python warehouse.py your_video.mp4
```

## Outputs

After running the script, the following files are created:

- `warehouse_safety_OUTPUT.mp4` — annotated output video
- `warehouse_safety_DASHBOARD.png` — analytics dashboard
- `safety_events.json` — detected safety events

## Notes

- The script auto-detects video files in the current folder.
- It uses the YOLOv8n model by default.
- Processing may take some time depending on video length and hardware.
