# game-sales-FIDS

This project presents an analysis of video game sales, using a dataset of games sold after the year 2000. We (Bryan Santos and Tim Lee) attempt to conduct a regression analysis to unlock actionable business insights.

In this repository are two notebooks: 

* **tech_presentation_notebook** - This notebook serves as a walkthrough through our initial data load and exploration, hypothesis testing, and feature engineering. 
* **regression_models** - This notebook contains our regression anaysis, including the training process for 19 models using various combinations of features, regression techniques, and polynomial complexity.

Our presentation deck is located here: https://docs.google.com/presentation/d/1I1X66QhRbQfrPFrWEN2oMRlhWjOwGluZ-PZPwMvtNwo/edit?usp=sharing

## EDA and Visualizations
Our EDA and visualizations can be viewed in detail in the tech_presentation_notebook.

## Feature Engineering
We added additional data and engineered several features, mostly related to the games' platforms/consoles:

* A percentage of where in the console's lifespan a game was released (to identify launch titles)
* A flag to indicate whether a game was released on an obsolete console (such as a PS2 game released after the PS3 launch)
* A flag to indicate games that were re-released on a future generation of a console
* Aggregations of Metacritic user and critic scores to serve as proxies for a game's publisher, developer, and genre

## Models
We generated 19 models, experimenting with various the inclusion of features, feature engineering, ridge regression, elastic regularization, gradient boosting, and polynomial complexity. We concluded that our 17th model was the best, with all features (and engineered features), and a third-order polynomial regression. Increasing the polynomial order or adding elastic regularization both risked overfitting the training data, as the spread between training and test R2 began to diverge.

Model 17: RMSE: 0.931, R2 (train): 0.434, R2 (test): 0.414
![models](https://github.com/JohnTheTripper/game-sales-FIDS/blob/master/readme_images/models.png)

## Key Features
We identified three key features with an effect on our model.
* **Console units sold**. This information was added as reference data to account for this simple axiom: people won't buy games for consoles they don't own. The PS2 and Dreamcast were competitors, but the PS2 outsold the Dreamcast 16:1. PS2 games would logically sell more units than Dreamcast games. Though this is a rather self-explanatory feature, we didn't achieve satisfactory models until adding this feature.
* **Current generation flag** This engineered feature indicates when a game was released for an obsolete console, a console whose successor has launched. A two-sample t-test suggested that these games have lower sales.
* **Metacritic score** This is a representation of a game's critical reception. Better-quality games have higher sales. It's worth noting that we observed a *negative* correlation between Metacritic's user scores and a game's sales. It may be because popular games attract lots of negative attention online, and dissatisfied users will take to the web to complain.

![PS2 and Wii dominance](https://github.com/JohnTheTripper/game-sales-FIDS/blob/master/readme_images/platform_sales.png)

## Conclusions and Use-Case Recomendations
We identified three business-case recommendations as guidance when planning development of games.
* **Make critically-accepted games, but ignore complaining from the masses** Game quality and reception DOES matter, but only from the critics. Professional critics and journalists are qualified at evaluating games, and their clout does matter in shaping public perception of games. However, finding a negative correlation between user scores and game sales was surprising, and indicates it may not be best to try and pander to the loudest or the most vocally dissatisfied customers.
* **Do not make games for obsolete consoles** We observed a drop in sales in games that were released on obsolete consoles. Games have moved onto the next generation, and resources are better spent capturing customers on the latest console.
* **Don't bother re-releasing games on successor consoles** Conversely, if a game is released on a console near the end of its lifespan, it may not be worth it to spend development time and effort porting the game to the successor console. We saw higher sales of games on the predecessor console. Perhaps gamers interested in the game would have bought it at their first opportunity, when available on the predecessor console. We admit that there is one scenario where this suggestion loses validity: if fans are actually purchasing the game twice. However, to negate this suggestion, the increased sales from gamers purchasing the game twice would have to offset the development resources spent on porting the game to the new console. 

![critical and user reception correlation with sales](https://github.com/JohnTheTripper/game-sales-FIDS/blob/master/readme_images/weights.png)

![obsolete consoles](https://github.com/JohnTheTripper/game-sales-FIDS/blob/master/readme_images/console.png)

![re-released games](https://github.com/JohnTheTripper/game-sales-FIDS/blob/master/readme_images/rerelease.png)
