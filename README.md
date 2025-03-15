
# Tennis Match Video Analysis

## Introduction
This Project **detects** the **tennis ball** as well as **tracks** the **players** across the whole video. It also **detects** the **courts keypoints** to know the players positions relative to the court. It calculates **shot count** and **shot speed**. It also measures the **player speed** and how many meters the player covered. 2 convolutional neural networks is trained in this project. The first one is **YOLO** an object detection model to detect fast moving tennis ball to enhance the detection accuracy of the out of the box models. The other one is a **resnet50** that is trained to estimate the courts keypoints. 

## Output
Here is a screenshot from one of the output videos:

![Screenshot](output_videos/screenshot.jpeg)

## Models Used
* Used YOLOv8 for player detection.
* Fine Tuned YOLOv5 on tennis ball detection dataset.
* Used resnet50 for Court Key point extraction.

* Trained YOLOV5 model: https://drive.google.com/drive/folders/1BkTC3iXvVrk5X9Btpn_VYVDard0hpuLb
* Trained tennis court key point model: https://drive.google.com/drive/folders/1BkTC3iXvVrk5X9Btpn_VYVDard0hpuLb

## Training
* Tennis ball detetcor with YOLO: training/tennis_ball_detector_training.ipynb
* Tennis court keypoint with Pytorch: training/tennis_court_keypoints_training.ipynb

## TennisCourtDetector
Deep learning network for detecting tennis court

It was developed a deep learning network to detect tennis court keypoints from broadcast videos. The proposed heatmap-based deep learning
network allows to detect 14 points of tennis court. Postprocessing techniques (based on classical computer vision methods) were implemented to enhance 
net predictions.

![](imgs/dataset_example.png)

## Dataset
The dataset consists of 8841 images, which were separeted to train set (75%) and validation set (25%). Each image has 14 annotated points. 
The resolution of images is 1280×720. This dataset contains all court types (hard, clay, grass). Click the link 
https://drive.google.com/file/d/1lhAaeQCmk2y440PmagA0KmIVBIysVMwu/view?usp=drive_link to download the dataset

### Dataset collection
This dataset was created in semi-automated way. Video highlights from different tournaments with length from 2 to 3 minutes were downloaded from YouTube. 
Frames from video were extracted with step 50 frames to run them through classical computer vision algorithm. The quality of existing computer vision 
algorithm is not good therefore the resulting images were filtered manually.    

## Model architecture
Proposed deep learning network is very similar to TrackNet architecture. 
![](imgs/tracknet_arch.png) 
<br> The difference is that input tensor consists of just 1 image (instead of 3 in TrackNet) and output tensor has 15 channels (14 from dataset and one additional
point is center of tennis court). We used additional point for better convergence. The resolution of input and output image is 640x360.

## Complete Flow of the Project

* **Model Training and Fine-tuning**

  Fine-tuned a YOLOv5 model on a specialized tennis ball detection dataset, which comprises images of tennis courts along with annotated bounding boxes indicating the precise locations of tennis balls within the frames. This fine-tuning process aimed to enhance the model's accuracy in detecting tennis balls.

  Trained a ResNet-50 model on a tennis court keypoint detection dataset to accurately identify and extract key points of the court from images. This training process aimed to enhance the model's ability to detect court keypoints.

* **Video Processing Pipeline**

  a. Read Input Video

  - Load the input video file for processing.

  b. Initialize Trackers

  - Create PlayerTracker and BallTracker objects.

  c. Detect Players and Ball

    - Detect players using player_tracker.detect_frames

    - Detect ball using ball_tracker.detect_frames

    - Interpolate ball positions with ball_tracker.interpolate_ball_positions

  d. Load Model and Predict Keypoints

    - Use the trained ResNet-50 model to predict keypoints on the tennis court.

  e. Choose and Filter Players

    - Select relevant players from detected player instances.

  f. Initialize MiniCourt

    - Define and set up a miniature version of the tennis court for easier coordinate transformations.

  g. Identify Shot Frames

    - Detect frames where shots occur.

  h. Convert Coordinates to MiniCourt

    - Transform real-world coordinates into MiniCourt coordinates.

  i. Initialize Player Stats

    - Set up data structures to store player performance statistics.

* **Shot Analysis Loop**

  - Loop over ball shots and for each shot:

    - Compute shot speed.

    - Identify the player who hit the ball and the opponent.

    - Calculate the opponent's speed.

    - Update player statistics accordingly.

* **Prepare DataFrame with Player Stats**

  - Convert player statistics into a structured DataFrame.

  - Fill missing values.

  - Calculate averages for shot and player speeds.

* **Draw Annotations on Video Frames**

  - Draw player and ball bounding boxes.

  - Give it in the format of README

  - This project implements automated tennis tracking using deep learning models to detect players, track ball movement, and analyze player performance efficiently.

## Requirements
* python3.8
* ultralytics
* pytroch
* pandas
* numpy 
* opencv
