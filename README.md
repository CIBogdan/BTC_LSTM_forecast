# BTC LSTM Forecast

Acest proiect prezintă un pipeline complet pentru prezicerea prețului BTC folosind modele clasice și LSTM.  

## Structura proiectului

BTC_LSTM_forecast/
│
├── README.md
├── BTC_prediction.ipynb
├── outputs/
│ ├── rezultate_modele_clasice.csv
│ ├── rezumat_multi_target.csv
│ ├── lstm_multi_orizont.csv
│ ├── Serii_temporale_corelatii.png
│ └── Predictii_BTC_multiscenariu_continuu.png
└── notebooks/
└── (alte notebook-uri experimentale)

yaml
Copy code

## Funcționalități principale

- Descărcarea și preprocesarea datelor istorice BTC și macroeconomice.
- Curățarea datelor (eliminare NaN și valori aberante folosind IQR).
- Feature engineering: lag-uri, medii mobile, schimbări procentuale, volum.
- Evaluarea modelelor clasice: Linear Regression, Lasso, Random Forest, XGBoost, SVR, KNN.
- Multi-target framing și evaluarea modelelor RF/XGB/LGBM pe mai mulți indicatori.
- Baseline LSTM univariabil și LSTM multivariabil multi-orizont.
- Vizualizări și analize:
  - Serii temporale pentru BTC_lag1, BTC_lag2, BTC_ma7, BTC_ma14, BTC_diff1, BTC_pct_change
  - Scatter și Cumsum pentru Pearson și Acc-sign
  - Predicții BTC multi-scenariu (continuu)
- Salvarea rezultatelor și artefactelor în folderul `outputs/`.

## Rezultate principale

### Modele clasice (pe setul curat)
| Model             | R2      | MSE        |
|------------------|---------|------------|
| LinearRegression  | 1.0000  | 6.14e-31   |
| Lasso             | 0.9996  | 2.62e-04   |
| RandomForest      | 0.9992  | 4.98e-04   |
| XGBoost           | 0.9991  | 5.98e-04   |
| SVR               | 0.9860  | 9.27e-03   |
| KNN               | 0.9877  | 8.15e-03   |

### Multi-target
| Target         | Pearson | Pearson_cumsum | Acc_sign |
|----------------|---------|----------------|----------|
| BTC_lag1       | 0.807   | 0.999          | 1.0      |
| BTC_lag2       | 0.831   | 0.999          | 1.0      |
| BTC_ma7        | 0.802   | 0.999          | 1.0      |
| BTC_ma14       | 0.818   | 0.999          | 1.0      |
| BTC_diff1      | -0.119  | 0.758          | 0.498    |
| BTC_pct_change | -0.102  | 0.776          | 0.495    |

### LSTM multi-orizont
| Orizont (zile) | RMSE   | Acc_dir | Pearson |
|----------------|--------|---------|---------|
| 1              | 3034.77| 0.422   | 0.795   |
| 5              | 4980.69| 0.476   | 0.119   |
| 7              | 7116.99| 0.429   | -0.059  |

## Cum se rulează

1. Deschide `BTC_prediction.ipynb` în Google Colab sau Jupyter Notebook.  
2. Instalează dependențele dacă nu le ai deja:
```bash
pip install yfinance scikit-learn xgboost lightgbm tensorflow seaborn pandas matplotlib
