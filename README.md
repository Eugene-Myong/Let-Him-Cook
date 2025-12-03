# Let! Him! Cook!
## By Eugene Myong

## Introduction
Provide an introduction to your dataset, and clearly state the one question your project is centered around. Why should readers of your website care about the dataset and your question specifically? Report the number of rows in the dataset, the names of the columns that are relevant to your question, and descriptions of those relevant columns.

Ah yes, food. You either love it or you starve to death (not recommended). But making food worth loving, now that's something else entirely. Thankfully, we as intuitive humans have (almost) perfected the ways of cooking, and we log our findings and methods in things called "recipes". These are finely detailed steps and instructions to recreate almost any food imaginable, from the simplest of pizzas to the most complex of crab rangoons.

This dataset Recipes and Ratings contains a bunch of recipes as well as ratings for most of them. In this project, we'll go through it and analyze a whole bunch of things about it. But we can't just go in willy nilly, we need a task, a focus. And for this project, the big question we are trying to answer is:

What kind of recipes have different numbers of steps?

Why steps you may ask? Well because when you're following along a recipe, what do you look at to estimate how much time it will take? Besides the estimated time it will take I mean. The number of steps. How the steps are written and what gets done in one step versus what takes many can really how what kind of person the author is, and can help you assess whether or not you should follow their recipe. The steps are like a hidden indicator of trustworthiness, or crediblity. And so I believe that analyzing them may lead to some interesting results.

As for some less interesting results, here are some facts about our data:

- Number of Rows: 83,782
- Number of Important Columns: 
- The Important Columns:
  - name: The name of the recipe.
  - Minutes: The number of minutes the recipe is said to take.
  - n_steps: The number of steps the recipe has.
  - n_ingredients: The number of ingredients the recipe uses.
  - avg_rating: The average rating of the recipe.
  - weekday; The day of the week the recipe was submitted.


<iframe
  src="assets/avg-rating-hist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


|     id |   minutes |
|-------:|----------:|
| 333281 |        40 |
| 453467 |        45 |
| 306168 |        40 |
| 286009 |       120 |
| 475785 |        90 |


## Data Cleaning and Exploratory Data Analysis
Describe, in detail, the data cleaning steps you took and how they affected your analyses. The steps should be explained in reference to the data generating process. Show the head of your cleaned DataFrame (see Part 2: Report for instructions).

Embed at least one plotly plot you created in your notebook that displays the distribution of a single column (see Part 2: Report for instructions). Include a 1-2 sentence explanation about your plot, making sure to describe and interpret any trends present. (Your notebook will likely have more visualizations than your website, and that's fine. Feel free to embed more than one univariate visualization in your website if you'd like, but make sure that each embedded plot is accompanied by a description.)

Embed at least one plotly plot that displays the relationship between two columns. Include a 1-2 sentence explanation about your plot, making sure to describe and interpret any trends present. (Your notebook will likely have more visualizations than your website, and that's fine. Feel free to embed more than one bivariate visualization in your website if you'd like, but make sure that each embedded plot is accompanied by a description.)

Embed at least one grouped table or pivot table in your website and explain its significance.
## Assessment of Missingness
State whether you believe there is a column in your dataset that is NMAR. Explain your reasoning and any additional data you might want to obtain that could explain the missingness (thereby making it MAR). Make sure to explicitly use the term "NMAR."

Present and interpret the results of your missingness permutation tests with respect to your data and question. Embed a plotly plot related to your missingness exploration; ideas include:
• The distribution of column Y
 when column X
 is missing and the distribution of column Y
 when column Y
 is not missing, as was done in Lecture 8.
• The empirical distribution of the test statistic used in one of your permutation tests, along with the observed statistic.
## Hypothesis Testing
Clearly state your null and alternative hypotheses, your choice of test statistic and significance level, the resulting 
-value, and your conclusion. Justify why these choices are good choices for answering the question you are trying to answer.

Optional: Embed a visualization related to your hypothesis test in your website.

Tip: When making writing your conclusions to the statistical tests in this project, never use language that implies an absolute conclusion; since we are performing statistical tests and not randomized controlled trials, we cannot prove that either hypothesis is 100% true or false.
## Framing a Prediction Problem
Clearly state your prediction problem and type (classification or regression). If you are building a classifier, make sure to state whether you are performing binary classification or multiclass classification. Report the response variable (i.e. the variable you are predicting) and why you chose it, the metric you are using to evaluate your model and why you chose it over other suitable metrics (e.g. accuracy vs. F1-score).

Note: Make sure to justify what information you would know at the "time of prediction" and to only train your model using those features. For instance, if we wanted to predict your final exam grade, we couldn't use your Final Project grade, because the project is only due after the final exam! Feel free to ask questions if you're not sure.
## Baseline Model
Describe your model and state the features in your model, including how many are quantitative, ordinal, and nominal, and how you performed any necessary encodings. Report the performance of your model and whether or not you believe your current model is "good" and why.

Tip: Make sure to hit all of the points above: many projects in the past have lost points for not doing so
## Final Model
State the features you added and why they are good for the data and prediction task. Note that you can't simply state "these features improved my accuracy", since you'd need to choose these features and fit a model before noticing that – instead, talk about why you believe these features improved your model's performance from the perspective of the data generating process.

Describe the modeling algorithm you chose, the hyperparameters that ended up performing the best, and the method you used to select hyperparameters and your overall model. Describe how your Final Model's performance is an improvement over your Baseline Model's performance.

Optional: Include a visualization that describes your model's performance, e.g. a confusion matrix, if applicable.
## Fairness Analysis
Clearly state your choice of Group X and Group Y, your evaluation metric, your null and alternative hypotheses, your choice of test statistic and significance level, the resulting 
-value, and your conclusion.

Optional: Embed a visualization related to your permutation test in your website.