# AgriGuard: Crop Disease Detection System

> **Empowering Farmers with AI-Driven Crop Health Insights**

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-ML_Framework-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![ONNX Runtime](https://img.shields.io/badge/ONNX_Runtime-Optimized_Inference-005CED?style=for-the-badge&logo=onnx&logoColor=white)](https://onnxruntime.ai/)
[![FastAPI](https://img.shields.io/badge/FastAPI-API_Serving-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)

AgriGuard is a cutting-edge system designed to detect crop diseases using AI and Computer Vision. This project leverages deep learning models, optimized inference, and scalable APIs to provide actionable insights for farmers.

---

## Detailed Sections

### Problem Statement
Crop diseases significantly impact agricultural productivity, leading to economic losses and food insecurity. Early and accurate detection of diseases can help mitigate these effects. AgriGuard aims to provide a reliable and accessible solution for identifying crop diseases from leaf images.

### Dataset Information
- **Source**: Publicly available datasets of diseased and healthy crop leaf images.
- **Classes**: Bacterial Blight, Brown Spot, Blast Disease, and Healthy.
- **Preprocessing**: Images resized to 224x224, normalized, and augmented for training.

### Model Architecture
- **Base Model**: ResNet-50 pre-trained on ImageNet.
- **Custom Layers**: Fully connected layers for classification.
- **Framework**: PyTorch.
- **Optimization**: ONNX Runtime for inference.

### Training Pipeline
1. **Data Loading**: PyTorch DataLoader with augmentations.
2. **Training**: Cross-entropy loss, Adam optimizer.
3. **Validation**: Accuracy and loss metrics.
4. **Logging**: TensorBoard for visualization.

### Evaluation Metrics
- **Accuracy**: Overall correctness of predictions.
- **Precision**: Correct positive predictions.
- **Recall**: Sensitivity to true positives.
- **F1-Score**: Balance between precision and recall.
- **Confusion Matrix**: Visual representation of predictions.

### Inference Pipeline
1. **Input**: Leaf image (JPEG/PNG).
2. **Preprocessing**: Resize, normalize.
3. **Model**: ONNX Runtime for optimized inference.
4. **Output**: Predicted class and confidence score.

### Deployment/API Serving
- **Framework**: FastAPI.
- **Endpoints**:
  - `/predict`: Accepts an image and returns the disease class.
  - `/health`: Health check for the API.
- **Dockerized**: Containerized for scalable deployment.

### Results
- **Accuracy**: 92%
- **Precision**: 90%
- **Recall**: 91%
- **F1-Score**: 90.5%

### Future Improvements
- **Object Detection**: Integrate YOLO for detecting multiple diseased areas.
- **OCR**: Extract text from leaf tags for additional context.
- **Transformers**: Explore ViT for improved classification.

---

## Tech Stack

- **Python**: Core programming language.
- **PyTorch**: Deep learning framework.
- **ONNX Runtime**: Optimized inference.
- **FastAPI**: API serving.
- **Docker**: Deployment.

---

## Getting Started

### Prerequisites
- Python 3.8+
- PyTorch
- ONNX Runtime
- FastAPI
- Docker

### Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/vedikalohiya/AgriGuard.git
   cd AgriGuard
   ```

2. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the API**
   ```bash
   uvicorn api:app --reload
   ```

4. **Docker Deployment**
   ```bash
   docker-compose up --build
   ```

---

## ONNX Runtime Optimization Workflow

1. **Convert PyTorch Model to ONNX**:
   ```python
   import torch
   import onnx

   # Load PyTorch model
   model = torch.load('models/resnet50.pth')
   model.eval()

   # Dummy input for tracing
   dummy_input = torch.randn(1, 3, 224, 224)

   # Export to ONNX
   torch.onnx.export(
       model,
       dummy_input,
       "models/resnet50.onnx",
       input_names=['input'],
       output_names=['output'],
       dynamic_axes={'input': {0: 'batch_size'}, 'output': {0: 'batch_size'}}
   )
   ```

2. **Optimize with ONNX Runtime**:
   ```python
   from onnxruntime import InferenceSession, SessionOptions

   # Load ONNX model
   session_options = SessionOptions()
   session = InferenceSession("models/resnet50.onnx", sess_options=session_options)

   # Run inference
   def predict(image):
       inputs = {session.get_inputs()[0].name: image}
       outputs = session.run(None, inputs)
       return outputs
   ```

3. **Benchmark Performance**:
   ```python
   import time

   start_time = time.time()
   for _ in range(100):
       predict(dummy_input.numpy())
   print(f"Average Inference Time: {(time.time() - start_time) / 100:.4f} seconds")
   ```

---

## Evaluation Metrics

### Accuracy
- Measures the overall correctness of predictions.
- Formula: $\text{Accuracy} = \frac{\text{True Positives} + \text{True Negatives}}{\text{Total Samples}}$

### Precision
- Indicates the proportion of true positive predictions among all positive predictions.
- Formula: $\text{Precision} = \frac{\text{True Positives}}{\text{True Positives} + \text{False Positives}}$

### Recall
- Measures the model's ability to identify all relevant instances.
- Formula: $\text{Recall} = \frac{\text{True Positives}}{\text{True Positives} + \text{False Negatives}}$

### F1-Score
- Harmonic mean of precision and recall, balancing both metrics.
- Formula: $\text{F1-Score} = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}$

### Confusion Matrix
- A table summarizing the performance of a classification model.
- Example:
  ```
  | Actual \ Predicted | Positive | Negative |
  |--------------------|----------|----------|
  | Positive           | TP       | FN       |
  | Negative           | FP       | TN       |
  ```
- **TP**: True Positives, **FP**: False Positives, **FN**: False Negatives, **TN**: True Negatives.

---

## Contributors

| **Vedika Lohiya** |
| :---: |
| [![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/vedikalohiya) |

---

## Suggested Folder Structure

```
AgriGuard/
├── data/                # Datasets and preprocessing scripts
├── models/              # Trained models and checkpoints
├── training/            # Training scripts and configurations
├── evaluation/          # Evaluation scripts and metrics
├── deployment/          # Dockerfiles and deployment configurations
├── api/                 # FastAPI application
├── notebooks/           # Jupyter notebooks for experiments
├── scripts/             # Utility scripts
├── requirements.txt     # Python dependencies
├── README.md            # Project documentation
└── .env                 # Environment variables
```

---

<div align="center">
  <p>Made with ❤️ to support Sustainable Agriculture</p>
</div>
