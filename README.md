# Goal
The goal of this project is to predict the sales price of a house using various features from a dataset. The target variable is SalePrice.

# Exploratory Data Analysis (EDA)
## Categorical Features:
MSSubClass,OverallQual,OverallCond

## Discrete Features:
BsmtFullBath, BsmtHalfBath, FullBath, HalfBath, BedroomAbvGr, KitchenAbvGr, TotRmsAbvGrd, Fireplaces, GarageCars, MoSold, YrSold

## Continuous Features:
### Positively Skewed: 
LotFrontage, LotArea, MasVnrArea, BsmtFinSF1, BsmtFinSF2, BsmtUnfSF, TotalBsmtSF, 1stFlrSF, 2ndFlrSF, GrLivArea, WoodDeckSF, OpenPorchSF, EnclosedPorch, ScreenPorch, SalePrice

### Negatively Skewed:
YearBuilt, GarageYrBlt,Bimodal Distribution (Negatively Skewed): YearRemodAdd

### Normally Distributed: GarageArea

# Key Insights from EDA:
## Boxplot Analysis:

1. RL (Residential Low Density) shows the widest range of sale prices.

2. C (Commercial) has the lowest, and FV (Floating Village Residential) has the highest median prices.

3. Paved road and alley access are linked to higher median prices than gravel access.

4. Lot configurations like CulDSac have a larger price range than other configurations.

5. Quality-related factors (e.g., ExterQual, KitchenQual, and BsmtQual) significantly impact prices, with higher quality ratings driving higher sale prices.

## Scatter Plot Analysis:

-Positive correlations exist between SalePrice and features like LotFrontage, LotArea, TotalBsmtSF, GrLivArea, GarageArea, and OpenPorchSF.

-OverallQual has the strongest correlation with SalePrice.

-Other strong correlations include TotRmsAbvGr with GrLivArea (0.83), GarageYrBlt with YearBuilt (0.83), and GarageCars with GarageArea (0.88).

# Data Manipulation

## Missing Data:
-Removed columns with > 15% missing data (e.g., PoolQC, MiscFeature, FireplaceQu).

-Dropped redundant variables like GarageX and BsmtX, as they had missing data and alternatives like GarageCars and BsmtQual provided sufficient information.

-Removed MasVnrArea and MasVnrType due to high correlation with YearBuilt and OverallQual.

-Kept only Electrical, with missing data rows removed.

## Outliers:
-Low outliers were minimal and close to zero.

-High outliers followed the overall trend and were kept to preserve data integrity.

# Model Building
## Models Used:
1. Lasso

2. Ridge Regression

3. XGBoost (with fine-tuning)

4. Random Forest Regressor (with fine-tuning)

# Evaluation Metrics:
-R² (Coefficient of Determination)

-Mean Squared Error (MSE)

# Model Performance:
## Lasso:
MSE: 829,064,489.65

R²: 0.8502

## Ridge Regression:
MSE: 828,472,463.23

R²: 0.8503

## XGBoost:
**Initial** MSE: 710,676,710.92

**Initial** R²: 0.8716

**Fine-tuned:**
-Best Params: {'colsample_bytree': 1.0, 'learning_rate': 0.2, 'max_depth': 3, 'n_estimators': 200, 'subsample': 0.8}

-**Fine-tuned:** MSE: 689,143,595.14

-**Fine-tuned:** R²: 0.8755

## Random Forest Regressor:

**Initial** MSE: 754,231,721.66

**Initial** R²: 0.8637

**Fine-tuned:**
-Best Params: {'max_depth': None, 'max_features': 'sqrt', 'min_samples_leaf': 1, 'min_samples_split': 2, 'n_estimators': 300}

**Fine-tuned:** R²: 0.8513 (overfitting)

# Best Model:
**Fine-tuned XGBoost** achieved the best performance with:

MSE: 689,143,595.14

R²: 0.8755
