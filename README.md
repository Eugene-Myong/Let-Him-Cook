# Let! Him! Cook!
## By Eugene Myong

## Introduction

Ah yes, food. You either love it or you starve to death (not recommended). But making food worth loving, now that's something else entirely. Thankfully, we as intuitive humans have (almost) perfected the ways of cooking, and we log our findings and methods in things called "recipes". These are finely detailed steps and instructions to recreate almost any food imaginable, from the simplest of pizzas to the most complex of crab rangoons.

This dataset Recipes and Ratings contains a bunch of recipes as well as ratings for most of them. In this project, we'll go through it and analyze a whole bunch of things about it. But we can't just go in willy nilly, we need a task, a focus. And for this project, the big question we are trying to answer is:

What kind of recipes have different numbers of steps?

Why steps you may ask? Well because when you're following along a recipe, what do you look at to estimate how much time it will take? Besides the estimated time it will take I mean. The number of steps. How the steps are written and what gets done in one step versus what takes many can really how what kind of person the author is, and can help you assess whether or not you should follow their recipe. The steps are like a hidden indicator of trustworthiness, or crediblity. And so I believe that analyzing them may lead to some interesting results.

Here are some important facts about our data:

- Number of Rows: 83,782
- Number of Important Columns: 6
- The Important Columns:
  - name: The name of the recipe.
  - Minutes: The number of minutes the recipe is said to take.
  - n_steps: The number of steps the recipe has.
  - n_ingredients: The number of ingredients the recipe uses.
  - avg_rating: The average rating of the recipe.
  - weekday; The day of the week the recipe was submitted.


## Data Cleaning and Exploratory Data Analysis

First things first, we need to make the data useable. This means that we take the two data sets we have and make them one, by taking all the ratings from the rating dataset and creating an average rating column, which we add to the recipes dataset, which is what we'll use from now on. 

Some columns like tags, steps, and ingredients are strigified lists, so we apply a custom function that turns them into regular lists of strings. We ensure that n_steps and the length of the steps list is the same for all recipes, and do the same for ingredients.

We then proceed by normalizing (lowercasing and removing excessive whitespaces/punctuation/characters) the names, description, and ingredients columns. We also change the submitted column to datetime objects, which will make it so much easier to work with, as well as creating columns for the year, month, and weekday.

A column called nutrition actully contains many nutritious facts, so we split that column into seven different ones, one for each fact. Another column called tags must also be stripped of any weird characters/spaces, and duplicate tags are removed for every recipe.

And with that, the data looks much better. Have a look for yourself:

| name                                 |     id |   minutes |   contributor_id | submitted   | tags                                        | nutrition                                   |   n_steps | steps                                       | description                                 | ingredients                                 |   n_ingredients |   avg_rating |
|:-------------------------------------|-------:|----------:|-----------------:|:------------|:--------------------------------------------|:--------------------------------------------|----------:|:--------------------------------------------|:--------------------------------------------|:--------------------------------------------|----------------:|-------------:|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', '... | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]    |        10 | ['heat the oven to 350f and arrange the ... | these are the most; chocolatey, moist, r... | ['bittersweet chocolate', 'unsalted butt... |               9 |            4 |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', '... | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 2... |        12 | ['pre-heat oven the 350 degrees f', 'in ... | this is the recipe that we use at my sch... | ['white sugar', 'brown sugar', 'salt', '... |              11 |            5 |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', '... | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0... |         6 | ['preheat oven to 350 degrees', 'spray a... | since there are already 411 recipes for ... | ['frozen broccoli cuts', 'cream of chick... |               9 |            5 |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12  | ['time-to-make', 'course', 'cuisine', 'p... | [878.3, 63.0, 326.0, 13.0, 20.0, 123.0, ... |         7 | ['freheat the oven to 300 degrees', 'gre... | why a millionaire pound cake?  because i... | ['butter', 'sugar', 'eggs', 'all-purpose... |               7 |            5 |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06  | ['time-to-make', 'course', 'main-ingredi... | [267.0, 30.0, 12.0, 12.0, 29.0, 48.0, 2.... |        17 | ['pan fry bacon , and set aside on a pap... | ready, set, cook! special edition contes... | ['meatloaf mixture', 'unsmoked bacon', '... |              13 |            5 |
C:\Users\eugen\AppData\Local\Temp\ipykernel_23088\2374596336.py:10: FutureWarning:

DataFrame.applymap has been deprecated. Use DataFrame.map instead.

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