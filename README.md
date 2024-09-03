---

# Potato Disease Classification

## Problem Statement

Potato crops are vulnerable to various diseases, among which Early Blight and Late Blight are particularly damaging. Identifying these diseases early is crucial for preventing crop loss. This project aims to build a machine learning model that classifies potato leaf images into three categories: **Early Blight**, **Late Blight**, and **Healthy**.

## Solution Architecture

1. **Model Training**: A Convolutional Neural Network (CNN) is trained using images of potato leaves categorized as Early Blight, Healthy, and Late Blight.
2. **Model Serving**: The trained model is served using TensorFlow Serving for efficient inference.
3. **Backend**: A FastAPI-based backend handles API requests for classification, interacting with the TensorFlow Serving API.
4. **Frontend**: A React-based frontend allows users to upload or drag and drop images of potato leaves for classification.
5. **Deployment**: The system can be containerized using Docker for easy deployment, and the backend and model can be deployed on platforms like Google Cloud.

## Setup for Python:

1. Install Python ([Setup instructions](https://wiki.python.org/moin/BeginnersGuide))

2. Install Python packages

```bash
pip3 install -r training/requirements.txt
pip3 install -r api/requirements.txt
```

3. Install TensorFlow Serving ([Setup instructions](https://www.tensorflow.org/tfx/serving/setup))

## Setup for Frontend

1. Install Node.js ([Setup instructions](https://nodejs.org/en/download/package-manager/))
2. Install NPM ([Setup instructions](https://www.npmjs.com/get-npm))
3. Install dependencies

```bash
cd frontend
npm install --from-lock-json
npm audit fix
```

4. Copy `.env.example` as `.env`.

5. Change the API URL in `.env`.

## Training the Model

1. Download the data from [Kaggle](https://www.kaggle.com/arjuntejaswi/plant-village).
2. Keep only folders related to Potatoes.
3. Run Jupyter Notebook in Browser.

```bash
jupyter notebook
```

4. Open `training/potato-disease-training.ipynb` in Jupyter Notebook.
5. Update the path to the dataset in cell #2.
6. Run all the cells one by one.
7. Copy the generated model and save it with a version number in the `saved_models` folder.

## Running the API

### Using FastAPI

1. Navigate to the `api` folder

```bash
cd api
```

2. Run the FastAPI server using Uvicorn

```bash
uvicorn main:app --reload --host 0.0.0.0
```

3. Your API is now running at `0.0.0.0:8000`

### Using FastAPI & TensorFlow Serving

1. Navigate to the `api` folder

```bash
cd api
```

2. Copy `models.config.example` as `models.config` and update the paths in the file.
3. Run TensorFlow Serving (update the config file path below)

```bash
docker run -t --rm -p 8501:8501 -v C:/Code/potato-disease-classification:/potato-disease-classification tensorflow/serving --rest_api_port=8501 --model_config_file=/potato-disease-classification/models.config
```

4. Run the FastAPI server using Uvicorn

```bash
uvicorn main-tf-serving:app --reload --host 0.0.0.0
```

5. Your API is now running at `0.0.0.0:8000`

## Running the Frontend

1. Navigate to the `frontend` folder

```bash
cd frontend
```

2. Copy `.env.example` as `.env` and update `REACT_APP_API_URL` to your API URL if needed.
3. Run the frontend

```bash
npm run start
```

---

