# 🥑 Avocado Price Prediction Project with Azure Databricks

This project demonstrates a complete **Data Engineering** and **Machine Learning** pipeline using **Azure Databricks**, **Azure Data Lake**, and **scikit-learn**, structured around the **Medallion Architecture** (Bronze → Silver → Gold).  
The dataset contains avocado sales data across US regions, including prices, volume, and type (organic/conventional).

---

## 📂 Project Structure: Medallion Architecture

### 🔸 Bronze Layer
- Raw source ingestion from a mounted Azure Data Lake container:
/mnt/Avocado_Project/Bronze/avocado_dataset.csv

---

### 🔸 Silver Layer
- Renamed columns for clarity and consistency
- Converted `date` to Spark `DateType` and extracted `year`
- Removed duplicates and handled nulls
- Categorical encoding:
- `type` and `region` transformed using `StringIndexer` and `OneHotEncoder`
- Two versions saved:
- `avocado_silver.parquet`: cleaned data with original categories
- `avocado_silver_ml_ready.parquet`: data with encoded features ready for ML

Saved to:/mnt/Avocado_Project/Silver/avocado_silver.parquet AND 
/mnt/Avocado_Project/Silver/avocado_silver_ml_ready.parquet


---

### 🔸 Gold Layer

#### 📊 Data Visualization
- Total volume by Hass type: bar chart (`SmallHass`, `LargeHass`, `XLargeHass`)
- Top 10 regions by volume: pie chart
- Total volume by type (`organic` vs `conventional`)
- Average price by type

#### 🤖 Machine Learning Workflow

- Converted encoded vectors (`type_vec`, `region_vec`) into usable numerical columns:
  - `type_bin`: 0 for conventional, 1 for organic
  - `region_index`: integer ID for region
- Removed rows with invalid regions
- Train/test split: 70% training, 30% test

#### 🧠 Models Trained with GridSearchCV

| Model              | RMSE   | R²    | Notes                        |
|--------------------|--------|--------|------------------------------|
| Random Forest      | 0.144  | 0.851  | 🏆 Best overall performance |
| KNN                | 0.145  | 0.849  | Very close to RF             |
| MLP Neural Network | 0.195  | 0.726  | Good performance             |
| SVM (RBF)          | 0.197  | 0.722  | Costly, but stable           |
| Decision Tree      | 0.171  | 0.789  | Decent, but lower than RF    |
| Linear Regression  | 0.254  | 0.536  | Weak performance             |

#### 📈 Visual Outputs
- Bar plots comparing **RMSE** and **R²** side-by-side for all models
- Rankings with labels and grid for better readability

#### 💾 Final Outputs
- Gold dataset saved to:/mnt/Avocado_Project/Gold/avocado_gold.parquet


## ⚙️ Technologies Used

- **Azure Databricks**
- **Azure Data Lake Gen2**
- **Apache Spark (PySpark)**
- **Scikit-learn**
- **Matplotlib / Seaborn / Pandas**
- **Medallion Architecture (Bronze, Silver, Gold)**

---

## 📫 Contact

**Diovanni Antonelli**  
Data Analyst | ML Enthusiast
📍 Brazil  
📧 dioantonellias@gmail.com  
🔗 https://www.linkedin.com/in/diovanni-antonelli/
