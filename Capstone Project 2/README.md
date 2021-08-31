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



## Approach:

### Models used:
 
- The high dimensionality of the data set meant that linear modelling would not be a strong fit for modelling revenue, this was borne out by **excessive** error
- I then attempted to use multiple different models: K-nearest neighbor, SVM, and Random Forest models; of those Random Forest performed the best.
- Finally I iterated on the various models that rely on decision trees and ultimately chose to use the Gradient Boosting algorithm as the most resilient to the       high number of dimensions.
    
### Modelling Strategy:

- While the Gradient Boosting model did provide the best accuracy, I was still only able to predict film revenue to within 80% mean absolute percent error.
- The ultimate goal of this project was not to predict revenue with pinpoint accuracy (predicting cumulative gross revenue rather than box office
      revenue), but rather to predict revenue with acceptable accuracy and then study which features have the largest impact on revenue. 
- Thusly, the next step was to create several 'tiers' of films which could be modelled independently and provide more detailed information specific to the immutable qualities of films.  What impacts the revenue for an action film will not be the same as what impacts revenue for a family animated film.
- Using the 'kitchen sink' gradient boosting model I was able to hypothesize tiers based on the feature weights which explained the most variance and were qualities of a film which a production studio has almost no influence over (EG: a film's genre, turning an action script into a family drama isn't easy)
      
## Results:
    
- Notably, predicting revenue is significantly easier depending on which season of the year a film is released in: 
    
![image of seasonal accuracy](https://github.com/NickD-Dean/Springboard/main/Capstone%20Project%202/Documents/Seasonal%20error.png)

- Some of the most important features of a film which impact revenue a product studio *does* have influence over: 
    
![image of feature importance](https://github.com/NickD-Dean/Springboard/main/Capstone%20Project%202/Documents/Feature%20Importance.png)
    
- It is interesting to note that while the contributions of a top tier production company are the single biggest important feature in three out of four seasons; when it comes to films released during the holidays (here designated as November and December) budget is the most important factor.
      
- Additionally, the film's plot overview and tagline length are features which are intended to be standins for marketing data.  These two features are consistently in the top ten most important features in addition to other post-production qualities like runtime. 
      
- Based on the above, I was able to model revenue based on production company and genre to within 30% accuracy, and provide insights as to what features in a film can be altered to maximize worldwide revenue.
