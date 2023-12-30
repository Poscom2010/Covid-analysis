# Covid 19  in Africa - analysis

## Project Overview 
COVID 19 pandemic  caused havoc and instability in the world. Even the most developed countries were not spared from its wrath. The most developed countries which had better health health standerds had  even the highest infections and death rates. Looking at the after effects of COVID 19 in countries like US and Canada as well as China, which are countries well known to have the economic and political muscles to wrestle the pandemic, it then calls for a deep dive into the less developed. It is against this background that a deep dive into COVID 19 in Africa became a neccessity of this project.

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
After importing the data, all the data types were checked and confirmed to be in the required data type.There after, Data Manipulation began - where other erequired important colums were required in order to fully satisfy the business task.To confirm the data was imported in the designated or required format i used the DESCRIBE function. Also i realized the column location was spelled wrongly with some fun character ('ï»¿location'). This would make it difficult when calling the calumn during sql quiries. As such i had to change the column name as well.Since COVID 19 was at its peak and all countries were required to report and record on the global and national systems, from the beginning of 2023, most countries started to move on and were nolonger reporting correct or actual numbers. As such, since the dataset had data spanning from  to **'2020-01-03' to '2023-12-19'**, i had to disregard data for year 2023.Also only 3 countries had data for 2023 (Angola, Benin and Algeria). This meant the project is for  3 years. Since filtering out 2023 data on each and every query was going to be heavy on the system, create long quiries and cumbersome, i then decided to create a copy table which had the data i was interested in.As i was investigating the data, i noted a lot of anomalies, 58 countries instead of 54 with other new unkonown Afriac countries (Mayotte and Saint Helena).I then decided to clean the data in MS excel  and re import again to mysql workbench for further EDA and prpeparation for analysis.


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
EDA means exploring the dataset or conducting a deep dive into the data, ton understand the data structure, characteristics of the data and identify issues that might need to be corrected. Above all, EDA assists in understanding the quirks and innuendos of the data.The main purpose of this activity was to asnwer the bussines questions as follows:
 1. Which are top 10 countries of the 54 in Africa had:
      - Highest COVID 19 infections vs population
      - Highest tests vs population
      - Highest positive yield vs tests conducted
      - Highest/ strictes Stringency Index
   
   
        
  3. Which are **the top 5 countries* that did well to avert the COVID 19 effects
  4. Which are the **bottom 15 countries** which did not do well  
          - having less tests vs population
          - less vaccinations and few peopple fully vaccinated
          
  5.  Which are the **top 5 countries** seriously ravaged by COVID 19 with highest death rates
         
      Highest COVID 19 death rates
      - Highest  19 vaccinations

   6. Any correlation between GDP and vaccination
   7. Any correlation between Stringency index and the total cases - in other words, did the strict rules implemented worked din countries where they were strict or they all perfomed the same just like countries that        had  relaxed regulations
   8. How bad was Africa as a whole in terms of new cases, vaccination and death rate - a graphical view would assist  
   9. What was the likelihood or chances of dying in AFrica after being infected bt COVID 19

## Data Analysis
To add some interesting codes used during the analysis and add some code chunks

## Results/ Findngs

## Recommendations

## Limitations

## References

### Definition of terms
Stringency Index  a composite measure  based on nine repsones indcators
