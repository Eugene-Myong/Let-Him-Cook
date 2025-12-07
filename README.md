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
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', '...] | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]    |        10 | ['heat the oven to 350f and arrange the ... | these are the most; chocolatey, moist, r...] | ['bittersweet chocolate', 'unsalted butt...] |               9 |            4 |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', '...] | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 2...] |        12 | ['pre-heat oven the 350 degrees f', 'in ... | this is the recipe that we use at my sch...] | ['white sugar', 'brown sugar', 'salt', '...] |              11 |            5 |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', '...] | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0...] |         6 | ['preheat oven to 350 degrees', 'spray a...] | since there are already 411 recipes for ... | ['frozen broccoli cuts', 'cream of chick...] |               9 |            5 |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12  | ['time-to-make', 'course', 'cuisine', 'p...] | [878.3, 63.0, 326.0, 13.0, 20.0, 123.0, ...] |         7 | ['freheat the oven to 300 degrees', 'gre...] | why a millionaire pound cake?  because i... | ['butter', 'sugar', 'eggs', 'all-purpose...] |               7 |            5 |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06  | ['time-to-make', 'course', 'main-ingredi...] | [267.0, 30.0, 12.0, 12.0, 29.0, 48.0, 2....] |        17 | ['pan fry bacon , and set aside on a pap...] | ready, set, cook! special edition contes... | ['meatloaf mixture', 'unsmoked bacon', '...] |              13 |            5 |

I wonder if making that millionaire pound cake will make me a millionaire...

You might be wondering, since we're looking at the number of steps, what does their distribution look like? Well, I'm happy to help:

<iframe
  src="assets/num-steps-hist.html"
  width="800"
  height="425"
  frameborder="0"
></iframe>
Having a look above, we note that many recipes have between five to nine steps. According to the graph, there does not appear to be any recipe with more than fifty steps, but believe it or not, the largest amount of steps is actually one-hundred! I bet that would take at least a couple of days.

But how does the number of steps look when considering the average rating? 

<iframe
  src="assets/num-steps-avg-rating-scatter.html"
  width="800"
  height="425"
  frameborder="0"
></iframe>
It looks like there is no strong trends or patterns between the number of steps and the average rating of a recipe. That big blob of blue in the top left is mainly due to the fact that most recipes are rated quite high and have less than about thirtyish steps. It also appears that recipes with more steps don't really impact the rating.

|        |       1 |       2 |       3 |       4 |       5 |       6 |       7 |       8 |       9 |      10 |      11 |      12 |      13 |      14 |        15 |      16 |      17 |        18 |        19 |        20 |        21 |      22 |   23 |    24 |   25 |   26 |   27 |   28 |   29 |   30 |   31 |   32 |   33 |   37 |  
|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|----------:|--------:|--------:|----------:|----------:|----------:|----------:|--------:|-----:|------:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|
|       1 | 4.66667 | 4.66299 | 4.7662  | 4.69459 | 4.66742 | 4.64639 | 4.55043 | 4.55658 | 4.56284 | 4.59369 | 4.58182 | 4.59259 | 4.5     | 4.68333 | nan       | 4.6     | 4.88889 | nan       | nan       | nan       | nan       | nan     |  nan | nan   |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |
|       2 | 4.80769 | 4.70988 | 4.67926 | 4.68089 | 4.65886 | 4.65024 | 4.71086 | 4.6784  | 4.58513 | 4.67214 | 4.68298 | 4.59547 | 4.85254 | 4.61364 |   4.58333 | 4.75    | 5       | nan       | nan       |   3.83333 | nan       | nan     |  nan | nan   |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |
|       3 | 4.72917 | 4.7295  | 4.63575 | 4.65626 | 4.66707 | 4.64634 | 4.65272 | 4.63952 | 4.62818 | 4.68428 | 4.6469  | 4.68756 | 4.63538 | 4.34722 |   4.75917 | 4.71314 | 4.8125  |   4.55556 |   5       |   4.46429 |   5       |   4.75  |  nan | nan   |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |
|       4 | 4.2881  | 4.63085 | 4.67689 | 4.63323 | 4.67487 | 4.66312 | 4.602   | 4.61868 | 4.63661 | 4.55808 | 4.61079 | 4.63675 | 4.69631 | 4.66539 |   4.66688 | 4.44592 | 4.75    |   4.75564 |   4.75    |   4.33333 |   4.9375  |   5     |  nan |   5   |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |
|       5 | 4.72692 | 4.58755 | 4.64606 | 4.65844 | 4.64185 | 4.61625 | 4.60035 | 4.60316 | 4.54143 | 4.57859 | 4.61475 | 4.60254 | 4.59136 | 4.52691 |   4.55336 | 4.67482 | 4.80797 |   4.77407 |   4.78571 |   4.91667 |   4.41667 |   4.925 |    5 |   4.5 |  nan |    5 |  nan |    5 |  nan |  nan |  nan |  nan |  nan |  nan |

And heres a table showing the number of steps (on the left) and the number of ingredients (on the top) and their average rating (in the cells). Notice how the more ingredients and steps you have, the more common missing values are.

## Assessment of Missingness

NMAR: Not Missing At Random. This term describes a missing value in which the reason for its missingness depends on the value itself. And after my hours of reasearch and acute calculations, I have reason to believe that this recipes dataset does in fact have a column that is NMAR! And it's none other than the Average Rating column.

First of all, the Average Rating column can only exist if it has at least one rating. Thus, if a recipe never recieved any ratings, than obviously it can't have an average of those nonexistent ratings! 

But when would this happen? Perhaps for new recipes that have just been uploaded or rare recipes that not many people are looking for, they may not recieve many views, and thus it's reasonable to think that they recieve even less ratings (or in this case, none at all). This could also happen with poorly written recipes. If you're looking for a pizza recipe and you find one that only has one step: "Buy one", then you would probably keep looking. Since that recipe was never technically used, it won't recieve any ratings. 

As such, additional data such as the number of steps/ingredients and the steps/ingredients themselves may clue us in as to why exactly a recipe has no ratings. If we could find a reason in other data as to why a recipe doesn't have a rating/average rating, then that would make the Average Rating column Missing At Random (MAR), which means the missing values depend on another column.

But is this the case for this data? Well...

As it turns out, it is! I ran a permutation test to find out whether the number of steps is involved in the missingness of average rating.

<iframe
  src="assets/nmar-test.html"
  width="800"
  height="425"
  frameborder="0"
></iframe>
The blue bars indicate the null distribution of the test stat while assuming that the missing Average Rating values are Missing Completely At Random (MCAR). In other words, these bars represent what we would expect to happen if the missing Average Rating values really didn't have anything to do with the number of steps, the kind of results we would see "normally" if you will.  
The red bar far on the right indicates what actually happened, the observed value in our dataset. If it were among the blue lines we would say that the number of steps has no relationship with the missingness of Average Rating, but it's way over there (not with the blue bars). 

What this means is that since the actual result is nowhere near what we expected to happen (where we assumed that there was no relationship between the number of steps and missingness of Average Rating), it appears that there is, in fact, a very real relationship between the number of steps and the missingess of Average Rating.  

In fact, as it turns out, the mean number of steps for recipes with average ratings is about 9.87, whereas the mean number of steps for recipes missing an average rating is 11.23. 

<iframe
  src="assets/nmar-test-diffs.html"
  width="800"
  height="425"
  frameborder="0"
></iframe>
You can see the difference above, the "True" group tends to have slightly more steps than the "False" group.

Give or take one step may not seem like a lot, but it does provide us with a potential explanation: more "complex" recipes are more likely to be missing ratings. Maybe some people see the higher number of steps and get intimidated? I don't blame them honestly, if I open a recipe for some spaghetti and see more lines than I was expecting than already I'm thinking "Man is there something easier I can make?"

## Hypothesis Testing

Now that we've tied up some loose ends, it's time to start the real digging. 

As a reminder, our big question was: What types of recipes tend to have different numbers of steps?

We'll take a shot at answering this by analyzing the number of ingredients in a recipe to try to find out recipes with different numbers of ingredients have different numbers of steps. We'll do so using a permutation test with:
- Null Hypothesis: Recipes with more ingredients have the same mean number of steps as recipes with fewer ingredients.
- Alternative Hypothesis: Recipes with more ingredients have a different mean number of steps than recipes with fewer ingredients.

Where we differentiate less and more by using the median: recipes with less than or equal to the median are said to have less or fewer ingredients, and recipes with more than the median are said to have more ingredients.

We will use a test statistic of difference in group means, and a significance level of 0.05.

And here are those results:

<iframe
  src="assets/hyp-test.html"
  width="800"
  height="425"
  frameborder="0"
></iframe>
Note that, once again, the red bar is very far to the right and nowhere near the blue bars. This means that, with a p-value of effectively 0.0, we reject the null hypothesis and conclude that recipes with more ingredients tend to have different numbers of steps than those with fewer ingredients.

As for the exact differences, recipes with more ingredients have on average 12.41 steps, and recipes with less ingredients have on average 8.05 steps. Here's that visualized:

<iframe
  src="assets/hyp-test-diffs.html"
  width="800"
  height="425"
  frameborder="0"
></iframe>
This is kind of what you would think right? The more ingredients a recipe has, the more steps you would think it needs to use all of those ingredients (provided the ingredients acutally serve a purpose and aern't just thrown in to make it look more complicated). While this test does not really prove anything, the statistical evidence is strong enough to support the idea that the number of ingredients is associated with the number of steps.

## Framing a Prediction Problem

We've discovered what affects the number of steps in a recipe as well as what the number of steps in a recipe affects. So what if we wanted to do some predicting (for the number of steps in a recipe, if that wasn't obvious already)?

We now define a prediction problem: predicting the number of steps in a recipe. This is a regression problem, with response variable: the number of steps (Wow). The metric that we'll use to evaluate our model is the Root Mean Squared Error (RMSE), which is like the Mean Squared Error (MSE) but we'll be able to evaluate our models performance in actual steps, makes it much easier to define a good versus a bad performance. RMSE also penalizes larger mistakes more heavily than metrics like Mean Absolute Error (MAE). This is good because severely mispredicting a recipe’s complexity (like predicting 5 steps when there are actually 30) is a more meaningful error than being slightly off, and should be treated as such.

At the time of prediction, we would know basically everything except one teeny tiny feature: Average Rating. This is because ratings come from the future, only after the recipe is published, wheras the number of steps is defined well before any ratings are made. As such, it makes no sense to use a recipes average rating to predict its number of steps.

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