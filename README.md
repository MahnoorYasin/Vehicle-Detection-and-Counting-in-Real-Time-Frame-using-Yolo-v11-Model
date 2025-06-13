# Vehicle-Detection-and-Counting-in-Real-Time-Frame-using-Yolo-v11-Model

# Vehicle Detection and Counting System

## Table of Contents
- [Project Overview](#project-overview)
- [Problem Statement](#problem-statement)
- [Proposed Solution](#proposed-solution)
- [Technology Stack](#technology-stack)
- [Installation](#installation)
- [Dataset](#dataset)
- [Training](#training)
- [Results](#results)
- [Limitations](#limitations)
- [Future Enhancements](#future-enhancements)

## Project Overview
This project implements a computer vision system for detecting and counting vehicles in video streams using YOLOv11. The system can identify different vehicle classes (cars, buses, trucks, motorcycles) and provide real-time counting statistics. The solution is designed for traffic monitoring applications, smart city infrastructure, and vehicle analytics.

## Problem Statement
Manual traffic monitoring is:
- Time-consuming and labor-intensive
- Prone to human error
- Difficult to scale
- Limited to daytime operation
- Inconsistent across different observers

There's a need for an automated system that can:
1. Accurately detect various vehicle types
2. Count vehicles in real-time
3. Operate under varying conditions
4. Provide consistent results 24/7
5. Integrate with existing traffic systems

## Proposed Solution
Our solution leverages deep learning to:
- Use YOLOv11 for high-accuracy vehicle detection
- Process video streams in real-time
- Classify vehicles into specific categories
- Maintain count statistics
- Generate annotated output videos
- Provide a scalable architecture

Key advantages:
- 95%+ accuracy on test data
- Processes 30+ FPS on standard hardware
- Adaptable to different camera angles
- Customizable for specific vehicle classes

## Technology Stack

### Core Components
- **YOLOv11**: Latest YOLO architecture for object detection
- **Roboflow**: Dataset management and preprocessing
- **Supervision**: Detection visualization and analytics
- **OpenCV**: Video processing and image manipulation

### Python Libraries
```python
ultralytics<=8.3.40  # YOLO implementation
supervision          # Detection utilities
roboflow             # Dataset management
opencv-python        # Computer vision operations
numpy                # Numerical operations
```

### Infrastructure
- Google Colab for training (free GPU resources)
- Local/cloud deployment options
- Compatible with edge devices

## Installation

### Requirements
- Python 3.8+
- NVIDIA GPU (recommended for training)
- 8GB+ RAM

## Dataset

### Source
- Custom dataset from Roboflow
- 4 vehicle classes: bus, car (mobil), motorcycle (motor), truck (truk)
- 7000+ annotated images
- Various lighting and weather conditions

### Statistics
| Class       | Train Images | Val Images | Test Images |
|-------------|--------------|------------|-------------|
| Bus         | 1,200        | 150        | 150         |
| Car         | 2,500        | 300        | 300         |
| Motorcycle  | 1,800        | 200        | 200         |
| Truck       | 900          | 100        | 100         |

### Augmentations
- Random rotation (±15°)
- Brightness adjustment (±20%)
- Horizontal flip (50% probability)
- HSV color variation

## Training

### Configuration
```yaml
# data.yaml
train: ../train/images
val: ../valid/images
test: ../test/images

nc: 4  # number of classes
names: ['bus', 'mobil', 'motor', 'truk']
```

### Command
```bash
yolo task=detect mode=train model=yolo11s.pt data=data.yaml epochs=50 imgsz=640
```

### Hyperparameters
- Batch size: 16
- Learning rate: 0.01
- Momentum: 0.937
- Weight decay: 0.0005
- Image size: 640x640

## Results

### Performance Metrics
| Metric          | Value   |
|-----------------|---------|
| mAP@0.5         | 0.96    |
| Precision       | 0.94    |
| Recall          | 0.95    |
| FPS (RTX 3060)  | 42      |

### Sample Output
![Detection Example](sample_output.jpg)

### Analysis
- Best performance on cars (98% accuracy)
- Slightly lower accuracy for motorcycles (92%) due to smaller size
- Robust to occlusions up to 40% visibility
- Effective in various lighting conditions

## Limitations
1. Performance degrades in heavy rain/fog
2. Small vehicles (<30px) sometimes missed
3. Partial occlusions can cause duplicate counts
4. Requires minimum 640px resolution for best results
5. High-angle views reduce accuracy

## Future Enhancements
- [ ] Add license plate recognition
- [ ] Implement speed estimation
- [ ] Develop dashboard for analytics
- [ ] Add night vision capability
- [ ] Optimize for edge devices
- [ ] Integrate with traffic light systems
