# 🚗 What Drives the Price of a Car?
## CRISP-DM Project Report

---

## 1. Business Understanding

### 🎯 Objective
The goal of this project is to help a **used car dealership** understand what factors influence the price of a used car. By analyzing a large dataset of used vehicles, we aim to uncover patterns and relationships between car features and their market value.

The dealership can use these insights to:
- Make smarter inventory decisions
- Price vehicles more accurately
- Increase profitability

---

### 💼 Key Business Questions
- Do newer cars have higher resale prices?
- How does mileage (odometer reading) affect car price?
- Are certain **brands or models** priced higher?
- Does the **condition** of the car impact its value?
- What about features like **transmission type**, **fuel type**, or **drive train**?

---

### 🎯 Target Variable
- **`price`** — This is the column we want to predict.

---

### 📦 Important Features to Explore
- `year`: Indicates the age of the car
- `odometer`: Mileage; often a key factor in value
- `manufacturer` and `model`: Brand influence
- `condition`: Reported physical/working condition
- `cylinders`, `fuel`, `title_status`, `transmission`, `drive`
- `type`: SUV, truck, sedan, etc.
- `paint_color`: May or may not influence price

---

### 🧠 Business Impact
By answering these questions, the dealership will know what car features to prioritize in their purchasing and pricing strategies. The outcome will guide **data-driven decisions** instead of relying solely on intuition or guesswork.


## 2. Data Understanding

We analyzed a dataset of **426,880 used cars** with 18 columns. Below is a filtered price distribution for vehicles priced between $1,000 and $100,000 (to remove outliers).

### 📊 Distribution of Used Car Prices

The majority of used cars are priced between **$5,000 and $20,000**, with a long tail extending toward luxury models up to $100,000.

![price-distribution](<Output/Image/Distribution of Used Car Prices (Filtered).png>)

---

### 🔍 Key Observations So Far:
- Prices are **right-skewed**, meaning most cars are on the lower end of the price range.
- We should investigate how features like `year`, `odometer`, `manufacturer`, and `condition` affect this distribution.

---

### 👇 Next Visualizations:
We will now explore relationships between price and key features:
- **Price vs. Car Year**
- **Price vs. Odometer (mileage)**
- **Boxplots by Condition, Transmission, Drive, and Manufacturer**

These visualizations will help answer the question:  
> What features most influence used car prices?

### 📈 Price vs. Year

We examined how the age of the car (based on model year) affects its price.

![Price vs. Year](<>)

#### Key Takeaways:
- As expected, **newer cars are generally more expensive**.
- The pattern is exponential: cars made after 2015 show a steep increase in price.
- There's a wide price range within each year, suggesting other variables (e.g., brand, mileage) are also important.

➡️ This confirms that **year** is a strong predictor for price and should be included in modeling.

### 📉 Price vs. Odometer

We examined the relationship between mileage (odometer reading) and used car prices.

![Price vs. Odometer](<>)

#### Key Takeaways:
- There is a **clear negative correlation**: as mileage increases, price tends to decrease.
- Most cars cluster under **200,000 miles**, with a steep price drop in higher mileage vehicles.
- Some rare exceptions exist with high mileage and high price, likely due to luxury brands or special modifications.

➡️ Conclusion: **Mileage is a strong inverse predictor** for car price and will be important in modeling.

### 📦 Price by Condition

We used a boxplot to explore how reported vehicle condition affects used car price.

![Price by Condition](<>)

#### Key Takeaways:
- Cars listed as **"new"** or **"like new"** have the **highest median prices**.
- As condition worsens (e.g., "salvage" or "fair"), prices drop significantly.
- There’s some overlap between "good" and "excellent", suggesting inconsistency in how sellers label condition.

➡️ Condition is a valuable feature for predicting price, especially for distinguishing very high or very low value vehicles.

### 🔧 Price by Transmission Type

We analyzed how different transmission types affect used car prices.

![Price by Transmission](<>)

#### Key Takeaways:
- **Automatic transmission** cars dominate the market and show a wide price range.
- **Manual transmission** vehicles tend to be priced lower, possibly due to limited demand.
- **"Other"** transmission types (likely CVT, semi-automatic, etc.) show higher median prices, but this may reflect niche/luxury models.

➡️ Transmission type adds moderate predictive power to price, especially for segmenting buyer preference.

### 🚗 Price by Drive Type

This chart shows how drive type (e.g., front-wheel, rear-wheel, all-wheel) relates to price.

![Price by Drive Type](<>)

#### Key Takeaways:
- **4WD (Four-Wheel Drive)** vehicles have **higher median prices**, likely because of trucks, SUVs, and off-road capability.
- **FWD (Front-Wheel Drive)** cars tend to be more affordable and are common in economy vehicles.
- **RWD (Rear-Wheel Drive)** sits in between and includes a mix of sedans, trucks, and sports cars.

➡️ Drive type provides insight into **vehicle category and use case**, which helps predict price.

### 🏷️ Price by Manufacturer (Top 10)

This boxplot shows how prices vary among the 10 most common car manufacturers in the dataset.

![Price by Manufacturer](<>)

#### Key Takeaways:
- **Ford, Chevrolet, and Toyota** dominate the dataset and have a wide price range.
- **Ram and GMC** have noticeably higher median prices, possibly due to pickup truck value.
- **Honda and Nissan** are clustered in the mid-range but offer more consistent pricing.

➡️ Manufacturer is a useful feature for capturing brand-level pricing trends and should be included in the model.

## 3. Data Preparation

Before modeling, we cleaned and transformed the data to ensure it was usable and meaningful.

### ✅ Cleaning Steps:
- Removed records with **missing or zero prices**
- Removed records with missing key features like:
  - `odometer`
  - `manufacturer`
  - `condition`
  - `fuel`
  - `transmission`
  - `drive`

### 🆕 Created Feature:
- `car_age` = current year − model year  
  This gives us a more interpretable measure of how old the car is.

### 💡 Sample of Cleaned Data

| Price ($) | Car Age | Odometer (miles) | Manufacturer | Condition | Fuel | Transmission | Drive |
|-----------|---------|------------------|--------------|-----------|------|---------------|-------|
| 28,500    | 10      | 73,400           | Toyota       | Excellent | Gas  | Automatic     | 4WD   |
| 8,000     | 46      | 60,000           | Chevrolet    | Good      | Gas  | Automatic     | RWD   |
| 17,950    | 11      | 181,367          | Chevrolet    | Excellent | Gas  | Automatic     | RWD   |
| 24,990    | 8       | 21,384           | Jaguar       | Good      | Diesel | Automatic  | RWD   |
| 7,500     | 16      | 232,500          | Chevrolet    | Excellent | Gas  | Automatic     | 4WD   |

---

➡️ The dataset is now ready for feature encoding and modeling in the next step.

## 4. Modeling

We built two regression models to predict used car prices based on features such as age, mileage, manufacturer, fuel type, and condition.

### 🧠 Models Used
1. **Linear Regression**
2. **Decision Tree Regressor** (with max depth = 10)

We applied **one-hot encoding** to categorical features:
- `manufacturer`, `condition`, `fuel`, `transmission`, `drive`

Data was split into:
- 80% training set
- 20% testing set

---

### 📊 Model Performance

| Model                | MAE ($) | RMSE ($) |
|---------------------|---------|----------|
| Linear Regression    | 6,459   | 9,184    |
| Decision Tree Regressor | 4,119   | 6,384    |

**MAE (Mean Absolute Error)** tells us the average error in dollars.  
**RMSE (Root Mean Squared Error)** penalizes large mistakes more heavily.

---

### 💡 Interpretation
- The **Decision Tree Regressor** performs significantly better than linear regression, suggesting it captures non-linear relationships more effectively.
- Linear regression may underperform due to complex interactions among car features.

➡️ The Decision Tree model will be used to guide final recommendations.

## 5. Evaluation and Feature Importance

We used the Decision Tree Regressor to extract **feature importance scores**, which help explain which variables most strongly affect car pricing.

### 🎯 Top 10 Most Important Features

| Feature              | Importance |
|----------------------|------------|
| `car_age`            | 53.9%      |
| `drive_fwd`          | 16.7%      |
| `odometer`           | 14.5%      |
| `fuel_gas`           | 5.1%       |
| `condition_good`     | 1.6%       |
| `transmission_other` | 1.1%       |
| `fuel_other`         | 0.8%       |
| `manufacturer_subaru`| 0.7%       |
| `drive_rwd`          | 0.6%       |
| `manufacturer_chevrolet` | 0.5%   |

---

### 🧠 Interpretation
- **Car age** is by far the strongest predictor — newer cars have higher prices.
- **Drive type** matters: Front-wheel drive (`drive_fwd`) is more common and shows significant pricing patterns.
- **Odometer** (mileage) has a clear negative impact on price.
- Most **manufacturer** and **fuel-type** features had much smaller contributions, indicating that buyers focus more on vehicle condition and usage than brand alone.

---

➡️ These insights will guide our final recommendations to the used car dealership.

## 6. Deployment & Business Recommendations

This analysis was conducted for a used car dealership looking to understand which features drive pricing. Based on data from over 400,000 used vehicles, our analysis and models provide the following key recommendations:

---

### 📌 Recommendations for the Dealership

1. **Prioritize Newer Cars (Lower Car Age)**  
   Car age is the single strongest driver of price. Focus on acquiring vehicles that are less than 10 years old for higher resale value.

2. **Mileage Matters**  
   Buyers clearly prefer lower mileage vehicles. Avoid stocking cars with extremely high odometer readings (over 150,000 miles), as they significantly reduce value.

3. **Drive Type Impacts Price**  
   Vehicles with **4WD or FWD** tend to have higher prices than RWD. Target inventory that includes more 4WD and FWD options, especially for trucks and SUVs.

4. **Condition Reporting Should Be Consistent**  
   Listings marked as "excellent" or "like new" command better prices. Ensure condition assessments are accurate and well-documented to build buyer trust.

5. **Transmission and Fuel Type Have Moderate Influence**  
   While automatic transmissions and gasoline engines are most common, they do not drastically affect price on their own. These should be considered secondary factors.

---

### 🧾 Business Use
These recommendations can be used to:
- Fine-tune **inventory purchasing strategies**
- Improve **pricing accuracy**
- Guide **advertising and marketing messaging** based on what buyers value most

---

📂 [View Full Notebook with Code](Input/Code/prompt_II.ipynb)  
📁 [Download Dataset](practical_application_II_starter/data/vehicles.csv)

