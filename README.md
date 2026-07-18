# Warehouse Forklift Safety Intelligence System

This project is a computer-vision-based warehouse safety analyzer that processes video footage to detect workers and forklifts, track their motion over time, and identify potentially dangerous situations such as near-misses, high-risk proximity, and zone intrusions.

The system is built around a YOLOv8 object detection model and a custom tracking and safety analysis pipeline implemented in Python. It produces an annotated output video, a JSON event log, and a dashboard image for post-analysis review.

## What the System Does

The pipeline performs the following steps:

1. Loads a video file from the project directory or from a supplied file path.
2. Detects objects in each frame using YOLOv8.
3. Classifies detections as workers and forklifts.
4. Tracks objects across frames to maintain identity over time.
5. Calculates relative distances between workers and forklifts.
6. Flags safety events such as:
   - high-risk proximity
   - medium-risk proximity
   - low-risk proximity
   - zone intrusions
7. Writes the processed video and analytics outputs to disk.

## Main Features

- Detects people and vehicles using YOLOv8
- Tracks multiple workers and forklifts simultaneously
- Computes proximity-based risk levels
- Draws bounding boxes, motion trails, and safety overlays on the output video
- Visualizes analytics in a dashboard image
- Saves a structured event log as JSON
- Automatically installs missing Python dependencies when needed

## Project Structure

- `warehouse.py` — main script for loading the video, running detection, tracking, analysis, and output generation
- `input1.mp4` — example input video file
- `yolov8n.pt` — YOLOv8 nano model weights
- `warehouse_output/` — directory containing generated outputs
- `warehouse_safety_OUTPUT.mp4` — annotated output video
- `warehouse_safety_DASHBOARD.png` — analytics dashboard image
- `safety_events.json` — detected safety event log

## Requirements

A working Python environment is required. The script can attempt to install missing dependencies automatically, but it is recommended to have the following packages available:

- `opencv-python`
- `numpy`
- `matplotlib`
- `ultralytics`
- `torch`
- `torchvision`
- `Pillow`
- `scipy`
- `tqdm`

## Installation

1. Open a terminal in the project directory.
2. Create and activate a Python environment if desired.
3. Install dependencies with:

```bash
pip install opencv-python numpy matplotlib ultralytics torch torchvision Pillow scipy tqdm
```

If you are using the provided script directly, it may install missing packages automatically when you run it.

## Usage

Run the script from the project folder:

```bash
python warehouse.py
```

The program will automatically look for a supported video file in the current directory. If you want to use a specific file, pass it as an argument:

```bash
python warehouse.py your_video.mp4
```

## How It Works

The script uses a YOLOv8 model to detect objects in every frame. Detections are converted into tracking objects, and the system estimates whether detected workers are close to forklifts. Depending on their distance, the system assigns a risk level and records an event if needed.

It also overlays zones on the frame and can mark when workers enter restricted or high-risk areas. The output video contains these visual annotations so a reviewer can quickly inspect the scene.

## Output Files

When the script finishes successfully, it generates:

- `warehouse_safety_OUTPUT.mp4` — a processed video with boxes, zones, motion trails, and safety annotations
- `warehouse_safety_DASHBOARD.png` — a summary dashboard with charts and safety metrics
- `safety_events.json` — a JSON list of detected events with timestamps and descriptions

## Configuration

The behavior of the pipeline can be adjusted in the configuration dictionary near the top of `warehouse.py`. Common settings include:

- model confidence threshold
- IoU threshold for tracking
- maximum track age
- risk-distance thresholds
- output file names
- HUD and heatmap settings

These parameters influence detection strictness, tracking stability, and event sensitivity.

## Notes

- The script auto-detects common video filenames such as `warehouse.mp4`, `forklift.mp4`, or any supported video file in the current folder.
- The default model is `yolov8n.pt`, which is lightweight and suitable for general use.
- Processing time depends on video length, resolution, and hardware performance.
- For long videos, expect the run to take several minutes.

## Example

```bash
python warehouse.py input1.mp4
```

This will process the supplied video and produce the annotated output files in the project folder.

## Troubleshooting

If the script fails to open the video:

- ensure the file exists in the current folder or provide it explicitly
- confirm the file uses a supported format such as `.mp4`, `.avi`, `.mov`, or `.mkv`

If model loading fails:

- verify that the internet connection is available for the first download of YOLO weights
- confirm the `ultralytics` package is installed correctly

If output files are not created:

- inspect the terminal output for errors
- verify that the script has permission to write files in the project directory
