
# Load Prediction Project

This project is about predicting electricity load (demand) using historical energy data together with weather information. The dataset includes different time resolutions (1-minute, 15-minute, 1-hour), and the notebook walks through how to prepare the data, explore it, and build inputs for machine learning models.

---

## What’s in here

- `loadprediction (3).ipynb` → the main notebook with all steps (data prep + analysis)  
- `reduced_data.zip` → compressed dataset (electricity + weather)  
- `prepared/` → folder created by the notebook with processed data ready for ML/DL models  
- `eda/` → folder created by the notebook with plots from exploratory analysis  

---
## Dataset

The dataset is too large to upload directly to GitHub.  

You can download it here:  
👉 [Download reduced_data.zip](https://drive.google.com/file/d/18OBecFxsV4fNe_AQjc8Kjhm7OzQsSRBl/view?usp=drive_link)  

After downloading:  
1. Place `reduced_data.zip` in the root of this repository.  
2. Run the notebook `loadprediction (3).ipynb`.  
   - The notebook will automatically extract the contents into a folder called `reduced_data/`.  
   
## Requirements

- Python 3.8+  
- Jupyter Notebook  
- Some common packages:  
  ```bash
  pip install numpy pandas matplotlib scikit-learn torch flwr tqdm
  ```

---

## Dataset

Unzip `reduced_data.zip` first:

```bash
unzip reduced_data.zip -d reduced_data
```

Inside, you’ll see three subfolders:  

- `1min/` → one-minute resolution data  
- `15min/` → 15-minute resolution data  
- `1h/` → one-hour resolution data  

Each contains:  
- `electricity_P.csv.gz` (active power: total, PV, CHP)  
- `electricity_W.csv.gz` (energy in Wh)  
- `heating_P.csv.gz`, `cooling_P.csv.gz`  
- `weather.csv.gz` (irradiance, temperature, etc.)  

---

## How to use

1. Unzip the dataset as shown above.  
2. Start Jupyter Notebook:  
   ```bash
   jupyter notebook
   ```  
3. Open `loadprediction (3).ipynb` and run through the cells.  
   - The notebook checks and extracts the dataset.  
   - Cleans and merges weather + electricity data.  
   - Builds new features (lags, rolling averages, time features).  
   - Splits into train/validation/test.  
   - Saves everything into `prepared/`.  
   - Runs EDA and saves plots under `eda/`.  

---

## What the notebook does

- Aggregates raw data to hourly values.  
- Creates features like:
  - Hour of day, day of week, weekend/weekday.  
  - Lagged load values (1h, 2h, 3h, 6h, 12h, 24h).  
  - Rolling statistics over short and long windows.  
- Defines the prediction target: **next hour’s total load**.  
- Produces plots such as:
  - Load and PV time series.  
  - Daily/weekly load profiles.  
  - Load vs. temperature and irradiance.  
  - Load duration curve.  
  - Autocorrelation.  
  - Correlation matrix between load, weather, and generation.  

---

## Next steps (things to try)

- Train regression models (Random Forest, XGBoost, etc.).  
- Train sequence models like LSTMs or Transformers on the prepared datasets.  
- Experiment with federated learning (the notebook is already set up with Flower).  
- Add external signals such as holidays or special events.  
- Build a simple API to serve predictions.  

---

## Author

Shiva Sai Dhanush Manda  
