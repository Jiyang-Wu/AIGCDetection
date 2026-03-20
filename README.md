# AIGCDetection
An AI generated video detection tool via a multimodal approach

## Overview

This project detects AI-generated videos by analyzing **structural inconsistencies** rather than visual artifacts.

Instead of looking for obvious mistakes, it focuses on deeper signals such as:
- motion dynamics that violate real-world physics
- temporal inconsistencies across frames
- synthetic audio characteristics
- mismatches between audio and visual signals

The system processes a video, extracts aligned video/audio segments, runs multiple independent detectors, and outputs a probability score with suspicious timestamps.

---

## Detection Methods

### 1. D3: Second-Order Temporal Volatility
Detects unrealistic motion dynamics using second-order differences of frame embeddings (acceleration-like behavior).

- Real videos → high volatility  
- AI videos → smoother patterns  

Paper: https://arxiv.org/abs/2508.00701  
*D3: Training-Free AI-Generated Video Detection Using Second-Order Features*

---

### 2. Optical Flow Residual Analysis
Detects motion inconsistencies by analyzing differences between consecutive optical flow fields.

- Captures unnatural motion acceleration patterns  

Paper: https://arxiv.org/abs/2508.00397  
*Video Forgery Detection with Optical Flow Residuals and Spatial-Temporal Consistency*

---

### 3. Audio Anti-Spoof Detection
Uses pretrained models to detect synthetic speech based on spectral and temporal anomalies.

- Identifies AI-generated voice characteristics  

---

### 4. Audio-Video Sync Consistency
Measures alignment between speech and mouth motion.

- Detects lip-sync mismatch and timing inconsistencies  


## Project Architecture
- Using ffmpeg to disassemble the video into properly segmented audio and video fragments
- Feeding the AV fragments accordingly into the detection models
- Calculating a weighted score indicating how likely is the content AI-generated
- (Maybe) generate a detailed report indicating the suspicious property or portion of the video that leads to "likely AI" conclusion
