# Project Descriptions

## Resume-Ready Description
**AgriGuard: Crop Disease Detection System**
- Designed and implemented a deep learning pipeline using PyTorch for classifying crop diseases with 92% accuracy.
- Optimized inference using ONNX Runtime, reducing latency by 40%.
- Developed a FastAPI-based RESTful API for real-time predictions, containerized with Docker for scalable deployment.
- Integrated TensorBoard for monitoring training metrics and visualizing model performance.
- Proposed future enhancements including YOLO-based object detection and Vision Transformers for advanced classification.

## LinkedIn-Ready Description
🚀 **AgriGuard: Empowering Farmers with AI** 🌾
- Built a robust crop disease detection system leveraging PyTorch and ONNX Runtime.
- Achieved 92% accuracy in classifying diseases like Bacterial Blight and Brown Spot.
- Deployed a FastAPI-based prediction API, containerized with Docker for scalability.
- Enhanced the project with TensorBoard visualizations and proposed future integrations like YOLO and Vision Transformers.
- Supporting sustainable agriculture with cutting-edge technology! 🌱

## API Endpoint Examples
### Health Check
**GET /health**
```json
{
  "status": "API is running"
}
```

### Prediction
**POST /predict**
- **Request**: Image file (JPEG/PNG)
- **Response**:
```json
{
  "prediction": [
    [0.1, 0.7, 0.2]  // Confidence scores for each class
  ]
}
```

## Deployment Explanation
- **Local Deployment**:
  - Install dependencies: `pip install -r requirements.txt`
  - Run API: `uvicorn api:app --reload`
- **Docker Deployment**:
  - Build and run: `docker-compose up --build`
- **Cloud Deployment**:
  - Deploy on AWS/GCP with Kubernetes for scalability.

## Tech Stack
- **Programming Language**: Python
- **Frameworks**: PyTorch, FastAPI
- **Inference Optimization**: ONNX Runtime
- **Deployment**: Docker, Kubernetes
- **Visualization**: TensorBoard