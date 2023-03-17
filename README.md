# Project 1: Data cleaning and analysis on global shark attacks

## Objective

In this project I was working with a large dataset attacks.csv which is freely available on [Kaggle](https://www.kaggle.com/datasets/teajay/global-shark-attacks?resource=download).

The goal was to import the file, clean it, and prepare it for analysis. With the clean dataset, I was then able to visualize data that validates the conclusions based on my hypoteses.

## Hypothesis

### **Hypothesis 1. Shark attacks are more common in the recent years.**
---

### **Hypothesis 2. Shark attacks are more likely to happen in warm waters.**

- in certain locations
- in warmer months, when more plankton is present in the waters
- attacks are more fatal in certain countries (oceans)
---

### **Hypothesis 3. Some activities are more fatal in a shark attack than others.**
---

## Cleaning methods

Original dataset was presented with 25723 entries in 24 columns. I first explored the columns, to see what data is available, in order to be able to pre-define the hypothesis.

Some columns contained irrelevant data for those hypothesis (e.g. Case Number.2, original order, Unnamed: 22, Investigator or Source). 

Others, even though they presented an interesting starting point for my analysis, appeared to be too fragmented to be easily used (e.g. Species).

### 1. Initial clean-up

- Dropped columns
- Dropped duplicates

14 unnecessary columns, and 19418 rows with null values were dropped. This resulted in a cleaner dataset with 6305 entries.

### 2. Cleaning the columns

- Dropped rows

Rows with null values in important columns were dropped if they were descriptive, and couldn't be replaced with an average (Date, Year, Type, Country).

#### **Column: Sex_**

- Lambda
- Dropped column

New Sex column was created, with F/M values copied from the old Sex_ column. Null, infinite and invalid entries were renamed to 'unknown'.

Old Sex_ column was dropped.

#### **Column: Type**

- Regex replace
- Regex contains

Some entries were renamed, to match others with the same meaning. Invalid entries were removed.

#### **Column: Area**

- Fill null values

Null values were replaced with 'unknown'.

#### **Column: Age**

- Regex extract
- Regex replace & dropna
- Lambda

All ages in and incorrect format were removed.

Infinite values got replaced with nulls. All null values got dropped. Data type was changed to integer.

#### **Column: Year & Month**

- Regex replace & dropna
- Lambda
- Regex extract

Infinite values got replaced with nulls. All null values got dropped. Data type was changed to integer. Invalid entries were removed.

New column **Month** was created, extracting the month from the column Year. Null values were dropped.

#### **Column: Activity**

Entries occuring less than 4 times got removed.

#### **Column: Fatal (Y/N)**

- Regex contains

All invalid entries got removed.

### 3. Final cleaned dataset

Cleaned dataset with no null values was left with 2158 entries, and distributed in 11 columns:

```python
0   Case Number  2158 non-null   object
 1   Date         2158 non-null   object
 2   Year         2158 non-null   int64 
 3   Type         2158 non-null   object
 4   Country      2158 non-null   object
 5   Area         2158 non-null   object
 6   Activity     2158 non-null   object
 7   Age          2158 non-null   int64 
 8   Fatal (Y/N)  2158 non-null   object
 9   Sex          2158 non-null   object
 10  Month        2158 non-null   object
 ```

Exported to a new file sharks_clean.csv

## Analysis

For the analysis, I decided to work only with _unprovoked_ shark attacks, with 1984 entries.

For easier visualization, new columns _Decade_ and _Hemisphere_ were created.

#### **New column: Decade**

- apply Lambda

#### **New column: Hemisphere**

- apply function

List of countries from the dataset was taken, and split between two new lists, _north_ and _south_. This was done manually, by removing S.hemisphere countries from _north_ and pasting them into _south_.

In the case of countries across both hemispheres, but with most territory in one hemisphere, that was the selected choice.

'North' and 'South' values were applied.

General names, like 'Pacific ocean' or 'Atlantic ocean' were defined as 'Other'.

## Visualization

![Shark attacks by decade](/images/shark_attacks_decade.png)

Data shows an increasing trend in global shark attacks throughout the years. The first substantial increase happened in the 1960s, and the second one in the 2000s.

In order to better understand the reasons behind this trend, additional analysis would be needed. One presumption could be this is due to global warming and warmer waters, which might attract more plankton and fish that the sharks feed on. 

On the other hand, more research would need to be done on the data collection methods, which might have changed throughout the decades.

There seems to be no significant difference in the number of _fatal_ attacks after the 1920s, which implies that the frequency of fatality in shark attacks has _decreased_.

![Fatality of shark attacks by decade](/images/shark_attacks_decade_fatality.png)

Looking closer at the frequency of fatal vs. non-fatal attacks, it can be concluded that there was a turn after the 1940s. Majority of shark attacks after that decade were not fatal anymore, compared to the decades before. 

With each subsequent decade, this trend has been futher decreasing. Finally, after 1980s, less than 15% of all shark attacks were fatal.

![Shark attacks per month and hemisphere](/images/shark_attacks_month_hemisphere.png)

Data from the Southern Hemisphere shows that most attacks happen in the months between Dec-Mar, and in the Northern Hemisphere during the months between Jun-Sep.

These are all summer months in the corresponding hemisphere, so it can be concluded that majority of shark attacks happen during the summer months.

Observing the whole year, for the months between Dec-Mar, overall there's more attacks in Southern Hemisphere, and for the months between Apr-Nov, there are more attacks in the Northern Hemisphere.

![Shark attacks per area](/images/shark_attacks_area50.png)

Globally, the areas with most shark attacks are located in Florida (USA), NSW (Australia), KwaZulu-Natal (S.Africa), Hawaii (USA), Eastern Cape Province (S.Africa), and California (USA).

![Shark attacks per country](/images/shark_attacks_country20.png)

Furthermore, looking at countries, by far most registered attacks happen in the USA, followed by Australia and South Africa.

Eventhough the USA leads in number of shark attacks overall, the most fatal attacks have happened in Australia.

![Frequency of fatality per country](/images/shark_attacks_country_fatality.png)

Comparing fatality rates across the countries where at least 20 attacks were registered, some places have a higher rate of death-resulting attacks. 

In Mexico, approximately 50% of all attacks ended with fatality. And in Australia, Brazil, New Zealand and Reunion, this rate is over 30%.

Only about 5% of all shark attacks in the USA end with fatality.

![Shark attack distribution per victim age](/images/shark_attacks_age_dist.png)

Shark attacks happen more commonly, and are also more fatal among younger population. On average, population below 25 y.o. is most often affected.

![Fatality per victim age and sex](/images/shark_attacks_age_sex.png)

There were sustantially more victims and fatalities among the male population.

![Fatality of shark attacks per acitivity](/images/shark_attacks_activity50.png)

Surfing is the activity involved in most of the shark attacks overall. However, swimming is the activity that results in most fatal attacks.

![Frequency of fatal shark attacks per acitivity](/images/shark_attacks_activity_fatality.png)

Comparing fatality rates across activities where at least 50 attacks were registered, we can conclude that swimming is the most fatal one, with almost 40% of all attacks resulting in death.

This is followed by body-boarding, where over 20% of all attacks end fataly.

Even-though surfing is involved in most shark attacks, only about 10% of those end with fatality.

## Conclusion

Shark attacks have been increasing in the recent years, however, on the contrary, attacks ending in fatality have been decreasing.

Warm summer waters are corelated with higher frequency of the attacks, both in North and South hemispheres. This could be related with the fact that the waters are warmer, with more plankton and fish present, that attract the sharks. On the other hand, this could be due to higher leisure activity in the sea during summer months. To confirm the reasons, further research would need to be done.

Locations with most shark attacks are the USA, Australia and South Africa. Eventhough the USA leads in number of shark attacks overall, the most fatal attacks happen in Australia.

Surfing is the activity involved in most of the shark attacks overall. However, swimming is the activity that results in most fatal attacks.

