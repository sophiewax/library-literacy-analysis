# library-literacy-analysis
Final project: Exploring public library access and literacy rates with Python

**Introduction**

Public libraries have long been pillars of educational access, providing free resources to communities across the United States. Literacy rates, however, vary widely by region, raising questions about the relationship between library availability and educational outcomes. This project explores the correlation between public library access and regional literacy rates across the United States. The guiding research question is: How does the density and availability of public libraries correlate with literacy levels, particularly in regions affected by systemic inequalities? This study explores how disparities in library infrastructure may reveal larger patterns of educational inequity, especially between rural and urban areas, and across economically disadvantaged regions.

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

**Methods**
1.	Data Cleaning:
- Cleaning steps included removing duplicate entries, standardizing state names, and filtering for active library branches.
- Standardized state names and abbreviations across datasets.
- Filtered public library data to active, physical branches only.
2.	Data Integration:
- Merged literacy rates with library density information at the state level.
- Created new variables, such as libraries per 100,000 residents, for better comparability.
3.	Preparation for Spatial Analysis:
- Datasets formatted for GIS visualization (CSV files ready for upload into ArcGIS).
- Plan to create heat maps displaying Library density by region, Literacy rates, and Poverty overlays (future work)

Preliminary observations suggest that states with higher library access tend to have higher literacy rates, while regions with fewer libraries per capita often experience lower literacy. Rural areas particularly demonstrate these disparities, suggesting that geographic isolation compounds educational inequality.

Preliminary visualization efforts suggest notable regional disparities, particularly in rural Southern states. Full GIS mapping is in progress and will be included in future versions.

## Results

Analysis indicates a strong geographic correlation between public library density and literacy rates. States with a higher number of libraries per capita — such as Vermont, Massachusetts, and Minnesota — tend to report higher literacy rates. Conversely, rural regions in the South and parts of the West, such as Mississippi and New Mexico, show lower literacy rates alongside lower library access.


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
- data = pd.merge(libraries, literacy, on='State')  
- data.head()

**Step 4: Calculate Library Density**
If you have state population data, calculate libraries per 100,000 residents using the following code: 
- data['Libraries_per_100k'] = (data['Library_Count'] / data['Population']) * 100000

If no population data, proceed with raw counts.

**Step 5: Visualize the Data for Scatterplot of library count vs literacy rate:**

Copy the following python code:  
- plt.figure(figsize=(10,6))  
- sns.scatterplot(data=data, x='Library_Count', y='Literacy_Rate')  
- plt.title('Public Libraries vs Literacy Rate by State')  
- plt.xlabel('Number of Libraries')
- plt.ylabel('Literacy Rate (%)')
- plt.grid(True)
- plt.show()
- Scatterplot with library density (optional):

In a seperate block copy the following python code for scatterplot with library density (optional):
- sns.scatterplot(data=data, x='Libraries_per_100k', y='Literacy_Rate')

**Step 6: Correlation Analysis**
Calculate Pearson correlation coefficient:
- correlation = data['Library_Count'].corr(data['Literacy_Rate'])
- print(f'Correlation between number of libraries and literacy rate: {correlation:.2f}')


Or calculate with library density using the following code:
- correlation = data['Libraries_per_100k'].corr(data['Literacy_Rate'])
- print(f'Correlation between library density and literacy rate: {correlation:.2f}')

  
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


Further research could incorporate more variables, use regression models, or explore spatial patterns with mapping tools.

Other Future Directions:
1. Mapping Literacy Inequality: Develop interactive GIS maps using ArcGIS StoryMaps or ArcGIS Online.
2. Multivariable Analysis: Overlay poverty data to see how economic status interacts with library access and literacy.
3. Granular Analysis: Refine data to the county or ZIP code level for more detailed regional insights.
4. Historical Analysis: Investigate how historical patterns of library development correlate with present-day literacy gaps.


**Students:**

Follow the above lesson to determine if there is a correlation between public library access and literacy rates using the provided csv files. 


After visualizing the relationshjip with the scatterplots and running a correlation test, reflect on what factors influence literacy beyond libraries.


**References**
1. Institute of Museum and Library Services. Public Libraries Survey Data.
2. National Center for Education Statistics (NCES). State and County Literacy Estimates.
3. Becker, Samantha. Opportunity for All: How the American Public Benefits from Internet Access at U.S. Libraries.
4. Johnson, Catherine A. "How Do Public Libraries Create Social Capital? An Analysis of Interactions between Library Staff and Patrons." Library and Information Science Research 34 (2012): 52-62.
5. U.S. Census Bureau. American Community Survey.
