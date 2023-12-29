# Covid 19  in Africa - analysis

## Project Overview 
COVID 19 pandemic  caused havoc and instability in the world. Even the most developed countries were not spared from its wrath. The most developed countries which had better health health standerds had  even the highest infections and death rates. Looking at the after effects of COVID 19 in countries like US and Canada as well as China, which are countries well known to have the economic and political muscles to wrestle the pandemic, it then calls for a deep dive into the less developed. It is against this background that a deep dive into COVID 19 in Africa became a neccessity of this project.

# Data Sources
A triangulation of different data sources assisted in examining the COVID 19 in Africa from different angles. Two main data sources were used as follows:  
 1. [Our World in Data for all] (https://ourworldindata.org/explorers/coronavirus-data-explorer)
 2. [Anshul Sharma from Kaggle] (https://www.kaggle.com/code/anshuls235/india-vs-covid19/input)

 # Tools
   
  1.  **Excel**  was usedas initial cleaning of data and prepare the CSV file for easy importing to My SQL workbench
  2.  **MySQL Workbench** - for further data cleaning, manipulation and analysis  
  3. **Tablea** used for visualizations and creating report
      
 ### Data Cleaning /Preparation
 1. ### Data Loading
In order to be able to load the data successfully into the Mysql workbench, a database was created and the columns in the dataset and their data types were created first. But before, the date colum data was in a wrong format (dd/mm/yyyy) and was converted to SQL data format first  as (yyyy/mm/dd). This was a solution after several unsucessful attempts. The Mysql import table wizard was utilized and data was successfullu imported into Mysql workbench.
  
2. ### Handling missing values
The dataset had lots of intention blank spaces. As in, for instance, the new cases column was recording new cases as they are reported, whenre there were no cases, the cells were blank instead of having a 0. Therefore, this was handles easily in excel by replacing all blank with 0. This successfully removed the issues of having NULL values.

3. ### Data cleaning and Formating
After importing the data, all the data types were checked and confirmed to be in the required data type.There after, Data Manipulation began - where other erequired important colums were required in order to fully satisfy the business task.

# Exploratory Data Analysis (EDA)
EDA means exploring the dataset or conducting a deep dive into the data, ton understand the data structure, characteristics of the data and identify issues that might need to be corrected. Above all, EDA assists in understanding the quirks and innuendos of the data.The main purpose of this activity was to asnwer the bussines questions as follows:
 1. Which are top 15 countries of the 54 in Africa had:
      - Highest COVID 19 infections vs population
      - Highest tests vs population
      - Highest positive yield vs tests conducted
      - Highest/ strictes Stringency Index
        
  2. Which are **the top 5 countries* that did well to avert the COVID 19 effects
  3. Which are the **bottom 15 countries** which did not do well  
          - having less tests vs population
          - less vaccinations and few peopple fully vaccinated
          
  4.  Which are the **top 5 countries** seriously ravaged by COVID 19 with highest death rates
         
      Highest COVID 19 death rates
      - Highest  19 vaccinations

   5. Any correlation between GDP and vaccination
   6. Any correlation between Stringency index and the total cases - in other words, did the strict rules implemented worked din countries where they were strict or they all perfomed the same just like countries that        had  relaxed regulations
   7. How bad was Africa as a whole in terms of new cases, vaccination and death rate - a graphical view would assist  
   9. What was the likelihood or chances of dying in AFrica after being infected bt COVID 19

##
