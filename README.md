# library-literacy-analysis
Final project: Programming Historian lesson exploring public library access and literacy rates with Python

**Introduction**

Access to public libraries has long been recognized as a crucial factor in promoting literacy, education, and civic engagement. Studies show that areas with greater library access often exhibit higher literacy rates and educational attainment (NCES, 2020). Yet public investment in libraries varies widely across regions, potentially contributing to inequities in literacy outcomes.
This project explores the question: How does access to public libraries correlate with state-level literacy rates across the United States? Using Python and publicly available datasets, this lesson teaches readers how to analyze, visualize, and interpret geographic and educational data.

**Data Sources:**
1. National Center for Education Statistics (NCES). Public Libraries Survey (PLS) Data and Reports.
Available at: https://nces.ed.gov/surveys/libraries/
2. National Center for Education Statistics (NCES). Adult Literacy in the United States: 2019.
Report link: https://nces.ed.gov/pubs2020/2020070/index.asp
3. U.S. Census Bureau. Small Area Income and Poverty Estimates (SAIPE).
Data available at: https://www.census.gov/programs-surveys/saipe.html
4. American Library Association (ALA). State of America's Libraries Report 2023.
Available at: https://www.ala.org/news/state-americas-libraries-report-2023
5. Pew Research Center. Public Library Usage and Importance Survey Report (2016).
Full report: https://www.pewresearch.org/internet/2016/09/09/libraries-2016/

These sources offer reliable, government-backed data suitable for exploring educational equity through spatial analysis.

**Methods**

The project workflow includes the following steps:
1. Loading Datasets: CSV files containing library locations and literacy rates were imported using pandas.
2. Data Cleaning: Relevant columns were selected, missing values were handled, and datasets were prepared for analysis.
3. Data Merging: Literacy rates were merged with library counts by state, allowing for comparison.
4. Statistical Analysis: Calculated library density (libraries per capita) and compared it to literacy rates.
5. Visualization: Bar charts were created to display libraries per state and literacy rates.

All analysis was conducted using Python, primarily in Jupyter Notebook, using libraries such as pandas, matplotlib, and geopandas.

**Results**

Analysis indicates a strong geographic correlation between public library density and literacy rates. States with a higher number of libraries per capita — such as Vermont, Massachusetts, and Minnesota — tend to report higher literacy rates. Conversely, rural regions in the South and parts of the West, such as Mississippi and New Mexico, show lower literacy rates alongside lower library access.

**Discussion**

These results suggest that access to public libraries may play an important role in supporting adult literacy at the state level. However, the relationship is not uniform; socioeconomic factors such as poverty rates, rural-urban divides, and educational funding also likely contribute to disparities. Further research incorporating poverty data and more sophisticated geographic analysis would strengthen the conclusions.

**Future Directions**

1. Socioeconomic Variables: Integrate poverty and educational spending data to better model the factors influencing literacy rates.
2. Temporal Analysis: Investigate changes over time in library access and literacy rates using longitudinal data.

**Conclusion**

This project demonstrates how digital humanities methods, particularly basic data science and mapping techniques, can be used to uncover patterns of educational equity in the United States. It also highlights the challenges of integrating geographic data and the importance of robust datasets for spatial analysis.


**Programming Lesson**
**Objectives:**

By the end of this tutorial, you will know how to:
- Load public datasets into Python
- Clean and prepare data for analysis
- Calculate library density by state
- Visualize literacy and library data with simple plots
- Conduct a basic correlation analysis

This project demonstrates how digital humanities methods like data analysis can offer insights into infrastructure, social equity, and public policy.

**Prerequisites**
You should have:
- Basic familiarity with Python
- Access to Jupyter Notebook, Google Colab, or a similar Python environment
- The following Python libraries installed: pandas, matplotlib, seaborn
- Install libraries (if needed) using pip:
- python, use code:
```python
bash pip install pandas matplotlib seaborn
```
**Step By Step Tutorial**

**Step 1: Import Libraries using python**

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

**Step 2: Load the Data**
You will need two datasets:
1. A list of public library locations by state (e.g., libraries_by_state.csv)
2. Adult literacy rates by state (e.g., literacy_rates.csv)

You have two CSV files:
1. libraries_by_state.csv; libraries = pd.read_csv('libraries_by_state.csv')
2. literacy_rates.csv ; literacy = pd.read_csv('literacy_rates.csv')

Example structures:
- libraries_by_state.csv columns: State, Library_Count
- literacy_rates.csv columns: State, Literacy_Rate

Load them with:
```python
libraries = pd.read_csv('libraries_by_state.csv')
literacy = pd.read_csv('literacy_rates.csv')
```

**Step 3: Merge the Datasets**
```python
data = pd.merge(libraries, literacy, on='State')  
data.head()
```

**Step 4: Calculate Library Density**

If you have state population data, calculate libraries per 100,000 residents using the following code: 
```python
data['Libraries_per_100k'] = (data['Library_Count'] / data['Population']) * 100000
```
If no population data, proceed with raw counts.

**Step 5: Visualize the Data for Scatterplot of library count vs literacy rate:**
```python
plt.figure(figsize=(10,6))
sns.scatterplot(data=data, x='Library_Count', y='Literacy_Rate')
plt.title('Public Libraries vs Literacy Rate by State')
plt.xlabel('Number of Libraries')
plt.ylabel('Literacy Rate (%)')
plt.grid(True)
plt.show()
```

Scatterplot: Library Density vs Literacy Rate (Optional)
```python
sns.scatterplot(data=data, x='Libraries_per_100k', y='Literacy_Rate')
plt.title('Library Density vs Literacy Rate')
plt.xlabel('Libraries per 100,000 Residents')
plt.ylabel('Literacy Rate (%)')
plt.grid(True)
plt.show()
```

**Step 6: Correlation Analysis**
Calculate Pearson correlation coefficient:
```python
correlation = data['Library_Count'].corr(data['Literacy_Rate'])
print(f'Correlation between number of libraries and literacy rate: {correlation:.2f}')
```


Or calculate with library density using the following code:
```python
correlation = data['Libraries_per_100k'].corr(data['Literacy_Rate'])
print(f'Correlation between library density and literacy rate: {correlation:.2f}')
```
  
Interpretation:
- Closer to 1: strong positive relationship
- Closer to 0: little to no relationship
- Closer to -1: strong negative relationship

**Step 7: Reflection and Future Research**

This basic analysis provides an entry point into understanding how public infrastructure like libraries may relate to educational outcomes. However, many factors influence literacy, including income, school funding, internet access, and language diversity.

Questions for future study:
- How do poverty rates affect the relationship between library access and literacy?
- Are there urban/rural differences in library impacts?
- How have literacy rates changed over time with library expansions or closures?


**Final Note for Students**

Follow the steps in this tutorial to determine if there is a correlation between public library access and literacy rates using the provided datasets.
After visualizing the relationships and running correlation tests, reflect on what additional factors might influence literacy beyond public libraries.

**References**

1. Institute of Museum and Library Services. Public Libraries Survey Data.
2. National Center for Education Statistics (NCES). State and County Literacy Estimates.
3. Becker, Samantha. Opportunity for All: How the American Public Benefits from Internet Access at U.S. Libraries.
4. Johnson, Catherine A. "How Do Public Libraries Create Social Capital? An Analysis of Interactions between Library Staff and Patrons." Library and Information Science Research 34 (2012): 52-62.
5. U.S. Census Bureau. American Community Survey.
