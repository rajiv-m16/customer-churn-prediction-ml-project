
# 📞 Telecom Customer Churn Prediction

## 1.0 Project Overview

This project is a Machine Learning web application designed to predict customer churn in the telecommunications sector. 
* It utilizes a Random Forest Classifier trained on historical customer data to identify users who are at a high risk of canceling their subscriptions. 
* By analyzing demographic information, account details, and service usage patterns, the application provides a predictive confidence score.
* This allows businesses to take proactive retention measures before the customer actually leaves.

## 2.0 Features

* **Real-Time Predictions:** Users can input customer data through a web interface and instantly receive a churn prediction.
* **Confidence Scoring:** The model doesn't just output "Yes" or "No"; it provides a probability percentage indicating how confident it is in the prediction.
* **Comprehensive Feature Analysis:** The model evaluates 19 distinct customer attributes, ranging from billing preferences to technical support usage.



![ML_LIFECYCLE](assets\ml_lifecycle.png)


## 3.0 Technology Stack

* **Machine Learning:** `scikit-learn` (Random Forest Classifier), `pandas` (Data Manipulation)
* **Backend:** Python, Flask
* **Frontend:** HTML5, Bootstrap 4, jQuery
* **Model Serialization:** `pickle`

## 4.0 Installation and Setup

To run this project locally, follow these steps:

1. **Clone the repository:**
   ```bash
   git clone <your-repository-url>
   cd TelecomChurnPredictionModel
   ```
2. **Install the required dependencies:**
   Ensure you have Python installed, then install the necessary packages.
   ```bash
   pip install pandas scikit-learn flask
   ```
3. **Run the Flask application:**
   ```bash
   python app.py
   ```
4. **Access the web interface:**
   Open your web browser and navigate to `http://127.0.0.1:5000/`.

## 5.0 Usage Example

To successfully predict a customer's churn probability, you must fill out the form fields with specific, formatted data that matches the training dataset.

**Example Input Scenario (High-Risk Customer):**
* **SeniorCitizen:** `0` (Meaning: No)
* **MonthlyCharges:** `85.50`
* **TotalCharges:** `120.00`
* **gender:** `Female`
* **Partner:** `No`
* **Dependents:** `No`
* **PhoneService:** `Yes`
* **MultipleLines:** `Yes`
* **InternetService:** `Fiber optic`
* **Contract:** `Month-to-month`
* **PaperlessBilling:** `Yes`
* **PaymentMethod:** `Electronic check`
* **tenure:** `2` (Meaning: 2 months)

Once submitted, the backend processes these inputs, encodes the categorical strings, and feeds them to the Random Forest model. The UI will return a statement such as: *"This customer is likely to be churned!! Confidence: 82.4%*".

## 6.0 Project Architecture & Structure

```text
└── 📁 TelecomChurnPredictionModel/
    ├── 📁 assets/
    │   └── WA_Fn-UseC_-Telco-Customer-Churn.csv  # Original dataset
    ├── 📁 templates/
    │   └── home.html                             # Frontend user interface
    ├── app.py                                    # Flask backend and prediction logic
    ├── Churn Analysis - EDA.ipynb                # Exploratory Data Analysis notebook
    ├── Churn Analysis - Model Building.ipynb     # Model training and export notebook
    ├── first_telc.csv                            # Base dataset used for dummy variable generation
    ├── model.sav                                 # Serialized Random Forest model
    └── tel_churn.csv                             # Cleaned dataset
```

## 7.0 Known Limitations & Future Improvements

To scale this application for a production environment, the following architectural refactoring is planned:

* **Optimize Data Encoding:** Currently, the application concatenates new user input with an entire historical dataset (`first_telc.csv`) to compute dummy variables via `pd.get_dummies()`. This will be replaced by saving a fitted `sklearn.preprocessing.OneHotEncoder` object during model training, allowing instant transformation of single-row inputs without memory overhead.
* **Global Model Loading:** The `model.sav` file is currently loaded inside the prediction route, meaning disk I/O occurs on every single form submission. This will be moved to the global scope to load into memory only once upon server startup.
* **Frontend Data Validation:** The HTML form currently relies on `<textarea>` elements for all inputs. These will be updated to `<select>` dropdowns for categorical variables and `<input type="number">` for continuous variables to prevent typos, data-type mismatches, and backend crashes.

***
