### **Advanced Data Analysis Example in Excel: Predicting Employee Attrition Using Logistic Regression (Without Add-ins)**  

#### **Scenario:**  
A company wants to **predict employee attrition** (whether an employee will leave or stay) based on factors like **salary, experience, and work-life balance**. We will use **Logistic Regression manually** in Excel using the **logit function and odds ratio**.

---

### **Step 1: Prepare the Data**  
Create a dataset in Excel with the following columns:

| Employee ID | Salary ($) | Experience (Years) | Work-Life Balance (1-5) | Attrition (1=Left, 0=Stayed) |
|------------|-----------|------------------|----------------------|------------------|
| 101        | 50000     | 3                | 2                    | 1                |
| 102        | 70000     | 5                | 4                    | 0                |
| 103        | 55000     | 4                | 3                    | 1                |
| 104        | 80000     | 6                | 5                    | 0                |
| 105        | 45000     | 2                | 1                    | 1                |
| 106        | 75000     | 7                | 4                    | 0                |
| 107        | 60000     | 5                | 3                    | 1                |
| 108        | 85000     | 8                | 5                    | 0                |
| 109        | 40000     | 1                | 1                    | 1                |
| 110        | 90000     | 10               | 5                    | 0                |

---

### **Step 2: Calculate Log Odds (Logit Function)**
Logistic Regression is based on the **logit transformation**:

\[
\log(\frac{p}{1 - p}) = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3 X_3
\]

Where:
- **p** = Probability of Attrition
- **X₁** = Salary  
- **X₂** = Experience  
- **X₃** = Work-Life Balance  
- **β₀, β₁, β₂, β₃** = Coefficients to be estimated  

#### **1. Compute Log Odds Using Regression Approximation**
Use Excel’s **LINEST function** to estimate **β coefficients**:

```
=LINEST(E2:E11, B2:D11, TRUE, TRUE)
```

This returns **β values**, which can be used in:

\[
\text{Log Odds} = \beta_0 + \beta_1(\text{Salary}) + \beta_2(\text{Experience}) + \beta_3(\text{Work-Life Balance})
\]

#### **2. Compute Predicted Probability (p)**
Convert **log odds** to probability using:

\[
p = \frac{e^{\text{Log Odds}}}{1 + e^{\text{Log Odds}}}
\]

Use Excel’s **EXP function**:

```
=EXP(F2)/(1+EXP(F2))
```

---

### **Step 3: Classify Employees Based on Probability**
- If **p > 0.5** → Predict "Will Leave"
- If **p ≤ 0.5** → Predict "Will Stay"

Use:

```
=IF(G2>0.5, "Will Leave", "Will Stay")
```

---

### **Step 4: Evaluate Accuracy with Confusion Matrix**
Create a **Confusion Matrix** in Excel:

| Actual \ Predicted | Will Leave | Will Stay |
|--------------------|-----------|-----------|
| **Left (1)**       | TP        | FN        |
| **Stayed (0)**     | FP        | TN        |

Use:

- **True Positives (TP)** → `COUNTIFS(Predicted="Will Leave", Actual=1)`
- **False Positives (FP)** → `COUNTIFS(Predicted="Will Leave", Actual=0)`
- **False Negatives (FN)** → `COUNTIFS(Predicted="Will Stay", Actual=1)`
- **True Negatives (TN)** → `COUNTIFS(Predicted="Will Stay", Actual=0)`

Calculate **Accuracy**:

\[
\text{Accuracy} = \frac{TP + TN}{TP + FP + FN + TN}
\]

---

### **Step 5: Visualizing Attrition Risk**
1. **Insert a Scatter Plot**
   - X-axis: Salary
   - Y-axis: Experience
   - Color by predicted **attrition risk**.

2. **Conditional Formatting**
   - Color **high attrition risk employees (p > 0.5)** in red.
   - Color **low attrition risk employees (p ≤ 0.5)** in green.

---

### **Conclusion**
- **Logistic Regression in Excel (manually)** predicts employee attrition.
- Helps **HR teams take proactive retention strategies**.
- **No need for add-ins or complex formulas.**

Would you like an example using time series forecasting instead?
