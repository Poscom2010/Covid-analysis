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
  
