
# Tennis Analysis

## Introduction
This project analyzes Tennis players in a video to measure their speed, ball shot speed and number of shots. This project will detect players and the tennis ball using YOLO and also utilizes CNNs to extract court keypoints.

## Output Videos
Here is a screenshot from one of the output videos:

![Screenshot](output_videos/screenshot.jpeg)

## Models Used
* YOLO v8 for player detection
* Fine Tuned YOLO for tennis ball detection
* Court Key point extraction

* Trained YOLOV5 model: https://drive.google.com/drive/folders/1BkTC3iXvVrk5X9Btpn_VYVDard0hpuLb
* Trained tennis court key point model: https://drive.google.com/drive/folders/1BkTC3iXvVrk5X9Btpn_VYVDard0hpuLb

## Training
* Tennis ball detetcor with YOLO: training/tennis_ball_detector_training.ipynb
* Tennis court keypoint with Pytorch: training/tennis_court_keypoints_training.ipynb

## Complete Flow of the Project

1. Model Training and Fine-tuning

Fine-tuned a YOLOv5 model on a specialized tennis ball detection dataset, which comprises images of tennis courts along with annotated bounding boxes indicating the precise locations of tennis balls within the frames. This fine-tuning process aimed to enhance the model's accuracy in detecting tennis balls.

Trained a ResNet-50 model on a tennis court keypoint detection dataset to accurately identify and extract key points of the court from images. This training process aimed to enhance the model's ability to detect court keypoints.

2. Video Processing Pipeline

a. Read Input Video

Load the input video file for processing.

b. Initialize Trackers

Create PlayerTracker and BallTracker objects.

c. Detect Players and Ball

Detect players using player_tracker.detect_frames

Detect ball using ball_tracker.detect_frames

Interpolate ball positions with ball_tracker.interpolate_ball_positions

d. Load Model and Predict Keypoints

Use the trained ResNet-50 model to predict keypoints on the tennis court.

e. Choose and Filter Players

Select relevant players from detected player instances.

f. Initialize MiniCourt

Define and set up a miniature version of the tennis court for easier coordinate transformations.

g. Identify Shot Frames

Detect frames where shots occur.

h. Convert Coordinates to MiniCourt

Transform real-world coordinates into MiniCourt coordinates.

i. Initialize Player Stats

Set up data structures to store player performance statistics.

3. Shot Analysis Loop

Loop over ball shots and for each shot:

Compute shot speed.

Identify the player who hit the ball and the opponent.

Calculate the opponent's speed.

Update player statistics accordingly.

4. Prepare DataFrame with Player Stats

Convert player statistics into a structured DataFrame.

Fill missing values.

Calculate averages for shot and player speeds.

5. Draw Annotations on Video Frames

Draw player and ball bounding boxes.

Give it in the format of README

This project implements automated tennis tracking using deep learning models to detect players, track ball movement, and analyze player performance efficiently.



## Requirements
* python3.8
* ultralytics
* pytroch
* pandas
* numpy 
* opencv
