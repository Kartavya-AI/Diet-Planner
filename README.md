# 🍏 AI-Powered Diet Planner

(Rajani) An intelligent diet planning application that uses Google Cloud's Vertex AI (Gemini Pro) to generate personalized diet plans based on user's BMI and health profile.

## 🚀 Features

- **AI-Powered Recommendations**: Uses Google Gemini Pro for intelligent diet plan generation
- **BMI-Based Planning**: Calculates BMI and tailors diet plans accordingly
- **Personalized Profiles**: Considers age, gender, weight, and height for custom plans
- **BigQuery Integration**: Stores user data and diet plans in Google BigQuery
- **Real-time Analytics**: Provides health assessment and BMI visualization
- **Downloadable Plans**: Export diet plans as markdown files
- **Responsive UI**: Clean, modern interface built with Streamlit

## 🛠️ Technology Stack

- **Frontend**: Streamlit (Python)
- **AI Model**: Google Gemini Pro (Vertex AI)
- **Database**: Google BigQuery
- **Cloud Platform**: Google Cloud Platform (GCP)
- **Containerization**: Docker
- **CI/CD**: Google Cloud Build

## 📋 Prerequisites

- Google Cloud Platform account
- Google Cloud SDK installed
- Docker (for containerized deployment)
- Python 3.12+ (for local development)

## 🔧 Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/Kartavya-AI/Diet-Planner.git
cd agent_diet_planner
```

### 2. Local Development Setup

#### Option A: Direct Python Installation
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run locally
streamlit run app.py
```

#### Option B: Docker Setup
```bash
# Build Docker image
docker build -t diet-planner .

# Run container
docker run -p 8080:8080 diet-planner
```

### 3. Google Cloud Setup

#### Enable Required APIs
```bash
gcloud services enable \
  aiplatform.googleapis.com \
  bigquery.googleapis.com \
  cloudbuild.googleapis.com \
  cloudresourcemanager.googleapis.com \
  bigquery.googleapis.com
```

#### Set Up Authentication
1. Create a service account with these roles:
   - `BigQuery Admin`
   - `Cloud Run Admin`
   - `Cloud Run Invoker`
   - `Vertex AI Service Agent`
   - `Vertex AI User`

2. Download the service account key JSON

3. Set environment variable:
```bash
export GOOGLE_APPLICATION_CREDENTIALS="path/to/service-account.json"
```

### 4. BigQuery Setup
The application automatically creates the required BigQuery dataset and table on first run:
- **Dataset**: `diet_planner_data`
- **Table**: `user_plans`

## 🚀 Deployment Options

### 1. Google Cloud Run (Recommended)
```bash
# Deploy to Cloud Run
gcloud run deploy diet-planner \
  --source . \
  --region us-central1 \
  --allow-unauthenticated
```

### 2. Google Cloud Build (CI/CD)
The repository includes a `cloudbuild.yaml` for automated deployments:
```bash
# Trigger build
gcloud builds submit --config cloudbuild.yaml
```

## 📊 Data Structure

### User Profile Data
```json
{
  "user_id": "string",
  "timestamp": "timestamp",
  "weight": "float (kg)",
  "height": "integer (cm)",
  "age": "integer",
  "gender": "string",
  "diet_plan": "string (markdown)"
}
```

## 🎯 Usage Guide

1. **Access the Application**: Open the deployed URL or `localhost:8501` for local development
2. **Enter Profile**: Fill in your weight, height, age, and gender
3. **Generate Plan**: Click "Generate Diet Plan" to get AI-powered recommendations
4. **View Results**: See your BMI assessment and personalized diet plan
5. **Download**: Save your plan as a markdown file for offline use

## 🔍 BMI Categories

| BMI Range | Category | Health Status |
|-----------|----------|---------------|
| < 18.5 | Underweight | ⚠️ |
| 18.5-24.9 | Normal | ✅ |
| 25-29.9 | Overweight | ⚠️ |
| ≥ 30 | Obese | ❗ |

## 📈 Monitoring

- **Cloud Logging**: Application logs available in Google Cloud Console
- **BigQuery**: User analytics and plan generation metrics
- **Cloud Monitoring**: Performance and error tracking

## 🔄 Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `GCP_PROJECT_ID` | Google Cloud Project ID | `replace with you project id` |
| `GCP_LOCATION` | Google Cloud Region | `us-central1` |
| `PORT` | Application port | `8080` |
