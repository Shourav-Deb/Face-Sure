<p align="center">
  <img src="https://i.pinimg.com/originals/77/d2/f8/77d2f8422167b7357cf4c0fc06a9a3cf.png" width="220" alt="Face Sure Logo"/>
</p>

<h1 align="center"><b>Face Sure</b></h1>

<p align="center">
  <b>A Deepfake Video Analyzer</b><br/>
  <i>Detecting deepfake-based cyber threats using deep learning and web deployment</i>
</p>

## 🔍 Overview

**Face Sure** is a deepfake detection system designed to identify manipulated videos that pose cyber-security threats such as identity impersonation, misinformation, and social engineering attacks.

The project focuses on **video-level deepfake detection**, combining:
- A deep learning model trained on the **FaceForensics++ dataset**
- A **real-time, web-based interface** for video analysis
- A deployment-ready pipeline suitable for practical cyber-defense use cases



## 🎯 Key Objectives

- Detect deepfake videos instead of isolated images  
- Use a modern, efficient deep learning model  
- Provide a user-friendly web interface for real-time analysis  
- Bridge the gap between academic research and real-world deployment  



## 📂 Dataset

- **Dataset:** [FaceForensics++ (FF++) - C23](https://www.kaggle.com/datasets/xdxd003/ff-c23) compression
- **Content:**  
  - Real videos  
  - Manipulated videos:
    - DeepFakes  
    - Face2Face  
    - FaceSwap  
    - FaceShifter  
    - NeuralTextures  

### Dataset Choice Rationale
- Industry-standard benchmark for deepfake research
- Realistic compression similar to social media platforms
- Widely used in foundational deepfake detection papers

> ⚠️ Note:  
> Instead of extracting and cropping faces manually, this project uses an **already face-cropped version of the [FaceForensics++ Dataset](https://www.kaggle.com/datasets/fatimahirshad/faceforensics-c32-frames-cropped-aligned)**, significantly reducing preprocessing complexity while maintaining dataset integrity.

## 🧠 Model Architecture

### Implemented Model
- **EfficientNet-B0**

### Why EfficientNet-B0?
- High accuracy with low computational cost
- More efficient than older architectures (e.g., XceptionNet)
- Suitable for real-time inference and web deployment
- Proven performance in recent deepfake detection research

### Classification Setup
The model is trained as a **6-class classifier**:

- Deepfakes  
- Face2Face  
- FaceShifter  
- FaceSwap  
- NeuralTextures  
- Original  

A final **binary decision (Real vs Fake)** is derived at video level using probability aggregation.

> ⚠️ Note:
> The training notebook is structured to support multiple architectures, but **only EfficientNet-B0 was fully trained, evaluated, and deployed** in this implementation.


## 📊 Evaluation Strategy

### Frame-Level Evaluation
- Accuracy
- Precision
- Recall
- Confusion Matrix


### Video-Level Decision (Core Contribution)

Since real-world attacks occur via videos, the system performs:
1. Frame sampling from uploaded video  
2. Frame-wise model prediction  
3. Probability aggregation across frames  
4. Final decision using:

## 🚀 Running the Project Web Application

The **[Face Sure](https://face-sure.streamlit.app)** web application is deployed online and can be accessed directly without any local setup.

### 1️⃣ Open the Website

Visit the live application using the link above.

You will see:
- Face Sure branding
- Detection controls (sliders)
- Video upload section

No login or installation is required.


### 2️⃣ Upload Videos

- Upload **up to 5 videos at a time**
- Supported formats:
  - MP4
  - AVI
  - MOV
  - MKV

You can upload:
- Your own custom videos
- Sample videos from this repo
- Videos from the **[FaceForensics++ 23 Dataset](https://www.kaggle.com/datasets/xdxd003/ff-c23)**

Each uploaded video will be displayed on the left side of the interface.

### 3️⃣ Configure Detection Settings

Before analysis, you can adjust the detection parameters:

- **Segment Duration (seconds)**  
  Controls how long each video segment is analyzed.

- **Frames Per Second (FPS)**  
  Controls how many frames are sampled per second.

- **Fake Confidence Threshold**  
  Determines the sensitivity of fake vs real classification.

These settings allow users to balance speed and accuracy.

### 4️⃣ Automatic Video Analysis

Once a video is uploaded, the system automatically:

1. Samples frames from the video
2. Detects faces using MTCNN
3. Runs EfficientNet-B0 inference on each face
4. Aggregates predictions across frames
5. Produces a video-level decision

No manual action is required after upload.


### 5️⃣ View Results

For each uploaded video, the results are shown on the **right side**:

- **Video Title** (e.g., *Video 1: example.mp4*)
- **Final Decision**
  - REAL ✅
  - FAKE 🚨
- **Fake Score**
- **Runtime**
- **Class-wise confidence visualization**

The Fake Score is calculated as:
> Fake Score = 1 − P(Original)

 A higher fake score indicates a higher likelihood of manipulation.



### 6️⃣ Interpret the Output

- **REAL**  
  The video is likely authentic.

- **FAKE**  
  The video shows signs of deepfake manipulation.

The per-class confidence bars provide insight into which manipulation type the model finds most likely.


## 🛡️ Use Case Perspective

Face Sure is designed for:

- Cyber-security awareness
- Deepfake threat analysis
- Educational and research demonstrations
- Practical deployment scenarios

It emphasizes **video-level detection**, which better reflects real-world cyber threats compared to frame-only approaches.


## ⚠️ Notes & Limitations

- Performance depends on video quality and face visibility
- Heavily occluded or low-resolution faces may reduce accuracy
- The current deployment uses **EfficientNet-B0 only**
- Explainability (Grad-CAM) is planned but not yet integrated

> 🚦 N.B: The trained model, notebooks, and supplementary documents are not included in this repository. If you want the files, [contact me](mailto:heyneeddev@gmail.com) anytime.

## ✅ Summary

Using Face Sure is simple:
1. Open the live website  
2. Upload videos  
3. Adjust settings (optional)  
4. View real-time deepfake detection results  

The system runs fully online and requires no local configuration.



