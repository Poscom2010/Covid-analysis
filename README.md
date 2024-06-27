# Covid 19  in Africa - analysis

## Project Overview 
COVID 19 pandemic  caused havoc and instability in the world. Even the most developed countries were not spared from its wrath. The most developed countries which had better health health standerds had  even the highest infections and death rates. Looking at the after effects of COVID 19 in countries like US and Canada as well as China, which are countries well known to have the economic and political muscles to wrestle the pandemic, it then calls for a deep dive into the less developed. It is against this background that a deep dive into COVID 19 in Africa became a neccessity of this project.Even though the stingy of COVID 19 started to decline around the end of 2022, the data is up to December 2023 (2020-2023. This then gives an up to date analysis and presentation of the how covid 19 affected Africa and how African countries fared. Which countries were affected the most that others.

# Data Sources
A triangulation of different data sources assisted in examining the COVID 19 in Africa from different angles. Two main data sources were used as follows:  
 1. [Our World in Data for all] (https://ourworldindata.org/explorers/coronavirus-data-explorer)
 2. [Anshul Sharma from Kaggle] (https://www.kaggle.com/code/anshuls235/india-vs-covid19/input)

 # Tools
   
  1.  **Excel**  was used as initial cleaning of data and prepare the CSV file for easy importing to My SQL workbench.
  2.  **MySQL Workbench** - for further data cleaning, manipulation and analysis  
  3. **Tablea** used for visualizations and creating report
      
 ### Data Cleaning /Preparation
 1. ### Data Loading
In order to be able to load the data successfully into the Mysql workbench, a database was created and the columns in the dataset and their data types were created first. But before, the date colum data was in a wrong format (dd/mm/yyyy) and was converted to SQL data format first  as (yyyy/mm/dd). This was a solution after several unsucessful attempts. The Mysql import table wizard was utilized and data was successfully imported into Mysql workbench.
  
2. ### Handling missing values
The dataset had lots of intention blank spaces. As in, for instance, the new cases column was recording new cases as they are reported, whenre there were no cases, the cells were blank instead of having a 0. Therefore, this was handles easily in excel by replacing all blank with 0. This successfully removed the issues of having NULL values.

3. ### Data cleaning and Formating
After importing the data, all the data types were checked and confirmed to be in the required data type.There after, Data Manipulation began - where other erequired important colums were required in order to fully satisfy the business task.To confirm the data was imported in the designated or required format i used the DESCRIBE function. Also i realized the column location was spelled wrongly with some fun character ('ï»¿location'). This would make it difficult when calling the calumn during sql quiries. As such i had to change the column name to 'location'. As i was investigating the data, i noted a lot of anomalies, 58 countries instead of 54 with other new know partly Oversears departments but regarded as African  countries (Mayotte,Saint Helena and Reunion as overseas Departments of France near Madagascar).I then decided to clean or delete these records from the dataset and stick to the 54 African countries.


```
 Describing the data and examine the data types 
DESCRIBE covid19_africar
```
```
Changing the location column name from 'ï»¿location' to proper location
ALTER TABLE covid_africar
CHANGE COLUMN `ï»¿location`  `location` VARCHAR (50);
```

# Exploratory Data Analysis (EDA)
EDA means exploring the dataset or conducting a deep dive into the data, to understand the data structure, characteristics of the data and identify issues that might need to be corrected. Above all, EDA assists in understanding the quirks and innuendos of the data.The main purpose of this activity was to answer the bussiness questions as follows:

 1. Give an overal picture or perspective on the effcts of COVID 19 in Africa. In other words, how badly was Africa ravaged by COVID19, that is in terms of new cases, vaccination and death rates - a graphical view would assist.

    
 2. Which are top 10 countries of the 54 in Africa had:
      - Highest COVID 19 infections vs population
      - Highest tests vs population
      - Highest positive yield vs tests conducted
      - Highest/ strictest Stringency Index
   
   
        
  3. Which are **the top 5 countries* that did well to avert the COVID 19 effects
  4. Which are the **bottom 15 countries** which did not do well  
          - having less tests vs population
          - less vaccinations and few peopple fully vaccinated
          
  5.  Which are the **top 5 countries** seriously ravaged by COVID 19 with highest death rates
        

   6. Any correlation between GDP and vaccination
   7. Any correlation between Stringency index and the total cases - in other words, did the strict rules implemented worked din countries where they were strict or they all perfomed the same just like countries that        had  relaxed regulations


## Data Analysis
To add some interesting codes used during the analysis and add some code chunks

```
-- extracting global numbers from the dataset
SELECT
SUM(DISTINCT population) total_population,
SUM(new_cases) total_infections,
SUM(new_deaths) total_deaths,
ROUND(SUM(new_cases)/ SUM(DISTINCT population)*100,2) AS infection_rate,
ROUND(SUM(new_deaths)/SUM(new_cases)*100,2) AS death_rate
FROM covid_africar;
```

### Average stringency index for all countries orderd by year and respective month for plotting
```
SELECT 
    YEAR(date) AS year,
    MONTH(date) AS month,
    AVG(stringency_index) AS avg_stringency_index
FROM
    covid_africar
GROUP BY YEAR(date), 
		MONTH(date)
ORDER BY YEAR(date),
			MONTH(date);
```
### Global numbers for Africa - total vaccinations and deaths by by year and month
```
---  Rolling number for Africa vaccinations
      SELECT 
    YEAR(date) AS year,
    MONTH(date) AS month,
    MAX(total_vaccinations) total_vaccinated,
    SUM(new_deaths)
FROM
    covid_africar
GROUP BY YEAR(date), 
		MONTH(date)
ORDER BY YEAR(date),
			MONTH(date);
```
### Checking if Africans accepted COVID 19 vaccinations and the level of protection
```
SELECT
    SUM(max_people_vaccinated) africal_total_vacc,
    SUM(max_fully_vaccinated)afriaca_total_fully_vac,
     ROUND(SUM(max_fully_vaccinated)/ SUM(max_people_vaccinated)* 100,2) AS full_protection_rate
    FROM
    (SELECT
     MAX(people_vaccinated) max_people_vaccinated,
    MAX(people_fully_vaccinated) max_fully_vaccinated
    FROM covid_africar
    GROUP BY location
    ) AS country_totals;
```

## Results/ Findngs
Now afetr all the data cleaning, manipulation and analysis, it is time to see what the data says right! Answering the analysis questions of interest. In order to do justice to all questions, i will go through each question and elaborate on the story from the data with reference to the Covid 19 Africa Data Analysis dashboard below.
![covid](https://github.com/Poscom2010/Covid-analysis/assets/112340892/8db47cb5-268a-4529-af1e-268dbe034d37)


#### 1. Give an overal picture or perspective on the effects of COVID 19 in Africa. In other words, how badly was Africa ravaged by COVID19, that is in terms of new cases, vaccination and death rates - a graphical view would assist*
 As seen on the dashboard above, based on the data availabe at the {our world our data] during that time, Africa had a total population of # 1.38 billion.*A 0.81% of its population was ifected by COVID19, which translates to about 11.31million people.Therefore, in Africa the population had > 1% chances of getting infected.However, those who got infected had a 2.14% chances of dieing due to COVID 19 infection. In total, about 241k people lost their lives due to COVID 19 infection.

 On a country level,  top 3  countries that had highest chances of death after one has been infected by COVID 19 was Sudan at 7.89%, Somalia 4.95% and Egypt at 4.81% respectively. One can also note that whilst Sudan had the highest chances of death due to COVID 19, THE SAME COUNTRY WAS AT NUMBER 9th in terms of vaccination rates (Population vs number vaccinated).
 
 So the question arises, since we have more than 50 countries in the continent, how did Africa cope at a country level. Which countries were seriously amputated and which ones did well to manage the  scorge of COVID 19? Next, these are some of the questions that were addressed in this analysis project.


#### 2. Which are the top 11 countries that had *Highest COVID 19 infections in relation  to population*
Among the top 10 countries, South Africa  is number one country that had the highest COVID 19 infections in Africa in relation to her population. Second was  Tunisia, followed by  Egypt, Libya and  Ethopia.Even though it is well known, that Nigeria is the labor horsepower for Africa with the highest population in the continent, contrastingly, when it comes to  to COVID 19 infections, the country was on number 11th with about 267k infections.
     
  #### 3.  Which are the **top 5 countries** that managed well the COVID 19
There are some countries that had few infections and deaths with high COVID 19 vaccinations.Though this project is not in a position to suggest that these fatalities were due to high vaccinations, what is certain is that there are also countries which had high infections, deaths and also vaccination. Egypty is one country which was ranked as 3rd on the dashboard in having highCOVID 19 burden,high chances of death and high deaths  and 3rd as well in terms total vaccination in relation to population.

Nigeria as one country with highest population in Africa was nowhere to be seen near the top 10 countries with highest  fatalities. Ranked 10th in terms of infections and leading as a pace setter in terms of vaccinations.A total of 94 million people were vaccinated in Nigeria.However, Nigeria performed badly in terms of COVID 19 testing.Only 5 million people were tested from the 218m population, an area where South Frica excelled as seen on Fig 2 below. South Africa on the other hand, was leading in terms of infections, deaths but the ranked 6th in terms of vaccinations in relation to its total population.

 ### 5.Which countries had   highest COVID 19 positivity yield
 ![Screenshot (247)](https://github.com/Poscom2010/Covid-analysis/assets/112340892/c4160b3c-9e6a-43b1-a589-56acfe35d4c4)


  Though South Africa had highest infections and deaths, it is the only African country that had COVID 19 tests bove 10 million.In fact, majority of tests in Africa were below 12 million as seen above.
      

### 6. Any correlation between between overal deaths in Africa and  vaccination rate
      
 ###  7. Any correlation between Stringency index and the total cases - in other words, did the strict rules implemented worked din countries where they were strict or they all perfomed the same just like countries that        had  relaxed regulations




## Recommendations

## Limitations

## References

### Definition of terms
Stringency Index  a composite measure  based on nine repsones indcators
