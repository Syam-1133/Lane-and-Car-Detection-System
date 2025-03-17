# 🚗 Lane and Car Detection System 🛣️

This project is a real-time lane and car detection system implemented using YOLOv8 for object detection and OpenCV for lane detection. The system processes video input, detects lane markings, identifies cars, and estimates their distance from the camera. It is designed to work with 720p video and maintains a frame rate of 30 FPS.

## ✨ Features

### 🚦 Lane Detection:
- Detects lane markings using Canny edge detection and Hough Line Transform.
- Draws a filled polygon between the detected lane lines to highlight the drivable area.
- Handles curved and straight lanes by fitting linear polynomials to the detected lines.

### 🚗 Car Detection:
- Uses YOLOv8 (You Only Look Once) to detect cars in the video frames.
- Draws bounding boxes around detected cars and displays their confidence scores.
- Estimates the distance of detected cars from the camera based on the bounding box size.

### ⏱️ Real-Time Processing:
- Processes video frames at 30 FPS for smooth real-time performance.
- Resizes input frames to 720p (1280x720) for consistent processing.

### 📏 Distance Estimation:
- Estimates the distance of detected cars using a simple inverse proportionality formula based on the bounding box width.
- Assumes a known car width and focal length for distance calculation.

## 🛠️ How It Works

### 🚦 Lane Detection Pipeline

#### 🎯 Region of Interest (ROI) Masking:
- The input frame is masked to focus only on the region where lane markings are likely to appear (e.g., the lower half of the frame).

#### 🔍 Edge Detection:
- The frame is converted to grayscale, and Canny edge detection is applied to identify edges in the image.

#### 📏 Line Detection:
- Hough Line Transform is used to detect lines in the edge-detected image.
- Lines are classified as left or right lane markers based on their slopes.

#### 🛣️ Lane Line Fitting:
- Linear polynomials are fitted to the detected left and right lane lines.
- A filled polygon is drawn between the lane lines to highlight the drivable area.

### 🚗 Car Detection and Distance Estimation

#### 🔎 YOLOv8 Object Detection:
- The YOLOv8 model is used to detect cars in the frame.
- Bounding boxes are drawn around detected cars, and their confidence scores are displayed.

#### 📏 Distance Estimation:
- The width of the bounding box is used to estimate the distance of the car from the camera.
- The formula `distance = (known_width * focal_length) / bbox_width` is used for estimation.

### ⏱️ Real-Time Video Processing

#### ⏳ Frame Rate Control:
- The system ensures a consistent frame rate of 30 FPS by introducing a delay between frames.

#### 🖼️ Frame Resizing:
- Input frames are resized to 720p (1280x720) for consistent processing and display.

#### 🕹️ User Interaction:
- The user can exit the application by pressing the `q` key.

## 📋 Requirements
- Python 3.10
- OpenCV (`cv2`)
- NumPy (`numpy`)
- Ultralytics YOLOv8 (`ultralytics`)

## 🛠️ Installation

### Clone the repository:
```bash
git clone https://github.com/Syam-1133/Lane-and-Car-Detection-System
```

### Install the required dependencies:
```bash
pip install opencv-python numpy ultralytics
```

### Download the YOLOv8 weights file (`yolov8n.pt`) and place it in the `weights` folder.
### Place your input video file (`car.mp4`) in the `video` folder.

## 🚀 Usage

Run the script to process the video:
```bash
python main.py
```

The system will display the processed video with lane detection, car detection, and distance estimation.

Press `q` to exit the application.

## 🛠️ Customization

### 📏 Focal Length and Known Width:
- Modify the `focal_length` and `known_width` values in the `estimate_distance` function for accurate distance estimation based on your camera setup.

### 🎯 Region of Interest:
- Adjust the `region_of_interest_vertices` in the `pipeline` function to match the road geometry in your video.

### 🔍 YOLOv8 Model:
- Replace `yolov8n.pt` with other YOLOv8 models (e.g., `yolov8s.pt`, `yolov8m.pt`) for different trade-offs between speed and accuracy.

## ⚠️ Limitations

### 📏 Distance Estimation:
- The distance estimation is based on a simple formula and may not be accurate without proper camera calibration.

### 🛣️ Lane Detection:
- The system assumes straight or slightly curved lanes. It may not perform well on highly curved or complex road layouts.

### ⏱️ Real-Time Performance:
- Performance may vary depending on the hardware and input video resolution.


## 📝 License
This project is licensed under the MIT License. See the `LICENSE` file for details.
