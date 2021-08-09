## Modelling Film Revenue 

- **Objective:** To apply multiple regression models to data acquired from TMDB and IMDB in order to predict movie revenue and conduct regression analysis using Python/Pandas/Sci-Kit Learn

- **Results:** Used a tiered modeling approach using a gradient boosting model to predict film revenue and leveraged feature importance to visualize actionable insights on which variables impact revenue using Seaborn.  Identified and corrected over 600 incorrect revenue values in TMDB  data and corrected using the open-source IMDbPy API.


- Notebooks are labeled with their 'version' number.  Initial attempt will be noted by "X.0" while the second attempt after identifying a mathmatical error that required a different approach are noted by "X.2".  

**To do:**

- [ ] Revisit data wrangling to extract more features from the original files

- [ ] Apply clustering model to new data set to create tiers for both revenue prediction

- [ ] Examine feature weights within the context of clustering analysis

File Organization:

- Code
  - 01 - Data Wrangling - Box Office Revenue
  - 01.5 - Learning to use IMDbPy & IMDB API
  - 02 - Exploratory Data Analysis - Box Office Revenue
  - 03 - Preprocessing and Training - Predicting Box Office Revenue
  - 04 - Preprocessing_optimizing_for_ouliers
  - 04.2 - Preprocessing_optimizing_for_ouliers - V2
  - 05 - Modeling & Reducing Dimensionality
  - 05.2 - Modeling & Reducing Dimensionality-V2.0
  - 06 - Modeling_revenue_tiers
  - 06.2 - Modeling_revenue_tiers
  - 07 - Modeling revenue on a film tier
  - README.md
  - Scratch notebook for capstone visualizations & statistics
- Data
  - BoxOfficeData.csv
  - No_Outliers.csv
  - No_Outliers2.csv
  - Reduced_dimensions.csv
  - Reduced_dimensions2.csv
  - boxoffice_EDA.csv
  - boxoffice_PreProcess.csv
  - boxoffice_cleaned.csv
  - boxoffice_data.csv
  - boxoffice_titles.csv
  - train.csv
- Documents
  - Project\ Proposal.pdf
  - Project\ Report.pdf
  - Project\ Slide\ Deck.pdf
  - README.md
- README.md


