# Mental Health Survey: Exploratory Data Analysis

An exploratory data analysis of CDC mental health survey indicators (BRFSS and PRAMS), 2011-2021. The project looks at how the average number of mentally unhealthy days changed over time, which states are highest and lowest, and how gender and race/ethnicity groups differ.

## Dataset

- **Source:** CDC mental health indicators from the BRFSS and PRAMS surveys, 2011-2021
- **Size:** 13,200 rows and 23 columns, covering 55 locations (50 states, DC, and 4 extra rows: United States, Guam, Puerto Rico, Virgin Islands)
- **What a row is:** a summary of a group of respondents (location + year + group + question + measure type), not an individual person
- **Three questions in one file**, with different units and populations, so they are analysed separately:

| Question | Unit | Who it covers |
|---|---|---|
| Recent mentally unhealthy days among adults | average days per month | all adults |
| At least 14 recent mentally unhealthy days | % | women aged 18-44 |
| Postpartum depressive symptoms | % | new mothers |

## Questions I answered

1. **Has the average number of bad mental health days changed over time?**
   Yes. The typical state (the median across states) rose from about 3.7 days a month in 2011 to 4.8 in 2021. Every state with data in both years was higher in 2021, typically by about 1 day. For women aged 18-44, the share with 14+ bad days rose from about 14.5% to 23.9%.

2. **Which states are highest and lowest?**
   In 2021, West Virginia (6.1), Arkansas, Tennessee and Alabama (5.8) and Louisiana (5.7) are highest. Hawaii (3.7), South Dakota and North Dakota (4.0), New York and Illinois (4.2) are lowest. The top five are clearly above the bottom five, but states within a group cannot be reliably ranked because their confidence ranges overlap.

3. **How do gender and race/ethnicity groups differ?**
   Women report more bad days than men in every year, and the gap grew from about 1.0 day (2011) to about 1.85 days (2021). Multiracial respondents report the most bad days. The race/ethnicity comparison is less reliable because many states have no value for these groups.

## Approach

- **Data checks:** no duplicate rows, no impossible values, confidence limits always bracket the value, labels are clean. Redundant columns (`YearEnd`, `Topic`, ID columns, `DataValueAlt`) were confirmed redundant before being dropped.
- **Missing values:** about 19% of values are blank. They are suppressed (sample too small) or unavailable, not mistakes, so they were left as missing and not filled. They are concentrated in race/ethnicity groups.
- **Focus on question 1:** it has the most rows, covers all years and has gender and race/ethnicity groups. Question 2 is used for an overall trend only (race/ethnicity estimates are missing for many states), and question 3 is excluded (one year, one group, 23 values).
- **Age-adjusted mean:** each result appears as both a Mean and an Age-adjusted Mean. I used the age-adjusted version because the analysis compares states and groups, and it avoids double counting. The two are very close (correlation 0.96, typical gap 0.1 days).
- **States only:** Guam, Puerto Rico, the Virgin Islands and the "United States" summary row were removed from state comparisons (51 locations kept).
- **Typical state:** trend lines use the median across states so a few unusual states do not pull the line.

## Limitations

- Each row summarises a sample of people, and BRFSS surveys a new sample of adults each year, so the results describe state averages, not changes in individuals.
- The data shows what changed, not why. No causes are claimed.
- Many estimates are blank, especially for race/ethnicity groups, and the set of reporting states changes by group and year.
- The "typical state" is a median of states, not a population-weighted national average.
- The file does not say which standard age mix was used for the age-adjusted values.

## How to run

1. Put `mental_health_data.csv` in the project folder.
2. Update the file path in the first data-loading cell of the notebook.
3. Install the libraries: `pip install pandas numpy matplotlib seaborn jupyter`
4. Open `mentalhealthanalysis.ipynb` and use **Restart & Run All**.

## Tools

Python, pandas, NumPy, Matplotlib, Jupyter Notebook
