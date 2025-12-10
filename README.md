# Academic-Abstract-Classifier
🧠 Project Overview

The Abstract Classification Service is a lightweight, high-performance system designed to classify research paper abstracts using a fine-tuned Transformer model.
The project includes:

A training pipeline for building a DistilBERT-based classifier

A fully functional REST API using FastAPI

Easy deployment using Docker

Clean dataset management and evaluation tools

This repository is ideal for researchers, developers, and students who want to build or integrate fast, efficient NLP classification models.

🚀 Key Features

🔥 Fast Transformer-based Classification using DistilBERT

🧹 Automated Data Cleaning & Column Detection

⚖️ Balanced Training Subset for better generalization

📊 Detailed Evaluation Metrics (precision, recall, F1, per-class metrics)

🧪 Confusion Matrix & Misclassification Logs

🌐 FastAPI-based REST API for real-time inference

🐳 Docker Support for easy deployment

🛠️ Environment Setup
1. Requirements

Python: 3.9 or 3.10 recommended

Pip & virtual environment suggested

GPU optional (automatically utilized if available)

2. Install Dependencies
pip install -r requirements.txt

📚 Training the Model
Steps:

Ensure your dataset (CSV/TSV) exists in the project root.
Default provided: arxiv_data.csv.

Train the model:

python train_model.py

Training Workflow:

Auto-detects abstract & label columns

Cleans missing or very short abstracts

Builds a balanced subset (≈1200 samples; 800 on CPU-only)

Splits data into train/val/test (80/10/10, stratified)

Fine-tunes a DistilBERT classifier for 1 epoch

Saves the following artifacts:

Artifact	Description
final_model/	Model, tokenizer, labels
train.csv	Training split
val.csv	Validation split
test.csv	Testing split
metrics.json	Accuracy + macro precision/recall/F1
confusion_matrix.csv	Confusion matrix data
misclassified_samples.csv	Records incorrect predictions
🌐 Running the API Locally

After training and ensuring final_model/ is present:

Start the FastAPI server
uvicorn app:app --host 0.0.0.0 --port 8000

API Endpoints
✔ Health Check
GET /health


Response:

{"status": "ok"}

✔ Fetch Labels
GET /labels

✔ Predict Label
POST /predict


Example:

curl -X POST "http://localhost:8000/predict" \
  -H "Content-Type: application/json" \
  -d '{"abstract":"This paper proposes a transformer-based classification approach..."}'


Example Output:

{
  "label": "cs.LG",
  "score": 0.9234,
  "all_scores": [
    {"label": "cs.LG", "score": 0.9234},
    {"label": "cs.AI", "score": 0.0345}
  ]
}

🐳 Docker Usage
Build Image
docker build -t abstract-classifier .

Train Model in Docker
docker run --rm -v ${PWD}:/app abstract-classifier python train_model.py

Run API in Docker
docker run --rm -p 8000:8000 -v ${PWD}:/app abstract-classifier \
  uvicorn app:app --host 0.0.0.0 --port 8000

☁️ Deployment Options
Render / Railway

Use this repo and set the Start Command:

uvicorn app:app --host 0.0.0.0 --port 8000

Hugging Face Spaces

Use Docker-based deployment
OR

Use app.py + requirements.txt directly

📂 Repository Structure
project-root/
│── app.py
│── train_model.py
│── arxiv_data.csv
│── requirements.txt
│── Dockerfile
│── final_model/
│── metrics.json
│── confusion_matrix.csv
│── misclassified_samples.csv
│── README.md

🤝 Contributing

Contributions are welcome!

Fork the repository

Create a new feature branch

Commit your changes

Submit a pull request
