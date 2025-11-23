# Heart Disease Risk Prediction - ML Hackathon

A machine learning project developed during a Kaggle-style hackathon for the Machine Learning course at ISAE-SUPAERO. The goal is to predict heart disease risk using a large dataset.

**My Contribution**: Primary focus on data engineering, feature extraction from HTML codebook, and feature selection strategies. Collaborative work on model development.

## Project Overview

This project tackles a **binary classification problem** to predict cardiovascular disease risk based on health survey data. The dataset contains responses from 225000 participants across 325 features including demographics, health status, lifestyle factors, and chronic conditions.

### Key Challenges
- **Highly imbalanced dataset**: Only ~10% positive cases
- **High dimensionality**: 325 features with varying levels of missing data
- **Complex survey data**: Optional questions leading to >90% missing values in some features

## Results

| Model | Approach | Validation F1-Score | Features |
|-------|----------|---------------------|----------|
| Random Forest | Class balancing + correlation filtering | **0.151** | 23 features (|corr| > 0.1) |

**Model Configuration:**
- Algorithm: Random Forest (1,000 trees)
- Feature selection: Correlation-based (|correlation| > 0.1 with target)
- Class balancing: Enabled to handle imbalanced dataset (~9% positive class)
- Selected 23 most relevant features from 322 total features

## 🔍 Methodology

### 1. Data Engineering (Author's Main Focus)
- **Feature categorization**: Organized 325 features into thematic sections
- **Data quality assessment**: Identified and removed features with 100% missing values
- **Correlation analysis**: Analyzed feature correlations within each section to identify redundancies

### 2. Key Features Selected
The final model uses 23 features with strongest correlation to target:
- **Age-related**: `_AGE80`, `_AGEG5YR`, `_AGE_G`, `_AGE65YR`
- **Health status**: `GENHLTH`, `_RFHLTH`
- **Chronic conditions**: `DIABETE4`, `HAVARTH4`
- **Lifestyle**: Smoking variables (`_PACKYRS`, `_YRSSMOK`, `_PACKDAY`)
- **Healthcare access**: `_HCVU652`, `EMPLOY1`

### 3. Model Development (Collaborative)
- **Feature selection**: Selected 23 features with |correlation| > 0.1 with target
- **Preprocessing**: Handled missing values and encoded categorical variables
- **Model**: Random Forest Classifier with 1,000 trees

## 💡 Key Learnings

### Data Engineering Insights
1. **Feature categorization matters**: Organizing features by sections (Health Status, Demographics, etc.) helped understand the data structure
2. **Missing data patterns**: Many features had >90% missing values (optional survey questions)
3. **Intra-section correlations**: Many sections contain redundant features (e.g., multiple age representations)

### Modeling Insights
1. **Feature selection is crucial**: Reducing from 322 to 23 features improved model performance and training speed
2. **Class imbalance is challenging**: 91%/9% split requires special handling (class weighting)
3. **Correlation-based selection works**: Simple correlation filtering (|corr| > 0.1) was effective
4. **Domain knowledge helps**: Understanding feature meanings guided better preprocessing decisions
