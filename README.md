# library-literacy-analysis
Final project: Exploring public library access and literacy rates with Python

**Introduction**

Public libraries have long been pillars of educational access, providing free resources to communities across the United States. Literacy rates, however, vary widely by region, raising questions about the relationship between library availability and educational outcomes. This lesson will teach you how to use Python to explore this relationship through basic data analysis.

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
- python, use code: !pip install pandas matplotlib seaborn


**Step 1: Import Libraries using python**

Copy the following the code: 
- import pandas as pd
- import matplotlib.pyplot as plt
- import seaborn as sns

**Step 2: Load the Data**
You will need two datasets:
1. A list of public library locations by state (available from IMLS Public Library Survey)
2. Adult literacy rates by state (e.g., from NCES)

Assume you have two CSV files:
1. libraries_by_state.csv; libraries = pd.read_csv('libraries_by_state.csv')
2. literacy_rates.csv ; literacy = pd.read_csv('literacy_rates.csv')

Example structures:
- libraries_by_state.csv columns: State, Library_Count
- literacy_rates.csv columns: State, Literacy_Rate

**Step 3: Merge the Datasets**
1. data = pd.merge(libraries, literacy, on='State')  
2. data.head()

**Step 4: Calculate Library Density**
If you have state population data, calculate libraries per 100,000 residents using the following code: 
- data['Libraries_per_100k'] = (data['Library_Count'] / data['Population']) * 100000

If no population data, proceed with raw counts.

**Step 5: Visualize the Data**
Scatterplot of library count vs literacy rate:  

Copy the following python code:  

plt.figure(figsize=(10,6))  

sns.scatterplot(data=data, x='Library_Count', y='Literacy_Rate')  

plt.title('Public Libraries vs Literacy Rate by State')  

plt.xlabel('Number of Libraries')
plt.ylabel('Literacy Rate (%)')
plt.grid(True)
plt.show()
Scatterplot with library density (optional):

python
Copy code
sns.scatterplot(data=data, x='Libraries_per_100k', y='Literacy_Rate')
Step 6: Correlation Analysis
Calculate Pearson correlation coefficient:

python
Copy code
correlation = data['Library_Count'].corr(data['Literacy_Rate'])
print(f'Correlation between number of libraries and literacy rate: {correlation:.2f}')
Or with library density:

python
Copy code
correlation = data['Libraries_per_100k'].corr(data['Literacy_Rate'])
print(f'Correlation between library density and literacy rate: {correlation:.2f}')
Interpretation:

Closer to 1: strong positive relationship

Closer to 0: little to no relationship

Closer to -1: strong negative relationship

**Step 7: Reflection and Future Research**
This basic analysis provides an entry point into understanding how public infrastructure like libraries may relate to educational outcomes. However, many factors influence literacy, including income, school funding, internet access, and language diversity.

Questions for future study:
-How do poverty rates affect the relationship between library access and literacy?
-Are there urban/rural differences in library impacts?
-How have literacy rates changed over time with library expansions or closures?

Further research could incorporate more variables, use regression models, or explore spatial patterns with mapping tools.

**References**
1. Institute of Museum and Library Services. Public Libraries Survey Data.
2. National Center for Education Statistics (NCES). State and County Literacy Estimates.
3. Becker, Samantha. Opportunity for All: How the American Public Benefits from Internet Access at U.S. Libraries.
4. Johnson, Catherine A. "How Do Public Libraries Create Social Capital? An Analysis of Interactions between Library Staff and Patrons." Library and Information Science Research 34 (2012): 52-62.
5. U.S. Census Bureau. American Community Survey.
