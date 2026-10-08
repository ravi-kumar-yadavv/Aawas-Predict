# Aawas Predict 🏠

### Machine Learning Based House Price Prediction

Aawas Predict is a small end-to-end machine learning project that estimates the price of a residential property in Mumbai from a few basic details entered by the user.

The project covers the complete journey from **data preparation and model training to a working prediction application**. A Random Forest regression model is trained on the Mumbai house-price dataset and then used through a Flask backend and Streamlit interface.

## What Aawas Predict does

The application takes these property details as input:

- BHK
- Property type
- Area in square feet
- Mumbai region
- Construction status
- Age/category of the property

It then sends the details to the backend, prepares the input in the same format used during model training, and returns an estimated price.

## Project workflow

```text
Mumbai House Price Dataset
          ↓
Data Cleaning & Preparation
          ↓
Feature Engineering
          ↓
Categorical Encoding
          ↓
Train / Test Split
          ↓
Regression Model Comparison
          ↓
Random Forest Model
          ↓
Saved Model + Feature Columns
          ↓
Flask API
          ↓
Streamlit Interface
          ↓
Estimated Property Price
```

## Machine Learning work

The model-development notebook is `model/MLmodel.ipynb`.

The notebook includes:

1. Loading and exploring the dataset with Pandas.
2. Converting prices from Lakh/Crore units into INR.
3. Creating a price-per-square-foot feature for analysis.
4. Grouping less frequent regions into `other`.
5. Removing price-per-square-foot outliers by region.
6. Converting categorical values into numerical features.
7. Splitting the data into training and testing sets.
8. Comparing regression approaches using cross-validation.
9. Training a Random Forest Regressor on the prepared dataset.
10. Saving the trained model with Pickle and saving the model columns in JSON format.

### Models explored

- Linear Regression
- Decision Tree Regression
- Random Forest Regression

The saved model used by the application is a **Random Forest Regressor**.

## Application structure

```text
Aawas-Predict/
│
├── client/
│   ├── app.py
│   └── Mumbai.jpg
│
├── model/
│   ├── MLmodel.ipynb
│   ├── Mumbai House Prices.csv
│   ├── Mumbai_Price_predictor.pickle
│   └── columns.json
│
├── server/
│   ├── server.py
│   ├── util.py
│   └── artifacts/
│       ├── Mumbai_Price_predictor.pickle
│       └── columns.json
│
├── .gitignore
├── requirements.txt
└── README.md
```

## How the application works

### 1. Streamlit frontend

The user enters the property details in `client/app.py`.

### 2. Flask backend

The Streamlit app sends those values to the Flask API in `server/server.py`.

### 3. Input preparation

`server/util.py` converts values such as status and age into the numerical representation expected by the trained model. It also creates the feature vector using the saved column information.

### 4. Prediction

The saved Random Forest model receives the prepared feature vector and returns the estimated property price.

### 5. Result

The estimated price is returned by Flask and displayed in the Streamlit interface.

## Run the project locally

### Step 1: Clone the repository

```bash
git clone <your-repository-url>
cd Aawas-Predict
```

### Step 2: Install dependencies

It is recommended to use a virtual environment.

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Then install the required packages:

```bash
pip install -r requirements.txt
```

### Step 3: Start the Flask backend

Open a terminal in the `server` folder:

```bash
cd server
python server.py
```

The Flask server will run locally on port `5000`.

### Step 4: Start the Streamlit frontend

Open a **second terminal** and go to the `client` folder:

```bash
cd client
streamlit run app.py
```

The Streamlit application will open in your browser.

### Step 5: Make a prediction

Enter the property details, click **Predict Price**, and the application will display the estimated price.

## Tech stack

- **Python** — main programming language
- **Pandas** — data loading and manipulation
- **NumPy** — numerical operations
- **Matplotlib** — exploratory data visualisation
- **Scikit-learn** — machine learning and model evaluation
- **Pickle** — saving the trained model
- **Flask** — backend prediction API
- **Streamlit** — user interface
- **Requests** — communication between the Streamlit app and Flask API
- **Jupyter Notebook** — model development and experimentation

## Key learning points

This project helped me understand how an ML model moves beyond a notebook and becomes part of a simple application:

**Dataset → Preprocessing → Model Training → Evaluation → Saved Model → API → User Interface → Prediction**

It also provides practical experience with categorical encoding, feature preparation, regression models, cross-validation, model serialization, REST-style API endpoints, and connecting a frontend to a backend.
