# ESG Controversies and Market Event Forecasting

## Project Overview
This project analyzes a dataset of corporate news labeled with **Environmental, Social, and Governance (ESG)** controversies. The goal is to understand how different ESG-related events influence market index movements and to predict future trends in ESG risk for major companies.

---

## Motivation
ESG controversies can significantly influence investor sentiment and stock performance. By exploring historical ESG event data, we aim to uncover patterns that relate controversial events to market responses and estimate future ESG risks for corporations.

---

## Objective
- Classify news articles by ESG controversy category using text data.  
- Analyze the impact of these controversies on market index changes.  
- Forecast the evolution of ESG risk probabilities and related market events for individual companies.

---

## Dataset
The dataset consists of **3,024 news records** with multiple features, including:

- **Date, Headline, Source**: Metadata about each news article.  
- **Market_Event**: Categorized events (e.g., *Product Safety Recall*, *Labor Rights Violation*).  
- **Market_Index** and **Index_Change_Percent**: The market index affected and the percentage change on the event date.  
- **Trading_Volume, Sector**: Additional context for each company.  
- **Sentiment**: Sentiment score of the headline (*Negative*, *Neutral*, *Positive*).  
- **Related_Company**: The company involved in the event.  
- **text_clean**: Preprocessed headline text for analysis.  
- **ESG_Label**: Target controversy category (*Environmental*, *Social*, *Governance*).

The data appears to be a curated collection of corporate news with labeled ESG issues and market outcomes. It is used to explore relationships between ESG controversies and market responses.

---

## Methodology

### 1. Data Exploration
Exploratory data analysis was performed to examine:
- ESG label distribution  
- Sentiment breakdown  
- Sector participation  
- Relationship between ESG categories and market index changes  

An imbalanced label distribution was observed, with many **Governance** controversies and fewer **Environmental** events.

---

### 2. Visualization
Key visualizations include:
- Counts of ESG labels and sentiment categories  
- Heatmaps of sentiment vs. impact level  
- Box plots showing market index changes across ESG labels and event types  
- Bar charts of most-affected companies and news sources  

---

### 3. Text Classification
A text classification model was trained to predict the ESG category from the news headline (`text_clean`).

- **Vectorization**: `TfidfVectorizer`  
  - Max features: 30,000  
  - N-grams: up to 2  
- **Classifier**: `LogisticRegression`  
  - Multinomial  
  - Class-weight balanced  

The model outputs **probability estimates** for each ESG label for every news item.

---

### 4. Time Series Construction
For a given company:
- Predicted ESG probabilities were aggregated over time (sorted by date).  
- A rolling average was applied to smooth short-term fluctuations.

---

### 5. Forecasting

#### ESG Risk Forecasting
- Simple **ARIMA (1,1,1)** models were fitted to each smoothed ESG probability series.  
- Future ESG risk probabilities were forecast for each category.

#### Event Probability Forecasting
- Conditional probabilities were computed from historical data:  

  \[
  P(\text{Event} \mid \text{ESG})
  \]

- Event probabilities were estimated as a weighted sum of ESG probabilities.  
- Short-term forecasts were generated using a **synthetic trend model** to illustrate potential future changes.

---

### 6. Example Analysis
The functions:
- `plot_company_esg_evolution`  
- `plot_company_event_evolution`  

were demonstrated on a specific company (e.g., **JPMorgan Chase**).

These plots show:
- Historical ESG risk probabilities and projected trends  
- Event-specific probability evolution  

Summary statistics (last observed values and forecast ranges) are printed for each event.

---

## Tools and Libraries
- **Python** (Jupyter Notebook or Google Colab)  
- **pandas**, **numpy** – data handling  
- **matplotlib**, **seaborn** – visualization  
- **scikit-learn** – `Pipeline`, `TfidfVectorizer`, `LogisticRegression`  
- **statsmodels** – ARIMA time-series modeling  

---

## Running the Notebook
1. Install required packages (`pandas`, `scikit-learn`, `statsmodels`, `seaborn`).  
2. Place the dataset file (`data (1).csv`) in the working directory or update the file path in `pd.read_csv`.  
3. Open `ESG_Controversies_Events_Expectation.ipynb` in Jupyter or Colab.  
4. Execute the cells sequentially.  
5. *(Optional)* Modify the `company_name` parameter in  
   - `plot_company_esg_evolution`  
   - `plot_company_event_evolution`  
   to analyze other companies.

---

## Results and Insights

### Class Distribution
- The dataset is heavily skewed toward **Governance** controversies.  
- Fewer **Social** and **Environmental** cases are present.

### Sentiment
- Headlines are predominantly **negative** or **neutral**.  
- Most events carry negative sentiment.

### Market Impact
- Environmental controversies show a slightly positive average market index change.  
- Governance and Social events have neutral to slightly negative median effects.

### Top Entities
Most frequently mentioned companies include:
- JPMorgan Chase  
- Chevron  
- Lockheed Martin  
- Intel  
- Bank of America  
- General Motors  
- Ford  
- Microsoft  
- Apple  
- ExxonMobil  

### Model Outputs
- The logistic regression classifier provides ESG probability estimates from headline text.  
- Time-evolution plots show how ESG risks change for individual companies.  

For **JPMorgan Chase**:
- Event probabilities such as *Product Safety Recall* and *Environmental Spill* are forecast to rise.  
- Events like *Climate Regulation Breach* and *Labor Rights Violation* trend downward.

These results illustrate how ESG issue frequencies and perceived risks may evolve, potentially shaping investor expectations.

---

## Limitations and Future Work

### Limitations
- **Data Bias**: Small dataset size and class imbalance may limit generalization.  
- **Model Simplicity**: Basic NLP and time-series models were used.  
- **Forecasting Assumptions**: Event forecasts rely on synthetic trends rather than real market dynamics.  
- **No Direct Price Prediction**: Stock returns were not modeled directly.

### Future Work
- Apply advanced NLP models (e.g., transformers).  
- Use more robust time-series and causal models.  
- Directly link ESG risk forecasts to stock return predictions.  
- Validate the approach on larger and more diverse datasets.
