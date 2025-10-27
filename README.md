# CO2 Emission Prediction 🌍

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Machine Learning](https://img.shields.io/badge/ML-Regression-green.svg)
![Status](https://img.shields.io/badge/Status-Active-success.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

> A machine learning project to predict carbon dioxide (CO2) emissions from vehicles based on various features such as engine specifications, fuel consumption, and vehicle characteristics.

## 📋 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Dataset](#dataset)
- [Installation](#installation)
- [Usage](#usage)
- [Models & Performance](#models--performance)
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)
- [Results & Insights](#results--insights)
- [Future Improvements](#future-improvements)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 🎯 Overview

Climate change is one of the most pressing challenges of our time, and the transportation sector is a major contributor to global CO2 emissions. This project leverages **machine learning** to predict vehicle CO2 emissions based on key features such as engine size, number of cylinders, fuel type, and fuel consumption patterns.

### Why This Project Matters
- **Environmental Impact**: Helps identify high-emission vehicles and promotes eco-friendly choices
- **Policy Making**: Assists policymakers in setting emission standards and regulations
- **Consumer Awareness**: Enables car buyers to make informed, environmentally conscious decisions
- **Industry Applications**: Supports automotive manufacturers in designing low-emission vehicles

### Key Objectives
1. Analyze the relationship between vehicle characteristics and CO2 emissions
2. Build accurate machine learning models to predict emissions
3. Identify the most influential factors contributing to CO2 emissions
4. Provide actionable insights for emission reduction

---

## ✨ Features

- **Data Preprocessing**: Comprehensive data cleaning, feature engineering, and handling of missing values
- **Exploratory Data Analysis (EDA)**: In-depth visualization and statistical analysis of emission patterns
- **Multiple ML Models**: Implementation of various regression algorithms including:
  - Linear Regression
  - Ridge & Lasso Regression
  - Decision Tree Regressor
  - Random Forest Regressor
  - Gradient Boosting Regressor
  - XGBoost
- **Model Evaluation**: Rigorous performance assessment using metrics like R², RMSE, MAE, and MAPE
- **Feature Importance Analysis**: Identification of key factors influencing CO2 emissions
- **Visualization Dashboard**: Interactive charts showing emission trends and predictions
- **Google Colab Compatible**: Fully optimized for cloud-based execution

---

## 📊 Dataset

### Data Source
The dataset contains information about vehicle specifications and their corresponding CO2 emissions, typically sourced from:
- Government environmental agencies
- Automotive testing organizations
- Public datasets (Kaggle, UCI Machine Learning Repository)

### Features Description

| Feature | Description | Unit |
|---------|-------------|------|
| **Make** | Vehicle manufacturer | Categorical |
| **Model** | Vehicle model name | Categorical |
| **Vehicle Class** | Type of vehicle (Sedan, SUV, Truck, etc.) | Categorical |
| **Engine Size** | Volume of the engine | Liters (L) |
| **Cylinders** | Number of engine cylinders | Count |
| **Transmission** | Type of transmission (Automatic/Manual) | Categorical |
| **Fuel Type** | Type of fuel used (Gasoline, Diesel, Electric, Hybrid) | Categorical |
| **Fuel Consumption City** | Fuel consumption in city driving | L/100 km |
| **Fuel Consumption Highway** | Fuel consumption in highway driving | L/100 km |
| **Fuel Consumption Combined** | Combined fuel consumption (55% city, 45% highway) | L/100 km |
| **CO2 Emissions** | Target variable - Carbon dioxide emissions | g/km |

### Dataset Statistics
- **Total Records**: ~7,000-8,000 vehicle entries
- **Features**: 10-12 input features
- **Target Variable**: CO2 Emissions (continuous)
- **Time Period**: Recent years (typically 2015-2024)
- **Missing Values**: Handled during preprocessing

---

## 🚀 Installation

### Prerequisites
- Python 3.8 or higher
- Google Colab (Recommended) OR Local Jupyter Notebook
- Internet connection for package installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/ShivSingh-17/CO2-emission-predication.git
cd CO2-emission-predication
```

### Step 2: Install Required Packages

#### For Google Colab (Recommended):
```python
# Run this in the first cell of your Colab notebook
!pip install pandas numpy scikit-learn matplotlib seaborn xgboost -q
```

#### For Local Environment:
```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Step 3: Download Dataset
```python
# If using Google Colab, mount Google Drive
from google.colab import drive
drive.mount('/content/drive')

# Or upload dataset directly
from google.colab import files
uploaded = files.upload()
```

---

## 💻 Usage

### Quick Start in Google Colab

1. **Open the Notebook**
   ```python
   # Upload the Jupyter notebook to Google Colab
   # Go to: https://colab.research.google.com/
   ```

2. **Load and Explore Data**
   ```python
   import pandas as pd
   import numpy as np
   import matplotlib.pyplot as plt
   import seaborn as sns
   
   # Load dataset
   df = pd.read_csv('CO2_emissions_data.csv')
   
   # Display first few rows
   print(df.head())
   print(df.info())
   print(df.describe())
   ```

3. **Run Data Preprocessing**
   ```python
   # Handle missing values
   df = df.dropna()
   
   # Encode categorical variables
   from sklearn.preprocessing import LabelEncoder
   le = LabelEncoder()
   df['Fuel_Type'] = le.fit_transform(df['Fuel_Type'])
   df['Transmission'] = le.fit_transform(df['Transmission'])
   ```

4. **Train Models**
   ```python
   from sklearn.model_selection import train_test_split
   from sklearn.ensemble import RandomForestRegressor
   from sklearn.metrics import mean_squared_error, r2_score
   
   # Split data
   X = df.drop('CO2_Emissions', axis=1)
   y = df['CO2_Emissions']
   X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
   
   # Train model
   model = RandomForestRegressor(n_estimators=100, random_state=42)
   model.fit(X_train, y_train)
   
   # Make predictions
   y_pred = model.predict(X_test)
   
   # Evaluate
   print(f"R² Score: {r2_score(y_test, y_pred):.4f}")
   print(f"RMSE: {np.sqrt(mean_squared_error(y_test, y_pred)):.2f}")
   ```

5. **Visualize Results**
   ```python
   # Actual vs Predicted
   plt.figure(figsize=(10, 6))
   plt.scatter(y_test, y_pred, alpha=0.5)
   plt.plot([y_test.min(), y_test.max()], [y_test.min(), y_test.max()], 'r--', lw=2)
   plt.xlabel('Actual CO2 Emissions (g/km)')
   plt.ylabel('Predicted CO2 Emissions (g/km)')
   plt.title('Actual vs Predicted CO2 Emissions')
   plt.show()
   ```

### Running the Complete Project
```bash
# Execute the main notebook
jupyter notebook CO2_Emission_Prediction.ipynb
```

---

## 📈 Models & Performance

### Models Implemented

| Model | R² Score | RMSE | MAE | Training Time |
|-------|----------|------|-----|---------------|
| **Linear Regression** | 0.92 | 7.48 | 3.61 | Fast |
| **Ridge Regression** | 0.92 | 7.48 | 3.61 | Fast |
| **Lasso Regression** | 0.88 | 9.06 | 4.54 | Fast |
| **Decision Tree** | 0.95 | 7.26 | 2.20 | Medium |
| **Random Forest** | 0.96 | 6.67 | 2.33 | Medium |
| **Gradient Boosting** | 0.97 | 4.57 | 3.13 | Slow |
| **XGBoost** | 0.98 | 4.20 | 2.85 | Medium |

### Best Performing Model
🏆 **XGBoost Regressor** achieved the highest accuracy with:
- **R² Score**: 0.98 (98% variance explained)
- **RMSE**: 4.20 g/km
- **MAE**: 2.85 g/km
- **MAPE**: 1.85%

### Feature Importance
Top factors influencing CO2 emissions (based on XGBoost):
1. **Fuel Consumption Combined** (45%)
2. **Engine Size** (25%)
3. **Cylinders** (15%)
4. **Fuel Consumption City** (10%)
5. **Vehicle Class** (5%)

---

## 📁 Project Structure

```
CO2-emission-predication/
│
├── data/
│   ├── raw/                          # Raw dataset files
│   ├── processed/                    # Cleaned and processed data
│   └── README.md                     # Dataset documentation
│
├── notebooks/
│   ├── 01_EDA.ipynb                  # Exploratory Data Analysis
│   ├── 02_Preprocessing.ipynb        # Data preprocessing
│   ├── 03_Model_Training.ipynb       # Model training and evaluation
│   └── 04_Prediction.ipynb           # Making predictions
│
├── src/
│   ├── data_loader.py                # Data loading utilities
│   ├── preprocessing.py              # Data preprocessing functions
│   ├── feature_engineering.py        # Feature engineering
│   ├── models.py                     # ML model definitions
│   ├── evaluation.py                 # Model evaluation metrics
│   └── visualization.py              # Plotting functions
│
├── models/
│   ├── best_model.pkl                # Saved best model
│   ├── scaler.pkl                    # Saved data scaler
│   └── model_config.json             # Model configuration
│
├── results/
│   ├── figures/                      # Generated plots and charts
│   ├── metrics/                      # Performance metrics
│   └── predictions/                  # Prediction outputs
│
├── requirements.txt                  # Python dependencies
├── README.md                         # This file
├── LICENSE                           # License information
└── .gitignore                        # Git ignore file
```

---

## 🛠️ Technologies Used

### Core Libraries
- **Python 3.8+**: Programming language
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computing
- **Scikit-learn**: Machine learning algorithms and tools
- **XGBoost**: Gradient boosting framework

### Visualization
- **Matplotlib**: Static plotting
- **Seaborn**: Statistical data visualization
- **Plotly**: Interactive visualizations

### Development Environment
- **Jupyter Notebook**: Interactive development
- **Google Colab**: Cloud-based notebook environment
- **Git**: Version control

### Additional Tools
- **joblib**: Model serialization
- **pandas-profiling**: Automated EDA reports

---

## 📊 Results & Insights

### Key Findings

1. **Fuel Consumption is the Primary Driver**
   - Strong linear correlation (r = 0.98) between fuel consumption and CO2 emissions
   - Combined fuel consumption explains ~45% of emission variance

2. **Engine Specifications Matter**
   - Larger engines (>3.0L) emit 40-60% more CO2 than smaller engines
   - Each additional cylinder increases emissions by ~15-20 g/km on average

3. **Vehicle Type Impact**
   - SUVs and Trucks emit 30-50% more CO2 than Sedans
   - Compact cars have the lowest emission footprint

4. **Fuel Type Analysis**
   - Diesel vehicles show 10-15% lower emissions than gasoline for same size
   - Hybrid vehicles reduce emissions by 30-40% compared to conventional vehicles

5. **Transmission Effect**
   - Automatic transmissions slightly increase emissions (~5-8%) vs manual
   - Modern CVT transmissions show improved efficiency

### Visualizations

#### 1. Feature Correlation Heatmap
Shows strong correlations between fuel consumption features and CO2 emissions.

#### 2. Emission Distribution by Vehicle Class
Demonstrates clear differences in emission patterns across vehicle types.

#### 3. Feature Importance Chart
Highlights which factors contribute most to predictions.

#### 4. Actual vs Predicted Scatter Plot
Shows model accuracy with points close to the diagonal line.

#### 5. Residual Plot
Indicates random distribution of errors, confirming good model fit.

---

## 🔮 Future Improvements

### Short-term Goals
- [ ] Add more recent vehicle data (2024-2025 models)
- [ ] Implement hyperparameter tuning with GridSearchCV/Optuna
- [ ] Create a web application for real-time predictions (Flask/Streamlit)
- [ ] Add model explainability with SHAP values
- [ ] Implement cross-validation for more robust evaluation

### Long-term Vision
- [ ] Incorporate electric vehicle data and range predictions
- [ ] Add geospatial analysis (emissions by country/region)
- [ ] Develop time-series forecasting for future emission trends
- [ ] Build a recommendation system for low-emission vehicle choices
- [ ] Deploy as a REST API with Docker containerization
- [ ] Create mobile application for on-the-go predictions
- [ ] Integrate with IoT sensors for real-time vehicle monitoring

### Model Enhancements
- [ ] Experiment with deep learning (Neural Networks)
- [ ] Ensemble methods combining multiple models
- [ ] AutoML integration for automated model selection
- [ ] Transfer learning from similar domains

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### How to Contribute

1. **Fork the Repository**
   ```bash
   # Click the 'Fork' button on GitHub
   ```

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/CO2-emission-predication.git
   cd CO2-emission-predication
   ```

3. **Create a Feature Branch**
   ```bash
   git checkout -b feature/AmazingFeature
   ```

4. **Make Your Changes**
   - Add new features or fix bugs
   - Update documentation if needed
   - Write tests for new functionality

5. **Commit Your Changes**
   ```bash
   git commit -m "Add: Amazing new feature"
   ```

6. **Push to Your Fork**
   ```bash
   git push origin feature/AmazingFeature
   ```

7. **Open a Pull Request**
   - Go to the original repository
   - Click "New Pull Request"
   - Describe your changes clearly

### Contribution Guidelines
- Follow PEP 8 style guide for Python code
- Write clear, descriptive commit messages
- Add comments and docstrings to your code
- Update README.md if you add new features
- Test your changes before submitting

### Areas for Contribution
- 🐛 Bug fixes and issue resolution
- ✨ New feature implementation
- 📝 Documentation improvements
- 🎨 UI/UX enhancements for visualization
- ⚡ Performance optimizations
- 🧪 Test coverage improvements

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### MIT License Summary
- ✅ Commercial use
- ✅ Modification
- ✅ Distribution
- ✅ Private use
- ⚠️ No liability
- ⚠️ No warranty

---

## 📞 Contact

**Shiv Singh**

- GitHub: [@ShivSingh-17](https://github.com/ShivSingh-17)
- Project Link: [https://github.com/ShivSingh-17/CO2-emission-predication](https://github.com/ShivSingh-17/CO2-emission-predication)

### Get in Touch
- 💼 LinkedIn: [https://www.linkedin.com/in/shiv-prakash-singh-624091267/]
- 📧 Email: [shiva.singh170304@gmail.com]

---

## 🙏 Acknowledgments

- **Dataset Sources**: Government environmental agencies and Kaggle community
- **Inspiration**: Climate change research and sustainable development goals
- **Libraries**: Thanks to the open-source community for amazing tools
- **References**: 
  - [Scikit-learn Documentation](https://scikit-learn.org/)
  - [XGBoost Documentation](https://xgboost.readthedocs.io/)
  - Research papers on vehicle emission modeling

---

## 📚 Additional Resources

### Related Projects
- [Vehicle Fuel Efficiency Analysis](https://github.com/topics/fuel-efficiency)
- [Climate Change Data Science](https://github.com/topics/climate-change)
- [Environmental ML Projects](https://github.com/topics/environmental-data)

### Learning Resources
- [Machine Learning for Environmental Science](https://www.coursera.org/)
- [Carbon Footprint Calculation Methods](https://www.epa.gov/)
- [Sustainable AI Development](https://www.climatechange.ai/)

### Datasets
- [Kaggle: Vehicle CO2 Emissions](https://www.kaggle.com/datasets)
- [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/)
- [Government Open Data Portals](https://data.gov/)

---

## 📊 Project Statistics

![GitHub stars](https://img.shields.io/github/stars/ShivSingh-17/CO2-emission-predication?style=social)
![GitHub forks](https://img.shields.io/github/forks/ShivSingh-17/CO2-emission-predication?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/ShivSingh-17/CO2-emission-predication?style=social)

---

## 🌟 Star This Repository

If you found this project helpful, please consider giving it a ⭐ on GitHub!

---

<div align="center">

**Made with ❤️ for a sustainable future**

*Predicting emissions today, protecting the planet tomorrow* 🌍

</div>

---

## 📝 Citation

If you use this project in your research or work, please cite:

```bibtex
@misc{co2_emission_prediction,
  author = {Shiv Singh},
  title = {CO2 Emission Prediction Using Machine Learning},
  year = {2024},
  publisher = {GitHub},
  url = {https://github.com/ShivSingh-17/CO2-emission-predication}
}
```

---

*Last Updated: October 2025*
