
# Product Sales Forecasting API  
*ML-Powered Sales Prediction using Northwind Dataset*  
**Technologies: FastAPI | scikit-learn | PostgreSQL | SQLAlchemy | Swagger | Python**

---

## Project Overview  
This project delivers a machine learning-powered REST API that forecasts product-level sales based on historical transaction data from the Northwind dataset. The API allows integration with external applications for sales insights, retraining, and visual exploration.

---

## Tech Stack  

| Area              | Technology               |
|-------------------|---------------------------|
| Programming       | Python 3.10+              |
| Web Framework     | FastAPI                   |
| Database          | PostgreSQL                |
| ORM               | SQLAlchemy                |
| ML Framework      | scikit-learn              |
| Data Wrangling    | pandas, numpy             |
| Model Persistence | joblib                    |
| API Docs          | Swagger UI (auto-gen)     |
| Testing Tools     | Swagger UI, Postman       |

---

## 🗂️ Project Structure  

```
SalesPredictionApi/
│
├── main.py                      # FastAPI application entry point  
├── requirements.txt             # Project dependencies  
├── processed_data.csv           # Cleaned dataset  
├── monthly_sales_summary.csv    # Aggregated monthly sales  
├── product_sales_summary.csv    # Product-level summaries  
│
└── src/
    ├── model/
    │   └── model.py             # Training, prediction logic  
    ├── utils/
    │   └── data_fetch.py        # SQL data retrieval methods  
    ├── development/
    │   └── data_manipulation.py # Feature engineering functions and data preprocessing 
    └── schemas.py               # Pydantic request/response models  
```

---

## 📈 Project Pipeline  

### A. Data Handling  
- PostgreSQL setup with Northwind schema  
- Analysis of key tables: Orders, Order_Details, Products, Customers  
- Data pulled with SQLAlchemy and transformed via pandas  
- Summary files generated for monthly and product-level trends  
- Feature engineering: month, segment, price bands, etc.

### B. Model Training  
- **Target**: Quantity sold per product  
- Dataset split into training and test sets  
- Regression models trained (e.g. LinearRegression, RandomForest)  
- Evaluation using **R²** and **RMSE**  
- Models saved using joblib as `.pkl` files  

### C. API Development  
The FastAPI backend offers real-time endpoints for product listings, sales prediction, summary reports, retraining, and visual access.

| Endpoint            | Method | Description  |
|---------------------|--------|--------------|
| `/products`         | GET    | Lists all available products  
| `/predict`          | POST   | Returns forecasted sales quantity based on input  
| `/sales_summary`    | GET    | Returns monthly/product sales summaries + visualizations  
| `/retrain`          | POST   | Retrains model using selected ML algorithm  
| `/visualizations`   | GET    | Lists saved model visualizations (charts/metrics)

---

## 🔁 Retraining Endpoint: `/retrain`

- **Method**: POST  
- **Query parameter**: `model_name` (e.g., LinearRegression, DecisionTree, KNN)  
- **Flow**:
  1. Pulls raw data using DataFetch  
  2. Preprocesses via DataManipulation  
  3. Trains selected model  
  4. Evaluates metrics  
  5. Saves model as `best_model.pkl` and features as `feature_columns.pkl`  

---

## 🚀 Run the API Locally  

```bash
# Step 1: Install dependencies
pip install -r requirements.txt

# Step 2: Start the API
uvicorn main:app --reload
```

- Access Swagger UI: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## ✅ Testing & Validation

- Swagger UI for live API testing  
- Postman requests for custom payloads  
- Input validation via Pydantic  
- Error handling: HTTP 200, 422, 500 responses covered  

---

## 🐳 Optional: Docker Setup

```dockerfile
FROM python:3.10  
WORKDIR /app  
COPY . /app  
RUN pip install -r requirements.txt  
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

## 📚 References & Inspirations

- [Northwind Database](https://github.com/engindemirog/Northwind-Database-Script-for-Postgre-Sql/tree/master)  
- FastAPI + Swagger UI integration  
- Real-world eCommerce APIs  

---

## 🌟 Key Highlights

-  Real SQL database integration  
-  Fully modular architecture  
-  Real-time ML prediction via API  
-  End-to-end pipeline: Data → Model → REST API → Docs  
-  Easy retraining and model versioning  

---

## License

This project is licensed under the **MIT License** – feel free to use, modify, and distribute it.