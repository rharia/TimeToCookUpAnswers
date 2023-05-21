# TimeToCookUpAnswers

## Introduction
The recipes and ratings dataset contains recipes and their reviews and ratings posted since 2008 from the food.com website. My analysis will be centered around the question: what is the relationship between the cooking time and the average rating of recipes? Shorter cooking times may result in easier and quicker recipes, but that does not guarantee a high rating. On the other hand, longer cooking times may require more effort, which may result in better-tasting recipes. Readers of the website can benefit from this analysis as it can help them discern which recipes will be easier to make and which ones will be more time-consuming. It can also help them determine the ideal level of effort and time that each recipe requires to achieve the desired rating. 
I have chosen to work with the recipe and ratings dataset which contains information about different recipes and their reviews posted since 2008 on the website food.com. This dataset has 83,782 rows. The names of the columns that are relevant to my question are the minutes, name, and the average_rating columns. The minutes column provides the number of minutes it takes to prepare each recipe. The name column provides the recipe name and the average_rating column provides the average rating for each recipe.

## Cleaning And EDA
### Cleaning
First, I merged the recipe and the ratings datasets together into one dataframe. Then I calculated the average rating for each recipe using the groupby function and then I merged the data into the dataframe. In order to clean up the data I filled all the ratings of 0 with np.nan because having a rating of 0 means that the recipe has not yet been rated. In order to get an accurate average rating for each recipe, it is important to change the 0 values to null so that it does not affect the average rating of the recipe. Additionally, I cleaned up the nutrition colun by creating separate columns for all the values in the list. I added columns for calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates from the nutrition column. After separating the values from the nutrition column, I removed the nutrition column from the dataframe. Furthermore, for all the columns that contain a string list (tags, steps, and ingredients), I converted the type of the column to a list. I also got rid of the reviews column as it was needed for the rest of the assignment. 

This is the first few rows of the cleaned recipes dataframe: 

|    | name                                 |     id |   minutes |   contributor_id | submitted   | tags                                                                                                                                                                                                                                                                                               |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                                                                             |   n_ingredients |   average_rating |   calories (#) |   total fat (PDV) |   sugar (PDV) |   sodium (PDV) |   protein (PDV) |   saturated fats (PDV) |   carbohydrates (PDV) |
|---:|:-------------------------------------|-------:|----------:|-----------------:|:------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-----------------:|---------------:|------------------:|--------------:|---------------:|----------------:|-----------------------:|----------------------:|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']                                                                        |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat ', 'stirring frequently ', 'until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs ', 'sugar ', 'cocoa powder ', 'vanilla extract ', 'espresso ', 'and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean ', 'about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']                                                          |               9 |                4 |          138.4 |                10 |            50 |              3 |               3 |                     19 |                     6 |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                                                                                                      |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl ', 'sift together the flours and baking powder', 'set aside', 'in another mixing bowl ', 'blend together the sugars ', 'margarine ', 'and salt until light and fluffy', 'add the eggs ', 'water ', 'and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop ', 'scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                                                                             |              11 |                5 |          595.1 |                46 |           211 |             22 |              13 |                     51 |                    26 |
|  2 | 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                                                                                               |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray ', 'set aside', 'in a large bowl mix together broccoli ', 'soup ', 'one cup of cheese ', 'garlic powder ', 'pepper ', 'salt ', 'milk ', '1 cup of french onions ', 'and soy sauce', 'pour into baking dish ', 'sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly ', 'about 10 more minutes']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']                                                                   |               9 |                5 |          194.8 |                20 |             6 |             32 |              22 |                     36 |                     3 |
|  3 | millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12  | ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less'] |         7 | ['freheat the oven to 300 degrees', 'grease a 10-inch tube pan with butter ', 'dust the bottom and sides with flour ', 'and set aside', 'in a large mixing bowl ', 'cream the butter and sugar with an electric mixer and add the eggs one at a time ', 'beating after each addition', 'alternately add the flour and milk ', 'stirring till the batter is smooth', 'add the two extracts and stir till well blended', 'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean ', 'about 1 1 / 2 hours', 'cool the cake in the pan on a rack for 5 minutes ', 'then turn it out on the rack to cool completely']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                                                                                                                |               7 |                5 |          878.3 |                63 |           326 |             13 |              20 |                    123 |                    39 |
|  4 | 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06  | ['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']                                                                                                                                             |        17 | ['pan fry bacon ', 'and set aside on a paper towel to absorb excess grease', 'mince yellow onion ', 'red bell pepper ', 'and add to your mixing bowl', 'chop garlic and set aside', 'put 1tbsp olive oil into a saut pan ', 'along with chopped garlic ', 'teaspoons white pepper and a pinch of kosher salt', 'bring to a medium heat to sweat your garlic', 'preheat oven to 350f', 'coarsely chop your baby spinach add to your heated pan ', 'stir frequently for approximately 5 min to wilt', 'add your spinach to the mixing bowl', 'chop your now cooled bacon ', 'and add it to the mixing bowl', 'add your meatloaf mix to the bowl ', 'with one egg and mix till thoroughly combined', 'add your goat cheese ', 'one egg ', '1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', 'transfer to a 9x5 meatloaf pan ', 'and cook for 60 min or until the internal temperature is at least 160f', 'let stand for 5min', 'melt 1tbsp unsalted butter into a frying pan ', 'and cook up to three eggs at a time', 'crack each egg into a separate dish ', 'in order to prevent egg shells from reaching the pan ', 'then add salt and pepper to taste', 'wait until the egg whites are firm looking ', 'but slightly runny on top before flipping your eggs', 'after flipping ', 'wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf'] | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] |              13 |                5 |          267   |                30 |            12 |             12 |              29 |                     48 |                     2 |

### Univariate Analysis
Univariate Plot #1: Number of Ingredients For Each Recipe

This plot shows the distribution of the number of ingredients in dataframe. From the plot we can see that the median number of infredients in the data is about 10 steps. The plot is slighlty skewed to the left adn from the plot we can see that there is a high chance that the average number of steps is also around 10.

<iframe src="assets/univariate_plot.html" width=800 height=600 frameBorder=0></iframe>

Univariate Plot #2: Number of Steps For Each Recipe

This plot shows the emperical distributionof the number of steps in the recipes dataframe. From the plot we can see that the average number of steps in a recipe is aroumd 10 steps if we ignore the outliers. The data for this column seems to contain many outliers, since it shows a few of the recipes having over 60 steps, which could possibly be a mistake.

<iframe src="assets/univariate_plot2.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis
Bivariate Plot #1: Effect of Protein on Number of Calories in the Recipe
This plot takes a look at how the protein level in a recipe affects the number of calories the recipe contains. From the graph below we can see that there is a positive correlation between the sugar levels and the number of calories present in a recipe.

<iframe src="assets/bivariate_plot.html" width=800 height=600 frameBorder=0></iframe>


Bivariate Plot #2: Effect of Sugar on Number of Calories in the Recipe
This plot takes a look at how the sugar levels in a recipe affect the number of calories the recipe contains. From the graph below we can see that there is a positive correlation between the sugar levels and the number of calories present in a recipe.

<iframe src="assets/bivariate_plot2.html" width=800 height=600 frameBorder=0></iframe>

### Aggregation
Aggregation of the number of steps in a recipe and its rating.
This grouped table is significant because it shows that as the number of steps in a recipe increases, the rating of that recipe also increases. This table is significant because it shows that as the average rating of a recipe increases the number of steps in he recipe does not really vary. We can see thnumber of steps in a recipe does not have much of an effect on the rating that recipe recieves.

|   average_rating |   count |     mean |   median |
|-----------------:|--------:|---------:|---------:|
|          1       |     261 |  9.5249  |      8   |
|          1.5     |      20 |  8.6     |      8.5 |
|          2       |     260 | 10.6423  |      9   |
|          2.16667 |       6 | 12.5     |     13.5 |
|          2.25    |       5 |  5.6     |      5   |
|          2.28571 |       7 | 12.1429  |      9   |
|          2.33333 |      28 | 11.5714  |      8.5 |
|          2.5     |     100 | 10.26    |      9   |
|          2.5625  |      20 | 12.55    |      9   |
|          2.6     |       5 |  9.2     |      7   |
|          2.66667 |      27 | 10       |      8   |
|          2.75    |      21 | 10.7619  |      9   |
|          2.83333 |       6 | 12.3333  |     11.5 |
|          3       |    1163 | 10.0361  |      9   |
|          3.09091 |      15 | 12.8     |     11   |
|          3.125   |       8 |  9.25    |      7.5 |
|          3.16667 |      15 | 10.5333  |      9   |
|          3.2     |      13 |  9       |      7   |
|          3.25    |      47 | 10.7872  |      8   |
|          3.28571 |      21 |  8.66667 |      7   |
|          3.3     |      10 | 13       |     13   |
|          3.33333 |     153 | 10.4379  |      9   |
|          3.38462 |      15 | 10.0667  |     10   |
|          3.4     |      41 |  8.12195 |      8   |
|          3.44444 |       9 |  7.44444 |      9   |
|          3.5     |     566 |  9.83922 |      9   |
|          3.55556 |      10 | 10.2     |     10.5 |
|          3.57143 |      22 |  9.27273 |      7   |
|          3.59091 |      24 | 11.0833  |     10.5 |
|          3.6     |      43 | 13.4651  |     11   |
|          3.66667 |     429 | 10.3287  |      9   |
|          3.69231 |      14 | 11.6429  |     11   |
|          3.70588 |      19 | 11       |     10   |
|          3.71429 |      50 | 10.54    |      9   |
|          3.75    |     123 |  9.47154 |      9   |
|          3.77778 |       9 |  8.44444 |      6   |
|          3.79012 |      90 |  8.38889 |      7   |
|          3.8     |      88 | 10.7273  |      8.5 |
|          3.83333 |      79 | 10       |      9   |
|          3.85714 |      79 |  8.58228 |      7   |
|          3.875   |      33 | 11.8182  |     12   |
|          3.88889 |       9 | 13.3333  |     13   |
|          3.90909 |      12 |  7.25    |      7   |
|          3.92308 |      15 |  9.86667 |      7   |
|          3.92857 |      14 | 12.5     |      9.5 |
|          3.94444 |      21 |  7.71429 |      6   |
|          3.95775 |      74 | 10.2838  |      8.5 |
|          4       |    6263 | 10.1905  |      9   |
|          4.06667 |      30 | 10.1     |      8   |
|          4.07692 |      26 | 10.2692  |      8   |
|          4.08333 |      38 |  9.05263 |      7.5 |
|          4.09091 |      23 | 10.5652  |     10   |
|          4.09677 |      36 | 11.4444  |     10   |
|          4.1     |      22 |  9.45455 |      9   |
|          4.11111 |      97 | 11.2784  |      9   |
|          4.11628 |      47 | 10.383   |     10   |
|          4.125   |      85 | 10.5059  |     10   |
|          4.13333 |      15 |  8.26667 |      6   |
|          4.14286 |      95 |  8.75789 |      8   |
|          4.16667 |     198 | 10.6212  |      9   |
|          4.18182 |      94 | 10.4043  |      9   |
|          4.2     |     467 |  9.70664 |      8   |
|          4.21429 |      57 | 10.2982  |      9   |
|          4.22222 |      89 |  9.93258 |      9   |
|          4.23333 |      37 |  9       |      8   |
|          4.25    |     669 | 10.0045  |      9   |
|          4.27273 |      26 | 10.8077  |     10.5 |
|          4.28571 |     213 |  9.70892 |      8   |
|          4.29167 |      29 | 10.1724  |      9   |
|          4.3     |      94 |  9.93617 |      8.5 |
|          4.30435 |      25 | 11.8     |     11   |
|          4.30769 |      88 | 10.5682  |      9   |
|          4.3125  |      36 |  9.47222 |      6   |
|          4.32    |      26 |  8.92308 |      8.5 |
|          4.32143 |      36 | 10.7778  |     10   |
|          4.33333 |    1710 | 10.0673  |      9   |
|          4.34615 |      27 | 12.1481  |     11   |
|          4.35714 |      15 | 12.1333  |     11   |
|          4.36364 |      61 | 11.5738  |     10   |
|          4.375   |     271 |  9.98524 |      9   |
|          4.37778 |      58 | 10.7069  |      9.5 |
|          4.38095 |      21 | 11       |     10   |
|          4.38462 |      71 |  9.02817 |      7   |
|          4.39286 |      32 |  9.25    |      8.5 |
|          4.4     |     596 |  9.82886 |      8   |
|          4.40625 |      89 |  9.73034 |      8   |
|          4.40741 |      27 | 10       |     10   |
|          4.41667 |      64 |  9.59375 |      8   |
|          4.42105 |      19 |  8.68421 |      9   |
|          4.42857 |     322 | 10.9534  |     10   |
|          4.4375  |      20 |  9.55    |      9.5 |
|          4.44444 |     257 |  9.52529 |      9   |
|          4.44828 |      36 |  9.97222 |      7   |
|          4.45455 |     188 | 10.266   |      9   |
|          4.46    |      56 | 12.25    |     10.5 |
|          4.46154 |      26 | 10.9231  |      9.5 |
|          4.46667 |      35 | 11.4286  |     10   |
|          4.47059 |      35 | 10.3714  |      9   |
|          4.47368 |      20 | 11.5     |     10.5 |
|          4.47826 |      33 |  9.54545 |      9   |
|          4.48    |      35 |  8.8     |      7   |
|          4.5     |    5008 | 10.0881  |      9   |
|          4.5122  |      46 |  8.04348 |      8   |
|          4.52941 |      39 |  9.97436 |      9   |
|          4.53125 |      37 |  7.05405 |      6   |
|          4.53333 |      93 |  9.65591 |      8   |
|          4.53846 |     108 |  9.97222 |      9   |
|          4.54545 |     140 |  9.45714 |      8   |
|          4.55    |      44 | 11.4091  |     10   |
|          4.55172 |      29 |  9.72414 |      9   |
|          4.55556 |     293 |  9.19454 |      8   |
|          4.5625  |     139 | 10.9209  |      9   |
|          4.56757 |      43 |  9.81395 |      8   |
|          4.57143 |     410 |  9.9561  |      9   |
|          4.57471 |     135 | 10.0148  |     10   |
|          4.58333 |      24 | 10.0417  |      8   |
|          4.58475 |     141 | 11.7589  |     10   |
|          4.58621 |      36 | 12.2778  |      9   |
|          4.58824 |      71 | 10.5352  |      9   |
|          4.6     |     923 | 10.104   |      9   |
|          4.60714 |      31 |  9.83871 |      8   |
|          4.61111 |      46 |  9.78261 |      8.5 |
|          4.61538 |     155 | 10.1871  |      8   |
|          4.61702 |      47 | 13.9574  |     13   |
|          4.62    |     120 |  9.5     |      9   |
|          4.625   |     370 | 10.5784  |     10   |
|          4.62963 |      30 | 11.6333  |     10   |
|          4.63158 |      57 | 10.614   |      9   |
|          4.63333 |      41 |  9.85366 |      8   |
|          4.63636 |     144 |  9.45139 |      8   |
|          4.64286 |      94 | 10.9149  |      9.5 |
|          4.64706 |      19 | 10.0526  |      9   |
|          4.64789 |      91 |  9.64835 |      9   |
|          4.65    |      40 | 12       |      9.5 |
|          4.65079 |      68 | 10.7941  |     10   |
|          4.65217 |      25 |  8.96    |      9   |
|          4.65517 |      36 | 10.5278  |     10   |
|          4.65625 |      36 | 14.7778  |     13   |
|          4.66667 |    3372 | 10.0033  |      9   |
|          4.67742 |      32 |  9.3125  |      8   |
|          4.68    |      52 |  9.55769 |      8   |
|          4.68421 |      83 | 11.012   |      9   |
|          4.6875  |      83 | 10.7108  |      9   |
|          4.69231 |     198 | 10.9394  |     10   |
|          4.69444 |      37 | 10.8378  |     11   |
|          4.7     |     350 |  9.93143 |      9   |
|          4.70588 |      71 | 10.0563  |      8   |
|          4.71429 |     790 |  9.60506 |      8   |
|          4.71739 |      50 | 10.4     |      9   |
|          4.71875 |      67 | 10.6269  |      9   |
|          4.7193  |      64 | 12.7969  |      9.5 |
|          4.72    |      26 |  9.30769 |      7.5 |
|          4.72222 |       4 |  5.5     |      6   |
|          4.72414 |      99 |  9.92929 |      9   |
|          4.72727 |     278 | 10.9964  |      9   |
|          4.73077 |      34 | 13.7941  |     10   |
|          4.73333 |     133 | 11.0827  |     10   |
|          4.73684 |     191 | 11.2618  |     10   |
|          4.73913 |      97 |  9.12371 |      9   |
|          4.74074 |      57 |  8.49123 |      8   |
|          4.74194 |      34 |  7.14706 |      7   |
|          4.74419 |      50 | 11.76    |     10   |
|          4.75    |    2426 | 10.3458  |      9   |
|          4.7619  |      24 |  9.04167 |      7.5 |
|          4.76471 |      55 |  9.67273 |      8   |
|          4.76744 |      43 |  8.53488 |      7   |
|          4.76923 |     296 | 10.6351  |     10   |
|          4.77273 |      47 | 10.7447  |      9   |
|          4.77358 |      59 |  9.79661 |      9   |
|          4.77419 |      32 |  7.25    |      6   |
|          4.77778 |     532 | 10.8703  |      9   |
|          4.78261 |      52 | 15.0962  |     14   |
|          4.78571 |     134 | 11.2239  |     10   |
|          4.78947 |      22 | 10.6818  |      9.5 |
|          4.7907  |      51 | 10.2353  |     10   |
|          4.79167 |      24 | 10.7917  |     10.5 |
|          4.79661 |      68 | 10.3971  |      8   |
|          4.8     |    1906 | 10.138   |      9   |
|          4.80702 |      62 |  9.5     |      8   |
|          4.80769 |      27 | 10       |      8   |
|          4.80952 |      22 |  7.54545 |      6   |
|          4.8125  |     148 | 11.0405  |      9   |
|          4.81481 |      32 |  8.5625  |      7.5 |
|          4.816   |     137 |  9.25547 |      8   |
|          4.81818 |     308 |  9.6039  |      8   |
|          4.82222 |      47 | 10.7234  |     10   |
|          4.82353 |      56 |  9.25    |      9   |
|          4.82609 |      23 |  9.78261 |      7   |
|          4.82857 |      37 |  9.05405 |      8   |
|          4.83333 |    1296 |  9.74769 |      9   |
|          4.83871 |      32 | 11.25    |      9   |
|          4.84211 |      38 |  8.89474 |      8   |
|          4.84615 |     165 | 10.2727  |      9   |
|          4.85185 |      65 |  9.67692 |      8   |
|          4.85714 |    1268 | 10.0158  |      9   |
|          4.86154 |      66 |  9.10606 |      8   |
|          4.86301 |      83 |  8.77108 |      7   |
|          4.86667 |     226 | 10.8142  |      9   |
|          4.86842 |      42 |  9.7619  |      8   |
|          4.86957 |      48 |  7.375   |      8   |
|          4.87179 |      41 |  8.97561 |      9   |
|          4.87356 |      90 | 11.0444  |     10   |
|          4.875   |     834 |  9.98082 |      9   |
|          4.87755 |      54 | 10.6296  |      9.5 |
|          4.88235 |     111 |  9.87387 |     10   |
|          4.88571 |      35 | 10.7429  |      8   |
|          4.88776 |     110 |  8.33636 |      7   |
|          4.88889 |     650 | 10.3877  |      9   |
|          4.8913  |      51 | 11.1176  |     11   |
|          4.89474 |      47 | 10.3404  |      8   |
|          4.89655 |      37 | 10.0811  |      9   |
|          4.9     |     482 |  9.93361 |      9   |
|          4.90244 |      44 |  8.68182 |      9   |
|          4.90323 |      32 | 10.5     |      9   |
|          4.90476 |      66 | 10.1667  |      8   |
|          4.90625 |      32 | 10.0938  |     10   |
|          4.90909 |     485 |  9.82887 |      9   |
|          4.91071 |      60 |  9.9     |      8   |
|          4.91667 |     224 | 10.4955  |      9   |
|          4.92308 |     458 |  9.81659 |      8   |
|          4.92857 |     258 | 10.3682  |      9   |
|          4.93333 |     196 |  9.69898 |      8   |
|          4.9375  |      33 |  9.66667 |      7   |
|          4.93878 |      62 | 10.2581  |      9   |
|          4.94118 |     174 |  9.90805 |      9   |
|          4.94444 |      94 | 10.1277  |      9   |
|          4.94737 |      57 | 10.9123  |     10   |
|          4.95    |      45 | 11.6222  |     11   |
|          4.95122 |      44 |  9.43182 |      9   |
|          4.95238 |      22 |  8.45455 |      7   |
|          4.95455 |      47 | 11.1277  |     10   |
|          4.95652 |      72 |  9.15278 |      8   |
|          4.96    |     108 | 10.2407  |      9   |
|          4.96154 |      27 | 10.5556  |      9   |
|          4.96296 |      29 |  9.10345 |      8   |
|          4.96552 |      33 | 11       |      9   |
|          4.97059 |      75 | 11.0667  |     10   |
|          4.97368 |      40 | 10       |      9   |
|          4.98113 |      58 |  9.53448 |      8.5 |
|          5       |   34719 | 10.0807  |      9   |


## Assessment of Missingness

### NMAR Analyiss
The rating column in the recipes dataframe is not missing at random (NMAR). There are some recipes in the dataset that have not yet been rated causing the data for rating column to be missing. Since the chance that the rating for a recipe will be missing depends on the actual missing value, the values in the rating column are not missing at random. Any additional data that I might want to obtain are Boolean values stating if the recipe has been rated or not, which could explain the missingness, thereby making the column missing at random.

### Missingness Dependency
