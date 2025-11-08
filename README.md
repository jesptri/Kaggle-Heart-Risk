# Heart Disease Risk Prediction - ML Hackathon

![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.4.0-orange.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

A machine learning project developed during a Kaggle-style hackathon for the Machine Learning course at ISAE-SUPAERO. The goal is to predict heart disease risk using the BRFSS (Behavioral Risk Factor Surveillance System) dataset.

**Author's Contribution**: Primary focus on data engineering, feature extraction from HTML codebook, and feature selection strategies. Collaborative work on model development.

## 📊 Project Overview

This project tackles a **binary classification problem** to predict cardiovascular disease risk based on health survey data. The dataset contains responses from 225,000 participants across 325 features including demographics, health status, lifestyle factors, and chronic conditions.

### Key Challenges
- **Highly imbalanced dataset**: Only ~9% positive cases
- **High dimensionality**: 325 features with varying levels of missing data
- **Complex survey data**: Optional questions leading to >90% missing values in some features

## 🎯 Results

| Model | Approach | Validation F1-Score | Features |
|-------|----------|---------------------|----------|
| Random Forest | Class balancing + correlation filtering | **0.151** | 23 features (|corr| > 0.1) |

**Model Configuration:**
- Algorithm: Random Forest (1,000 trees)
- Feature selection: Correlation-based (|correlation| > 0.1 with target)
- Class balancing: Enabled to handle imbalanced dataset (~9% positive class)
- Selected 23 most relevant features from 322 total features

## 📂 Project Structure

```
Mini_Hackathon_Novembre/
│
├── data/                           # Data directory (not included in repo)
│   ├── train.csv                  # Training dataset
│   ├── test.csv                   # Test dataset
│   ├── USCODE22_LLCP_102523.HTML  # Feature codebook
│   └── labels_questions.csv       # Extracted feature labels
│
├── data_engineering.ipynb         # Data preprocessing & feature extraction (main work)
├── models.ipynb                   # Model training & evaluation (collaborative)
│
├── main_ag.ipynb                  # Original data engineering experiments
├── main_je.ipynb                  # Original SVM experiments
├── main_ag_le_mien.ipynb          # Original extensive analysis
├── main_nf.ipynb                  # Original Random Forest experiments
│
├── predictions_random_forest.csv  # Final model predictions
├── predictions_svm.csv            # Alternative SVM predictions
│
├── requirements.txt               # Python dependencies
├── .gitignore                     # Git ignore file
└── README.md                      # This file
```

## 🚀 Getting Started

### Prerequisites

- Python 3.11 or higher
- pip package manager

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/heart-disease-prediction.git
cd heart-disease-prediction
```

2. **Install dependencies**
```bash
pip install -r requirements.txt
```

3. **Download the data**
   - Place `train.csv`, `test.csv`, and `USCODE22_LLCP_102523.HTML` in the `data/` directory
   - Note: Data files are not included in the repository due to size constraints

### Usage

#### 1. Data Engineering (Main Work)
Run the data engineering notebook to see feature extraction and preprocessing:
```bash
jupyter notebook data_engineering.ipynb
```

This notebook includes:
- HTML codebook parsing to extract feature labels
- Feature categorization by sections
- Removal of empty features (100% NaN)
- Intra-section correlation analysis
- Feature metadata extraction

#### 2. Model Training (Collaborative Work)
Run the models notebook to see the machine learning pipeline:
```bash
jupyter notebook models.ipynb
```

This notebook covers:
- Feature selection based on correlation with target
- Data preprocessing and encoding
- Random Forest model training with class balancing
- Model evaluation and performance metrics
- Prediction generation on test set

## 🔍 Methodology

### 1. Data Engineering (Author's Main Focus)
- **HTML codebook parsing**: Extracted feature labels and sections from HTML documentation
- **Feature categorization**: Organized 325 features into thematic sections
- **Data quality assessment**: Identified and removed 3 features with 100% missing values
- **Correlation analysis**: Analyzed feature correlations within each section to identify redundancies

### 2. Model Development (Collaborative)
- **Feature selection**: Selected 23 features with |correlation| > 0.1 with target
- **Preprocessing**: Handled missing values and encoded categorical variables
- **Class balancing**: Used `class_weight='balanced'` to handle 91%/9% class imbalance
- **Model**: Random Forest Classifier with 1,000 trees

### 3. Key Features Selected
The final model uses 23 features with strongest correlation to target:
- **Age-related**: `_AGE80`, `_AGEG5YR`, `_AGE_G`, `_AGE65YR`
- **Health status**: `GENHLTH`, `_RFHLTH`
- **Chronic conditions**: `DIABETE4`, `HAVARTH4`
- **Lifestyle**: Smoking variables (`_PACKYRS`, `_YRSSMOK`, `_PACKDAY`)
- **Healthcare access**: `_HCVU652`, `EMPLOY1`

## 💡 Key Learnings

### Data Engineering Insights
1. **HTML parsing is valuable**: Extracting feature metadata from documentation provided crucial context
2. **Feature categorization matters**: Organizing features by sections (Health Status, Demographics, etc.) helped understand the data structure
3. **Missing data patterns**: Many features had >90% missing values (optional survey questions)
4. **Intra-section correlations**: Many sections contain redundant features (e.g., multiple age representations)

### Modeling Insights
1. **Feature selection is crucial**: Reducing from 322 to 23 features improved model performance and training speed
2. **Class imbalance is challenging**: 91%/9% split requires special handling (class weighting)
3. **Correlation-based selection works**: Simple correlation filtering (|corr| > 0.1) was effective
4. **Domain knowledge helps**: Understanding feature meanings guided better preprocessing decisions

## 📝 Future Improvements

### Data Engineering
- [ ] Merge redundant features within sections (e.g., combine age variables)
- [ ] Feature engineering from correlated groups
- [ ] Handle missing data with domain-specific imputation strategies
- [ ] Create interaction features between high-correlation variables

### Modeling
- [ ] Try SVM or other algorithms with threshold optimization
- [ ] Implement SMOTE or other resampling techniques
- [ ] Hyperparameter tuning with GridSearchCV/RandomizedSearchCV
- [ ] Ensemble methods (stacking, voting classifier)
- [ ] Feature importance analysis and interpretation
