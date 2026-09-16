# 📰 Fake News Detection Dashboard

An interactive **Data Analytics and Visualization** project that uses **Machine Learning and Streamlit** to classify news headlines as **REAL** or **FAKE**.

The project covers the complete machine-learning workflow: establishing a baseline, analyzing data quality, refining the training dataset, validating the model on independent datasets, and deploying the final application through Streamlit.

## 🚀 Live Demo

The application is designed for Streamlit deployment and can also be run locally. Add your deployed Streamlit URL here once available:

> **Live App:** _Add Streamlit deployment URL_

## 📌 Project Overview

The initial model was trained on a preliminary dataset, `merged_news.csv`, to establish a baseline and verify that the classification approach was feasible.

During analysis, the baseline predictions exposed inconsistencies in the original dataset labels. For example, headlines from trusted sources such as Reuters appeared with incorrect `FAKE` labels. This indicated that the issue was not simply model performance, but also **training-data quality and labeling consistency**.

To address this, the project was retrained using the **ISOT Fake News Dataset**, which provides separate `Fake.csv` and `True.csv` files and a more consistent labeling structure.

For deployment, the application uses a **10% representative sample of the ISOT dataset**. This keeps the repository and deployment footprint manageable while retaining the overall structure of the training data. The Logistic Regression model is trained when the Streamlit application starts, with `@st.cache_resource` used to avoid retraining on every interaction.

## 🧠 Machine Learning Pipeline

```text
Initial Dataset
      ↓
Baseline Model
      ↓
Data Quality Analysis
      ↓
Label / Dataset Refinement
      ↓
ISOT Dataset
      ↓
10% Representative Training Sample
      ↓
TF-IDF Feature Extraction
      ↓
Logistic Regression
      ↓
Cross-Validation & Independent Evaluation
      ↓
Streamlit Deployment
```

### Model

- **Algorithm:** Logistic Regression
- **Text Representation:** TF-IDF
- **Task:** Binary text classification
- **Classes:** `REAL` / `FAKE`
- **Deployment:** Streamlit

## ✨ Features

The dashboard is divided into five tabs, each corresponding to a stage of the analysis workflow.

### 1. 📰 News Analyzer

Enter a news headline and receive:

- Predicted class: **REAL** or **FAKE**
- Model confidence score
- Immediate classification through the deployed ML pipeline

### 2. 📊 Visual Insights

Explore the characteristics of the ISOT training sample, including:

- REAL vs. FAKE class distribution
- Article subject distribution, such as `politicsNews` and `worldnews`
- Article-length distribution

These visualizations help demonstrate the patterns present in the training data.

### 3. 🔍 Cross-Validation — WELFake

The trained ISOT model is evaluated against `welfake_sample_final.csv`.

The evaluation workflow:

- Detects the label convention used by the validation dataset
- Corrects the label mapping when the WELFake labels are inverted
- Calculates validation accuracy
- Generates a confusion matrix

This provides an external check of model performance on data that was not used for training.

### 4. 🧪 Final Evaluation

A second independent evaluation is performed using `evaluation_final.csv`.

The application:

- Checks whether the evaluation labels use the expected mapping
- Adjusts the mapping when necessary
- Calculates validation accuracy
- Displays a confusion matrix

### 5. ℹ️ About This Model

Provides information about:

- The datasets used in the project
- Why the original dataset was replaced
- The 10% deployment sample
- The Logistic Regression + TF-IDF architecture
- The overall project workflow

## 📂 Project Structure

```text
fake-news-app/
├── app1.py
├── requirements.txt
├── README.md
├── welfake_sample_final.csv
├── evaluation_final.csv
└── ...
```

> Dataset filenames may vary depending on the version of the repository. The application expects the required CSV files to be available at runtime.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Pandas | Data loading and preprocessing |
| NumPy | Numerical operations |
| Scikit-learn | TF-IDF, Logistic Regression, metrics and evaluation |
| Matplotlib / Seaborn | Data visualization |
| Streamlit | Interactive web application |
| Git & GitHub | Version control and deployment workflow |

## 📊 Datasets

### ISOT Fake News Dataset

Used as the primary training dataset after analysis of the original baseline data revealed labeling inconsistencies.

The deployment version uses a **10% representative sample** of the available ISOT data to reduce repository and deployment size.

### WELFake

Used as an independent validation dataset to evaluate how the ISOT-trained classifier performs on another source of labeled news data.

### Evaluation Dataset

`evaluation_final.csv` is used for a separate final evaluation step and confusion-matrix analysis.

## 🔬 Why the Dataset Was Changed

The project initially focused on model development using `merged_news.csv`. However, exploratory analysis of the resulting predictions revealed examples where headlines from known trusted sources were associated with incorrect labels.

Rather than attempting to compensate for potentially inconsistent labels through model tuning alone, the project changed the primary training source to the ISOT dataset.

This highlights an important machine-learning lesson:

> **Model quality depends heavily on data quality.**

Better algorithms cannot reliably compensate for systematically incorrect training labels.

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/david7635/fake-news-app.git
cd fake-news-app
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the Streamlit application

```bash
streamlit run app1.py
```

The application will start locally and Streamlit will provide a browser URL, usually:

```text
http://localhost:8501
```

## ☁️ Deployment

The application can be deployed using **Streamlit Community Cloud** or another environment capable of running Streamlit applications.

For deployment, make sure the repository contains:

- `app1.py`
- `requirements.txt`
- Required CSV datasets
- Any additional project files imported by the application

Because the model is trained at application startup, the deployment environment needs enough memory and CPU resources to load the data and fit the classifier.

## ⚠️ Limitations

This project is intended as an academic **data analytics and machine-learning demonstration**, not as a definitive fact-checking system.

A text classifier can identify patterns associated with the training data, but it does not independently verify whether a real-world claim is factually true.

Performance may also vary across:

- Different news sources
- Topics not well represented in the training data
- Writing styles outside the training distribution
- Datasets with different labeling conventions

The reported validation results should therefore be interpreted in the context of the datasets used for evaluation.

## 🔮 Possible Improvements

Future versions could explore:

- Larger training samples or the complete ISOT dataset
- Hyperparameter tuning for Logistic Regression
- Additional models such as Linear SVM or Naive Bayes
- More robust preprocessing and text normalization
- Precision, recall, F1-score and ROC-AUC reporting
- Model explainability using influential TF-IDF features
- Real-time news-source verification APIs
- Persistent model artifacts to avoid training during application startup

## 👨‍💻 Author

**David Dasari**

GitHub: [@david7635](https://github.com/david7635)

## 📄 License

Add the project's license here if one is included in the repository.
