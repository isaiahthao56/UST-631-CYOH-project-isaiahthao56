# The Rise of Plant-Based Protein Drink Alternatives 


## 1. Research Question
This project aims to analyze the key differences between plant-based and animal-based protein drinks. This topic is important because it touches upon issues such as healthy dieting, food labeling transparency, and ultra processed foods. It is increasingly crucial to make informed decisions regarding one's diet when companies have flooded the market with "high protein" products. While the importance of protein is highly debated, this project is an introduction into one convenient and cheap source: protein drinks. Animal-based protein drinks, such as whey, are the gold standard for protein sources. In recent years, plant-based food products have seen explosive growth and demand. This project aims to compare plant-based protein drinks to animal-based protein drinks. The main research question is: do plant-based protein drinks provide the same quantity and quality of protein as animal-based drinks?


## 2. Hypothesis
Test Statistic: Difference in mean calories from protein ratio between plant-based and animal-based protein drinks.

Null Hypothesis: There is no difference in the mean protein ratio between plant-based and animal-based protein drinks.

Alternative Hypothesis: There is difference in the mean protein ratio between plant-based and animal-based protein drinks. This is a two-tailed test because plant proteins could have a greater or smaller protein ratio. 


## 3. Data Description
The data source of this project comes from the USDA FoodCentral database. The data is a collection of product nutrient label information provided by private companies. This data set is the result of a private-public partnership with the goal of enhancing public food health transparency. The database includes several tables that follow a normalized relational database design. The three tables of interest used in this project are named: ‘Branded’_Food’, ‘Food_nutrient’ and ‘Food’. The tables are linked by an internal key identifier ,‘fdc_id’, for each product. 

Branded_Food – The largest table in the data set by memory size (2.9 GB). It contains product information such as brand, product category and ingredients. It contains 2 million rows and 21 columns.

Food_nutrient- This table contains detailed nutrient information for each product in the Branded_Food table. Each row is a unique combination of fdc_id and nutrient_id. For example, one product would have x number of rows for the x number of nutrients it has. The table contains 26 million rows and 11 columns.

Food – This table contains the description and other miscellaneous columns for each product. It contains 2 million rows for each product and 8 columns.

Before exploratory analysis could be conducted, it was necessary to conduct transformations because the datasets were normalized.  In addition, the giant size of the files made it difficult to process. The first step in transformation was filtering unnecessary rows to make analysis more feasible. 

    1.	The Branded table was imported as a Pandas DataFrame and filtered to only contain products with a food category matching “'Energy, Protein & Muscle Recovery Drinks'”. 

    2.	Next, the resulting table was joined to the Food Table to obtain product descriptions

    3.	The last join involves the Food_nutrient table that contains the actual numerical nutrient information.

    4.	After merging the three tables, the final step is pivoting the rows into columns and renaming the nutrients from id numbers to names. 

    5. Observations with a low or very high calories from protein ratio were removed. In addition, observations with less than 10 grams of protein were removed. 

The final resulting table contains 4093 rows and 25 columns. Each row represents a protein drink product. Key variables include:  Ingredients, Description, Calories, Protein, Fiber and the 9 amino acids.


## 4. Methods
The selected test statistic was the difference in mean protein ratios between animal-based and plant-based drinks. This statistic was chosen because it represents the proportion of calories in a drink that derives from protein in the drink. We take the difference because we are interested in whether one source type provides a higher ration than another. In the permutation test, we simulated data under the null by shuffling the source type column. This simulates the null because it creates no association between source type and protein ratio observation values. 10,000 permutations were conducted to generate a null distribution. 

In the first bootstrap we selected the mean difference in fiber amounts in grams. This measure is important because fiber is a beneficial nutrient that typically has a higher concentration in plant-based products.  10,000 bootstrap samples were created by resampling with replacement to create a reference distribution. Then a 95% confidence interval was placed on the reference distribution. 

The second bootstrap was conducted on the difference in median number of ingredients between plant-based and animal-based drinks. The number of ingredients is an important measure because it can signifify highly processed products. Highly processed products are typically less nutritious and contain filler ingredients. This measure does not follow the Central Limit Theorem because it is a discrete value that can only take whole or half numbers. Products cannot have half of an ingredient. Even after thousands of bootstrap samples, the curve will not smooth out because there are a limited number of outcomes. This bootstrap was conducted in the same method as the first bootstrap.


## 5. Results
The null distribution of the permutation test on difference in mean protein ration resulted in a normal curve centered around 0. Comparing the observed value of 0.11 to the null distribution, the value lands extremely far to the right. 

The permutation test yielded a p-value of 0.00. There were no simulations with a difference in mean protein ratio as extreme as the observed value of 0.11, in either direction. With a p-value below the significance threshold of 0.05, we reject the null hypothesis. The difference in mean protein ratios of 0.11 is likely not due to randomness. This result is consistent with pre-existing notions of animal-based proteins. In context, the results provide evidence that the average animal-based protein drink gets more of its calories from protein than plant-based protein drinks.


## 6. Uncertainty Estimation
The first bootstrap on difference in mean fiber was constructed with 10,000 boot samples. The reference distribution shape follows a normal distribution in line with the central limit theorem. The distribution is centered around the observed value of 3.45 grams. A 95% confidence interval of the middle 95% observations produce the bounds of 2.93 and 3.97 grams of fiber. This interval is interpreted as the range of values we expect the true statistic lie. We are 95% confident that the true difference in mean fiber between plant-based and animal-based protein drinks is between 2.93 and 3.97 grams. In context, plant-based protein drinks provide around 3-4 grams more fiber.

The second bootstrap was conducted on the difference of median number of ingredients. The reference distribution of 10,000 boot sample appears very jagged, not in line with the Central Limit Theorem. More than half of the boot samples resulted in a statistic that was the observed statistic of 4 ingredients. The spread of the distribution is very limited, the values range from 3 to 6, with only 5 unique values.  The confidence interval of the middle 95% of observations ranges from 3 to 5 ingredients. Thus, we are 95% confident that the true difference in groups is between 3 and 5 ingredients. In context, a typical plant-based protein drink has 3 to 5 more ingredients than a typical animal-based protein drink. 


## 7. Limitations
There are critical limitations of this data that should be taken into consideration. First, the data is provided voluntarily by private companies. According to the FDA, the nutrients reported on nutrition labels are permitted to be 20% off actual measurements. This results in uncertainty about the reported protein amounts. Protein amounts are likely to be inflated to attract customers. This can create bias in the data that skews protein amounts. 

Second, there is data missing not at random in the data set. Because federal oversight is limited, not all products are required to undergo standardized testing. Producers may omit nutrients that are not necessary to hide poor quality ingredients. In this analysis, only a small portion of products reported the amino acids profile.  This made it difficult to accurately assess which products contained complete proteins. 

Regarding the assumption of independence, some observations may not be completely independent. Many products are produced by the same supplier, under different labeling. In addition, producers use the same base formula with different flavorings such as vanilla or chocolate. This can result in many observations with replicated nutrients values. This may alter the analysis because one brand with multiple products can overweight unique products. This creates bias that favors large brands. This is especially significant in this project because the plant-based industry is still an emerging market. On the other hand, animal-based protein drinks have larger, more established brands. 


## 8. References

Datasets: https://fdc.nal.usda.gov/download-datasets/

FDA, "Interactive Nutrition Facts Label - Protein." U.S. Food and Drug Administration, Oct. 2021, www.accessdata.fda.gov/scripts/InteractiveNutritionFactsLabel/assets/InteractiveNFL_Protein_October2021.pdf.

Li Day, Julie A. Cakebread, Simon M. Loveday, Food proteins from animals and plants: Differences in the nutritional and functional properties, Trends in Food Science & Technology, Volume 119, 2022, Pages 428-442, ISSN 0924-2244, https://doi.org/10.1016/j.tifs.2021.12.020.



