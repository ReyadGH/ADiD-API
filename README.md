# Arabic Dialect Identification (ADiD)

An intelligent API system that identifies Arabic dialects from text and Twitter content.

## Description

ADiD is a machine learning-based system that classifies Arabic text into different dialectal varieties:
- Solves the challenge of identifying different Arabic dialects in text
- Serves users wanting to search for dialect-specific content and businesses seeking valuable audience insights
- Uses NLP techniques and ML algorithms (Naive Bayes, SVM, XgBoost)
- Provides both general text classification and Twitter-specific features

## Demo

The API is accessible at: https://adid-app.herokuapp.com/

## Getting Started

### Prerequisites

* Python 3.8+
* Required libraries (listed in requirements.txt)
* Twitter API access (Not Working)

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/adid-api.git

# Navigate to project directory
cd adid-api

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Running the Application

```bash
# Run the application
python app.py
```

## Usage Examples

### Using the API

```python
import requests
import json

# Predict dialect of text
url = "https://adid-app.herokuapp.com/api/general"
payload = {
    "request": [
        {
            "id": "1",
            "text": "قمة جبل فوجي هي اعلي قمة جبلية في اليابان حيث يبلغ ارتفاعها ثلاثة آلاف وسبعمائة وستون مترا"
        }
    ]
}
headers = {
    "Content-Type": "application/json",
    "accept": "application/json"
}
response = requests.post(url, json=payload, headers=headers)
print(json.dumps(response.json(), ensure_ascii=False, indent=2))

# Get Twitter user dialect
twitter_user = "username"
url = f"https://adid-app.herokuapp.com/api/twitter/by_user/{twitter_user}"
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), ensure_ascii=False, indent=2))
```

## Project Structure

```
adid-api/
├── app.py                  # Main application entry point
├── endpoints.py            # API endpoints
├── general_methods.py      # General utility methods
├── twitter_methods.py      # Twitter-specific methods
├── models/                 # Trained ML models
│   ├── MultinomialNB(CountVectorizer).joblib
│   └── transformerMultinomialNB(CountVectorizer).joblib
├── static/                 # Static files for web UI
│   ├── img/
│   └── swagger.yml         # API documentation
├── templates/              # HTML templates
│   └── home.html
├── requirements.txt        # Required dependencies
└── Procfile                # Heroku deployment config
```

## API Reference

| Endpoint | Method | Description | Parameters |
|----------|--------|-------------|------------|
| `/api/general` | POST | Predict dialect of text | JSON body with text |
| `/api/twitter/by_user/{username}` | GET | Predict Twitter user dialect | `username` (required) |
| `/api/twitter/by_hashtag/{hashtag}` | GET | Predict hashtag dialects | `hashtag` (required) |
| `/api/twitter/by_user/{username}/{dialect}` | GET | Get user's tweets in specific dialect | `username`, `dialect` (required) |
| `/api/twitter/by_hashtag/{hashtag}/{dialect}` | GET | Get hashtag tweets in specific dialect | `hashtag`, `dialect` (required) |

## Authors

- Reyad Abdullah Al-Ghamdi
- Abdullah Ahmad Babrouk

## License

This project was completed under the supervision of Dr. Ali Alkhathlan at King Abdulaziz University.
