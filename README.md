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

![price-distribution](<insert image path or GitHub notebook output>)

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

