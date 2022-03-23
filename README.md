# data_clean1a

# Clean & Analyze Employee Exit Surveys

## Please refer to clean1b.ipynb notebook attached for python scripts and printout of data

### It is said that about 50% of a data scientist's job is spent on cleaning and transforming data.  Hence the motivation for this project. 

### Two data sets ( Department of Education, Training and Employment (DETE) and the Technical and Further Education (TAFE) institute in Queensland, Australia) are read in, cleaned, transformed, combined and then analyzed. At the end, the following questions will be answered: 1. Are employees who only worked for the institutes for a short period of time resigning due to some kind of dissatisfaction? What about employees who have been there longer?  2. Are younger employees resigning due to some kind of dissatisfaction? What about older employees?  There are 10 parts to this project.

## Part 1: Read in data files, examine data

### In this first part, we will examine the two datasets, and highlight aspects of the datasets that are problematical and in need of cleaning and/or transformation.  This first part identifies the problems in the datasets that need to be addressed, providing for a more coherent project.


### Summary of Part 1:  Both datasets have an enormous number of columns, and there does not seem to be a column the two dataframes can easily merge on.  Many columns include NaN values, other columns include 'Not Stated' as a response, which is constructively a null value.  Tafe has a length of service column, Dete does not, but it can be calculated by subtracting Dete start date from Cease date columns.  Both dataframes include reasons for leaving (i.e. separation type), cease date, employees age and gender.  Both dataframes include information on whether employee was dissatisfied, but in different forms.  Both data sets include a column showing reason for separation, but have different column names and one data set has 3 categories for a resignation while the other just one.  This analysis should highlight the need for some of the cleaning and transformation steps that will now occur

## Part 2:  Drop unwanted columns, convert 'Not Stated' entries to NaN

### Summary of Part 2:  Note the drop in the number of column numbers.  Also, the number of NaN values have increased for the 'Cease Date' and 'DETE Start Date' columns of the DETE dataset by characterizing 'Not Stated' entries as null values.  New dataframes dete_survey_updated and tafe_survey_updated are formed where unwanted columns from dete_survey and tafe_survey respectively are dropped

## Part 3:  Modify column names
### Capitalization issues, punctuation issues, and different nomenclature differ in the column names of the two datasets.  This Part 3 will address this so that the column names of the two data sets can be more consistent with each other by converting to a snake case to put them in better condition for combining and analysis

### Summary of Part 3:  Column names of both datasets were changed using different techniques so that the column names of each dataset are consistent with each other, are in snake case, and are in better condition for a subsequent combining and analysis steps

## Part 4:  Screen for 'separationtypes' that include the word 'Resignation' 
###  In this part, new dataframes 'dete_resignations' and 'tafe_resignations' are formed that only contain rows of dete_survey_updated and tafe_survey_updated respectively of where the employee separated due to a resignation (i.e. rows where separationtype column includes the word 'Resignation').  This eliminates separations that were not characterized as a resignation of some type

### Summary of Part 4: New dataframes dete_resignations and tafe_resignations were constructed containing only rows where the 'separationtype' column included the word 'Resignation'.

## Part 5:  Cleaning Cease and Start Dates
![image](https://user-images.githubusercontent.com/28972117/159764060-cce08126-3b6f-44a5-a44b-0ec008b3ca32.png)

Boxplot Distribution for 'cease_date' column of dete_resignations dataframe

![image](https://user-images.githubusercontent.com/28972117/159764270-8d456408-f026-44dd-9e60-8c7694e04875.png)

Boxplot Distribution for 'dete_start_date' column of dete_resignations dataframe

![image](https://user-images.githubusercontent.com/28972117/159764418-e21c1d28-5d00-46ff-a2f0-eb608a3b201d.png)

Boxplot Distribution for 'cease_date' column of tafe_resignations dataframe

### Summary Part 6:  It appears that the new 'institute_service' column of dete_resignations dataframe is complete and comparable with that of the 'institute_service' column in tafe_resignations.  Now these two dataframes are in better condition for being combined and analyzed

## Part 7:  Identify (and create new column) showing whether employees were dissatisfied. 
### Specifically, we want to create a new column 'dissatisfied' for each of the dete_resignations and tafe_resignations dataframes that is determined from other column entries.  This column will summarize, as a binary, whether the employee who resigned was or was not dissatsified with his or her job
### We begin with the TEFE dataset and notice it includes 2 columns ('Contributing Factors. Dissatisfaction' & 'Contributing Factors. Job Dissatisfaction') that determine whether the employee was dissatisfied


### Summary of Part 7:  New dataframes tafe_resignations_up and dete_resignations_up were created with a new column 'dissatisfied' which is derived from other columns in the corresponding datasets and has a boolean value for each row to show whether or not the employee was dissatisfied with his or her job.  Now that both dataframes have similar columns, we can now proceed to combine the data frames

## Part 8:  Combine Dataframes


### Summary of Part 8:  Datasets combined, columns weeded out, now left with just a more managable 10 columns 

## Part 9:  Clean 'institute_service' column


### Summary for Part 9:  The 'institute_service' column of the combined dataframe was cleaned to rid of text and numerical ranges, converted to a numeric data type, and then categorized to become a new column 'service_cat' in combined dataframe 'combined_updated' to prepare for data analysis

## Part 10: Analysis

![image](https://user-images.githubusercontent.com/28972117/159764588-2e8a01fd-b0c2-423f-a0f4-46b72421c441.png)

Barplot showing portion of resignees that are dissatisfied according to length of service

![image](https://user-images.githubusercontent.com/28972117/159764725-e34a098a-c69d-4829-b788-efc13a9b28f7.png)

Barplot showing portion of resignees that are dissatisfied according to employee's age

![image](https://user-images.githubusercontent.com/28972117/159764823-dd55adfb-55d8-4e13-9a3e-bec2f73fe709.png)

Barplot showing portion of resignees that are dissatisfied according to which institute the employee worked at

![image](https://user-images.githubusercontent.com/28972117/159764895-7c49a5c5-58ba-4589-8b92-c6ab3c5ac7d5.png)

Barplot showing portion of resignees that are dissatisfied according to position held

## In conclusion, it seems that years of service and which institutute the employee worked at had greatest bearing on dissatisfaction, and employee age and gender had lesser bearing on dissatisfaction

