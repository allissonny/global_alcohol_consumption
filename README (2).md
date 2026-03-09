# Global Alcohol Consumption Analysis (WHO 2000--2022)

## Project Overview

This project analyzes global alcohol consumption trends using
country-level data derived from the **World Health Organization Global
Health Observatory**. The goal of the analysis is to identify long-term
consumption patterns, detect countries experiencing significant
increases in alcohol use, and demonstrate how clustering and forecasting
techniques can support public health monitoring and policy planning.

Alcohol consumption is a major global health concern and contributes to
a range of chronic diseases and social harms. Understanding how
consumption patterns evolve across countries can help policymakers and
public health organizations identify emerging risks and develop targeted
prevention strategies.

This project applies exploratory data analysis, clustering, and
predictive modeling techniques to evaluate alcohol consumption trends
from **2000 to 2022**.

------------------------------------------------------------------------

## Dataset

**Source:**\
World Health Organization Global Health Observatory\
Available via Kaggle

Dataset:\
Global Alcohol Consumption (WHO 2000--2022)

The dataset includes annual estimates of alcohol consumption for
countries worldwide.

### Key Variables

  -----------------------------------------------------------------------
  Variable                            Description
  ----------------------------------- -----------------------------------
  Country                             Name of the country

  Year                                Observation year

  Alcohol_Consumption                 Liters of pure alcohol consumed per
                                      capita (age 15+)
  -----------------------------------------------------------------------

This metric includes both recorded alcohol sales and estimated
unrecorded consumption.

------------------------------------------------------------------------

## Project Goals

The primary objectives of this project are:

-   Analyze global alcohol consumption trends over time\
-   Identify countries with significant increases in consumption\
-   Group countries with similar consumption patterns using clustering\
-   Demonstrate forecasting techniques to estimate future consumption
    trends\
-   Provide insights that could support public health monitoring and
    policy planning

------------------------------------------------------------------------

## Methods

### Data Preparation

``` python
df = pd.read_csv("global_alcohol_consumption.csv")

df = df[['Country', 'Year', 'Alcohol_Consumption']].copy()

df['Year'] = pd.to_numeric(df['Year'], errors='coerce')
df['Alcohol_Consumption'] = pd.to_numeric(df['Alcohol_Consumption'], errors='coerce')

df = df.dropna(subset=['Country', 'Year', 'Alcohol_Consumption'])
```

### Exploratory Data Analysis

``` python
global_trend = df.groupby('Year')['Alcohol_Consumption'].mean().reset_index()

plt.figure(figsize=(10,6))
plt.plot(global_trend['Year'], global_trend['Alcohol_Consumption'], marker='o')
plt.title("Global Alcohol Consumption Trend")
plt.xlabel("Year")
plt.ylabel("Liters of Pure Alcohol Per Capita")
plt.show()
```

### Clustering Analysis

Countries were grouped using **K-Means clustering** based on trend
features.

``` python
X = features_df[['Avg_Level','Slope','Volatility','Change_Period']]

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

kmeans = KMeans(n_clusters=5, random_state=42)
features_df['Cluster'] = kmeans.fit_predict(X_scaled)
```

### Forecasting

A simple linear regression model was used to demonstrate forecasting of
alcohol consumption trends.

``` python
x = country_data['Year']
y = country_data['Alcohol_Consumption']

m, b = np.polyfit(x, y, 1)

future_years = np.arange(x.min(), x.max()+6)
forecast_values = m * future_years + b
```

------------------------------------------------------------------------

## Key Insights

-   Alcohol consumption patterns vary widely across countries.
-   Some countries maintain relatively stable consumption levels.
-   Other countries demonstrate increasing consumption trends.
-   Clustering analysis reveals distinct global consumption profiles.
-   Forecasting methods can help anticipate potential future public
    health challenges.

------------------------------------------------------------------------

## Visualizations

This project includes several visualizations used to analyze alcohol
consumption patterns:

-   Global alcohol consumption trend (2000--2022)
-   Countries with largest increases in consumption
-   Distribution of alcohol consumption across countries
-   Cluster analysis of country consumption patterns
-   Forecast example
-   Global alcohol consumption map (2022)

Example visualization code:

``` python
fig = px.choropleth(
    df_2022,
    locations="Country",
    locationmode="country names",
    color="Alcohol_Consumption",
    hover_name="Country",
    color_continuous_scale="Reds",
    title="Global Alcohol Consumption by Country (2022)"
)

fig.show()
```

------------------------------------------------------------------------

## Tools and Technologies

-   Python
-   Pandas
-   NumPy
-   Matplotlib
-   Plotly
-   Scikit-learn
-   Jupyter Notebook

------------------------------------------------------------------------

## Repository Structure

    global-alcohol-consumption-analysis
    │
    ├── alcohol_consumption_analysis.ipynb
    ├── project_report.pdf
    ├── presentation_slides.pdf
    ├── figures/
    │   ├── global_trend.png
    │   ├── top_countries_increase.png
    │   ├── consumption_distribution.png
    │   ├── cluster_analysis.png
    │   ├── forecast_example.png
    │   └── world_consumption_map.png
    └── README.md

------------------------------------------------------------------------

## References

World Health Organization. (2024). *Global status report on alcohol and
health.*

World Health Organization Global Health Observatory.

World Bank. *Total alcohol consumption per capita (liters of pure
alcohol, 15+ years of age).*

Our World in Data. *Alcohol consumption dataset.*

------------------------------------------------------------------------

## Author

**Allison Evanich**\
Master of Science in Data Science\
Bellevue University

------------------------------------------------------------------------

## Future Improvements

Future work could expand this project by incorporating:

-   Alcohol taxation policies
-   Alcohol-related mortality rates
-   Socioeconomic indicators
-   Advanced forecasting models
-   Regional policy comparisons
