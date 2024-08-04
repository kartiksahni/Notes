Converting scorecard cut-offs to the probability of default (PD) is an important step in assessing credit risk. Here's how this is typically done:

### 1. **Scorecard Model Overview:**
   - **Scorecard:** A credit scorecard is typically built using logistic regression or another statistical model that predicts the likelihood of default based on various factors (e.g., income, credit history, DTI).
   - **Scores:** The output of the scorecard is a score that represents the creditworthiness of an applicant. Higher scores typically indicate lower risk.

### 2. **Relationship Between Score and PD:**
   - **Logistic Regression:** If your scorecard is based on logistic regression, the score is usually a transformation of the underlying probability of default.
   - **Score to PD Mapping:** The relationship between the score and PD is typically monotonic, meaning as the score increases, the PD decreases. The scorecard is calibrated so that each score corresponds to a specific PD.

### 3. **Steps to Convert Score to PD:**

   1. **Score Distribution:** Begin by understanding the distribution of scores in your portfolio.
   
   2. **Calibrate the Scorecard:** 
      - This involves using historical data to calibrate the scorecard, which means mapping each score to the corresponding observed probability of default.
      - This is done by fitting a logistic regression model where the dependent variable is whether a borrower defaulted, and the independent variables are the factors considered in the scorecard.
   
   3. **Calculate the Odds:** 
      - The score is often a linear transformation of the log-odds of default (logistic function).
      - The log-odds are given by:
        \[
        \text{Log-Odds} = \ln\left(\frac{\text{PD}}{1-\text{PD}}\right)
        \]
      - Inverting this equation gives the PD:
        \[
        \text{PD} = \frac{e^{\text{Log-Odds}}}{1 + e^{\text{Log-Odds}}}
        \]
   
   4. **Score to PD Mapping:**
      - Typically, you would have a score range (e.g., 300-850) and a corresponding PD range (e.g., 0% to 100%).
      - For a given score \( S \), you would calculate:
        \[
        S = \text{Intercept} + \text{Coefficient} \times \text{Log-Odds}
        \]
      - Rearranging this gives the Log-Odds, which you then convert to PD.

### 4. **Practical Example:**
   - Let’s say you have a score \( S \) and want to find the PD:
     1. **Determine the Intercept and Coefficient:** These are derived from your logistic regression model.
     2. **Calculate Log-Odds:**
        \[
        \text{Log-Odds} = \frac{S - \text{Intercept}}{\text{Coefficient}}
        \]
     3. **Convert Log-Odds to PD:**
        \[
        \text{PD} = \frac{e^{\text{Log-Odds}}}{1 + e^{\text{Log-Odds}}}
        \]

### 5. **Score Cut-Off to PD:**
   - When you increase the score cut-off, you are essentially requiring a higher creditworthiness threshold for approval.
   - By determining the score associated with your new cut-off, you can convert that score to a corresponding PD, which represents the maximum acceptable default probability for approved loans.

### 6. **Validation:**
   - **Back-testing:** Validate the PD estimates against actual outcomes to ensure accuracy.
   - **Monitoring:** Continuously monitor how well the score-to-PD mapping performs over time, especially in changing economic conditions.
