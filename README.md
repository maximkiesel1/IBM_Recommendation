# Recommendation Engine For Blog Articles
![sam-pak-nwlFMVePZhI-unsplash](https://user-images.githubusercontent.com/119667336/230715935-03d94081-b069-44db-86fe-d5439d657bca.jpg)
# Project Motivation 

In this project, I will create a recommendation engine for users of the IBM Watson Studio blog article platform. This engine will provide new articles for the user, no matter if the user is new or have already interacted with the platform. 

Therefore, I will use the following algorithms: 

- Ranked-Based 

- User-Based 

- Matrix Factorization (FunkSVD) 

# File Descriptions 

- Jupyter Notebook: `Recommendation Engine for IBM Watson Studio Blog Articles.ipynb`

  - This Jupyter Notebook includes the following content: 
    1. Exploratory Data Analysis 
    2. Ranked-Based Recommendation 
    3. User-Based Recommendation 
    4. Matrix Factorization Recommendation 
    5. Final Model 
  - Used Libraries:  
    - `import numpy as np`
    - `import pandas as pd`
    - `import matplotlib.pyplot as plt`
    - `import statistics`
    - `from collections import Counter` 

- CSV-file: `articles_community.csv`

  - File with all blog articles from the platform 
  - 5 columns (datatypes: 1 integers, 4 objects) 
  - 1056 rows 
  - Hardly any duplicates/NaN-Values 
- CSV-file: `user-item-interactions.csv`
  - File with all user-article interactions 
  - 3 columns (datatypes: 1 float, 2 objects) 
  - 45993 rows 

# Exploratory Data Analysis 

In the file `user-item-interactions.csv`, there are the following findings: 

- 80% of articles were viewed 80 times:
<img width="1012" alt="Bildschirmfoto 2023-04-08 um 12 07 57" src="https://user-images.githubusercontent.com/119667336/230715632-4fbee6e2-dbd8-4ffb-be9d-8972420842fe.png">

- Most users interacted with 1 to 20 articles: 
<img width="1011" alt="Bildschirmfoto 2023-04-08 um 12 07 34" src="https://user-images.githubusercontent.com/119667336/230715623-1b2f0d98-5979-4bb8-b503-59387701606b.png">

- Most users viewed 1 to 7 different articles (not including multi viewing):
<img width="1021" alt="Bildschirmfoto 2023-04-08 um 11 58 36" src="https://user-images.githubusercontent.com/119667336/230715269-0379bf6f-93f9-420d-bbe6-5952b5d2a8fd.png">


# Ranked-Based Recommendation 
The algorithm uses a ranking to find the most viewed items and sorts them from most viewed to least viewed.

# User-Based Recommendation 

The algorithm search for user with similar behavior. To find similar behavior, I look at the articles a user has viewed and compare them to all users to find the user with the most matches. The items that the first user didn't see, but the similar user did, will be recommended. 


# Matrix Factorization Recommendation 

he next recommendation algorithm will be based on the Matrix Factorization. Therefore, I use the famous FUNK-SVD algorithm. 

The FUNK-SVD based on the splitting of a matrix in three matrices with latent factors. The problem with the normal SVD is that it can´t work with nan values, so objects which a user didn´t see jet. So, solve this problem, the FUNK-SVD use just the existing rating of a user and updated the nan and all other values of the latent factors with it. This will be done so long until a minimum error is reached. 

The smallest MSE in at the number of 3 latent factors. 

 <img width="1057" alt="Bildschirmfoto 2023-04-08 um 11 58 11" src="https://user-images.githubusercontent.com/119667336/230715249-9bc53f41-cce8-4ae1-9925-179573ffbb6b.png">

The define the cut point is at `± 0.000356` (the MSE at the lowest point). 

# Summery 

The Ranked-Based Recommendation just recommend the most popular articles. For completely new users (cold-start-problem) this is complete enough. But for older user this is not satisficing. Therefore, the User-Based Recommendation can be used. The problem here is that a minimum number of articles seen is necessary. If this value is by 3, then just 50% of the users can have a recommendation with this algorithm. The last recommendation function can solve the problem. With the FUNK-SVD there is the possibility to predict article for a user. Just on interaction with an article can be enough. But the accuracy depends on the number of previews user interactions. Therefore, a cutoff value is necessary to find just the articles with the best accuracy. Overall, a combination of all 3 algorithm is the best option to find the best recommendation.  

An improvement for my final model can be to restart the searching in the User-Based-Recommendation, when articles are sorted out because they have already been seen.  

# Acknowledgements 

The dataset for this analyzation was thankfully provided from IBM Watson Studio: `https://www.ibm.com/blogs/watson/` 
