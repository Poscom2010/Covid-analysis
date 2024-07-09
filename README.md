# Africa Covid 19  - Analysis

## Project Overview 
The COVID 19 was recorded in the books of history as one pandemic which caused an outcry, deaths and  serious economic instability in the world. Even the most developed countries were not spared from its wrath. The most developed countries despite having effective and efficient health systems, incurred serious losses wit highest infections and death rates. After reflecting on the effects of COVID 19 in countries like US and Canada as well as China, which are well known to have the economic and political muscles to wrestle the pandemic, one wonders, if the tide was strong enough to  overturn the big boats, how then did the developing countries managed? This then sparked an interest for a deep dive analysis of COVID 19 in Africa as a whole.It is against this background that this project became a neccessity.Even though the stingy of COVID 19 started to decline around the end of 2022, the data source or dataset had data from 2019 - 2023. However, there were serious gaps in countries reporting post 2022. As such, the project focus on the 2019-2022 period.  Critical questions were focused on interrogating and consulting the data on  how COVID 19 affected Africa and how African countries fared. Which countries were affected the most than others.

# Data Sources
A triangulation of different data sources assisted in examining the COVID 19 in Africa from different angles. Two main data sources were used as follows:  
 1. [Our World in Data for all] (https://ourworldindata.org/explorers/coronavirus-data-explorer)
 2. [Anshul Sharma from Kaggle] (https://www.kaggle.com/code/anshuls235/india-vs-covid19/input)

# Tools
   
  1.  **Excel**  was used as initial cleaning of data and prepare the CSV file for easy importing to My SQL workbench.
  2.  **MySQL Workbench** - for further data cleaning, manipulation and analysis  
  3. **Tableau** used for visualizations and creating report
      
 ### Data Cleaning /Preparation
 
1. ### Data Loading
In order to be able to load the data successfully into the Mysql workbench, a database was created and the columns in the dataset and their data types were created first. But before, the date column data was in a wrong format (dd/mm/yyyy) and was converted to SQL data format first  as (yyyy/mm/dd). This was a solution after several unsuccessful attempts. The Mysql import table wizard was utilized and data was successfully imported into Mysql workbench.
  
2. ### Handling missing values
The dataset had lots of  blank spaces (missing data). For instance, the new cases column was recording new cases as they are reported, when there were no cases, the cells were blank instead of having a 0. Therefore, this was handled easily in excel by replacing all blank with 0. This successfully removed the issues of having NULL values.

3. ### Data Cleaning and Formating
After importing the data, all the data types were checked and confirmed to be in the required data type.There after, data Manipulation began. To confirm if the  data was imported in the designated or required format i used the DESCRIBE function. Also i realized the column location was spelled wrongly with some fun character ('ï»¿location'). This would make it difficult when calling the calumn during sql queries. As such i had to change the column name to 'location'. As i was investigating the data, i noted a lot of anomalies.The dataset had a total of  58 countries instead of 54 with other new known partly Oversears departments being recorded as  standalone African  countries (Mayotte,Saint Helena and Reunion as overseas Departments of France near Madagascar).I then decided to clean or delete these records from the dataset and stick to the 54 African countries.

## Below are some of the queries i depolyed during the data cleaning and formatting process

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
EDA means exploring the dataset or conducting a deep dive into the data, to understand the data structure, characteristics and identify issues that might need to be corrected. Above all, EDA assists in understanding the quirks and innuendos of the data. Moreso, during EDA, one can as well be in the light to realize if there is enough data required or sufficient to answer the  researcg questions. The main purpose of this activity was to answer the folloing bussines questions:

1. Give an overal picture or perspective on the effcts of COVID 19 in Africa. In other words, how badly was Africa ravaged by COVID 19, that is in terms of new cases, vaccination and death rates.   
2. Which  are the top 11 countries that had *Highest COVID 19 infections in relation  to population
3. Which are the **top 5 countries** that managed well the COVID 19 pandemic
4. Which countries had   highest COVID 19 positivity yield      
5.  Any correlation between between overal deaths in Africa and  vaccination rate


## Data Analysis
During the analysis and exploration phase, different techniques were used with simple and complex sql queries. Below are some of the queries used and the purpose of the query.

### extracting global numbers from the dataset
```
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
 As seen on the dashboard above, based on the data availabe at the {our world our data] during that time, Africa had a total population of # 1.38 billion.*A 0.81% of its population was ifected by COVID 19, which translates to about 11.31 million people.Therefore, in Africa had > 1% chances of getting infected i.e less chances of being infected. However, those who got infected had a 2.14% chances of dieing due to COVID 19 infection. In total, about 242k people lost their lives due to COVID 19 infection.In terms of vaccinations, about 531 million people were vaccinated, that is 439.2 million were fully vaccinated and 91.2m only recieved single dose vaccinnation.

 On a country level,  top 3  countries that had highest chances of death after one had been infected by COVID 19 was Sudan at 7.89%, Somalia 4.95% and followed by Egypt at 4.81% respectively. One can also note that whilst Sudan had the highest chances of death due to COVID 19, THE SAME COUNTRY WAS AT NUMBER 9th in terms of vaccination rates (Population vs number vaccinated).
 
 So the question arises, since we have more than 50 countries in the continent, how did Africa cope at a country level. Which countries were seriously amputated and which ones did well to manage the  scorge of COVID 19? Next, these are some of the questions that were addressed in this analysis project.


#### 2. Which are the top 11 countries that had *Highest COVID 19 infections in relation  to population*
Among the top 10 countries, South Africa  is number one country that had the highest COVID 19 infections in Africa in relation to her population. Second was  Tunisia, followed by  Egypt, Libya and  Ethopia.Even though it is well known, that Nigeria is the labor horsepower for Africa with the highest population in the continent, contrastingly, when it comes to  to COVID 19 infections, the country was on number 11th with about 267k infections.
     
  #### 3.  Which are the **top 5 countries** that managed well the COVID 19
There are some countries that had few infections and deaths with high COVID 19 vaccinations.Though this project is not in a position to suggest that these fatalities were due to high vaccinations, what is certain is that there are also countries which had high infections, deaths and also vaccination. Egypty is one country which was ranked as 3rd on the dashboard in having highCOVID 19 burden,high chances of death and high deaths  and 3rd as well in terms total vaccination in relation to population.

Nigeria as one country with highest population in Africa, was nowhere to be seen near the top 10 countries with highest  fatalities. Ranked 10th in terms of infections and leading as a pace setter in terms of vaccinations. A total of 94 million people were vaccinated in Nigeria. However, Nigeria performed badly in terms of COVID 19 testing. Only 5 million people were tested from the 218m population, an area where South Africa excelled as seen on Fig 2 below. South Africa on the other hand, was leading in terms of infections, deaths but then ranked 6th in terms of vaccinations in relation to its total population.

 ### 4. Which countries had   highest COVID 19 positivity yield
 ![Screenshot (247)](https://github.com/Poscom2010/Covid-analysis/assets/112340892/c4160b3c-9e6a-43b1-a589-56acfe35d4c4)


  Though South Africa had highest infections and deaths, it is the only African country that had COVID 19 tests above 10 million.In fact, majority of tests in Africa were below 12 million as seen above.
      

### 5. Any correlation between between overal deaths in Africa and  vaccination rate
In order to answer this question,  number of people reported succumbing to COVID 19 were plotted against time. Based on the findings from the data, Africa experienced high deaths before the advent of vaccines.

![Screenshot (248)](https://github.com/Poscom2010/Covid-analysis/assets/112340892/f482c8f7-3bd3-4c16-be55-f211ff76ff13)

Between the period of Jan 2020 to May 2021,Africa witnessed a surge in covid 19 infections. In particular, in January 2021 a record high of  793.14k infections we recorded. During the same time that is when African countries started to prioritize vaccination and testing. As such, since deaths were going up, vaccinations started to increase signficantly.
Therefore, from Jan 2021, a positive correlation between increase in vaccinations and significant drop in covid 19 infections and deaths was witnessed.From Feb 2021 all countries were prioritizing vaccination and workplaces were also requesting vaccination certificates. The result was an increase in vaccinations and a drop in deaths and infections. Does this then means vaccinations worked? Unfortunately, this question was beyond the scope of this project.
      

## Recommendations

1. **Proactive vaccination than reactive** - from the data above, it is clear that Africa started to prioritize vaccinations and tests after September 2020 record highs in deaths and infections with full implementation from May 2021. Before this phase, deaths and infections were being reported, however the numbers did not raise enough alarm.It is therefore recommended for Africa to embrace any new pandemics and immediately implement preventative measures.
    
2. **Recording and reporting of data for future use** - the data in this project went through serious data cleaning. Some countries did not reliably report data. For instance, some countries stopped reporting COVID 19 data. This then  deprives the opportunity to use available data to understand the COVID 19 epidemic and make informed decision making in the future.
   
## Limitations
1.**Incomplete data**
The dataset for the project was downloaded from ourworldindata website, which is a public database. The data set had data from 2019 to 2023. However, majority of the countries stopped reporting data or had missing values from 2022. This then forced the project to be limited to 2021 only.

### References
1. [Our World in Data for all] (https://ourworldindata.org/explorers/coronavirus-data-explorer)
2. [Anshul Sharma from Kaggle] (https://www.kaggle.com/code/anshuls235/india-vs-covid19/input)

👍
💻 	
🌍
💡💡💡💡💡💡💡💡💡💡💡❤️❤️❤️❤️❤️❤️❤️❤️❤️❤️❤️❤️❤️💻 💻 💻 💻 💻 💻 💻 💻 💻 💻 💻 💻 👍👍👍👍👍👍👍👍👍👍👍👍👍👍👍👍👍👍👍👍👍👍👍🌍🌍🌍🌍🌍🌍🌍🌍🌍🌍🌍🌍

