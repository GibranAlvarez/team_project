# Team Project

## Description
The team project consists of two modules. Each module requires participants to apply the skills they have learned to date, and explore a dataset of their choosing. The first part of the team project involves creating a simple program with a database in order to analyze a dataset from an open source, such as Kaggle. In the second part of the team project, teams will come together again and apply the skills developed in each of the data science or machine learning foundations certificate streams. Teams will either create a data visualization or a machine learning model.

Participants will work in assigned teams of 4-5. 

#### Project Descriptions

* [First Team Project Description](./team_project_1.md)
* [Second Team Project Description](./team_project_2.md)

## Learning Outcomes
By the end of Team Project Module 1, participants will be able to:
* Resolve merge conflicts
* Describe common problems or challenges a team encounters when working collaboratively using Git and GitHub
* Create a program to analyze a dataset with contributions from multiple team members

By the end of Team Project Module 2, participants will be able to:
* Create a data visualization as a team
* Create a machine learning model as a team

### Contacts
**Questions can be submitted to the _#cohort-3-help_ channel on Slack**

* Technical Facilitator: 
  * **Phil Van-Lane**(he/him)
  phil.vanlane@mail.utoronto.ca

* Learning Support Staff:
  * **Taneea Agrawaal** (she/her)
  taneea@cs.toronto.edu
  * **Farzaneh Hashemi** (she/her )
  fhashemi.ma@gmail.com
  * **Tong Su** (she/her)
  tong.su@mail.utoronto.ca

### Delivery of Team Project Modules

Each Team Project module will include two live learning sessions and one case study presentation. During live learning sessions, facilitators will introduce the project, walk through relevant examples, and introduce various team skills that support project success. The remaining time will be used for teams to assemble and work on their projects, as well as get help from the facilitator or the learning support to troubleshoot any issues a team may be encountering. 

Work periods will also be used as opportunities for teams to collaborate and work together, while accessing learning support. 

### Schedule

|Day 1|Day 2|Day 3|Day 4|Day 5|
|-----|-----|-----|-----|-----|
|Live Learning Session |Live Learning Session|Case Study|Work Period|Work Period|

## Requirements
* Participants are expected to attend live learning sessions and the case study as part of the learning experience. Participants are encouraged to use the scheduled work period time to complete their projects.
* Participants are encouraged to ask questions and collaborate with others to enhance learning.
* Participants must have a computer and an internet connection to participate in online activities.
* Participants must not use generative AI such as ChatGPT to generate code to complete assignments. It should be used as a supportive tool to seek out answers to questions you may have.
* We expect participants to have completed the [onboarding repo](https://github.com/UofT-DSI/onboarding/tree/main/onboarding_documents).
* We encourage participants to default to having their camera on at all times, and turning the camera off only as needed. This will greatly enhance the learning experience for all participants and provides real-time feedback for the instructional team. 

### How to get help
![image](/steps-to-ask-for-help.png)

## Folder Structure

### Project 1
```markdown
|-- data
|---- processed
|---- raw
|---- sql
|-- reports
|-- src
|-- README.md
|-- .gitignore
```

### Project 2
```markdown
|-- data
|---- processed
|---- raw
|---- sql
|-- experiments
|-- models
|-- reports
|-- src
|-- README.md
|-- .gitignore
```

* **Data:** Contains the raw, processed and final data. For any data living in a database, make sure to export the tables out into the `sql` folder, so it can be used by anyone else.
* **Experiments:** A folder for experiments
* **Models:** A folder containing trained models or model predictions
* **Reports:** Generated HTML, PDF etc. of your report
* **src:** Project source code
* README: This file!
* .gitignore: Files to exclude from this folder, specified by the Technical Facilitator









After meeting with the team members, we decided to study a subject related to immigration and cost of rent. Other team member worked on getting
a very detailed housing and rent data set. For me, after reading some articles, I discovered that the subject of "EMMIGRANTS" is not much investigated.

The final decision about studying  (IMMIGRANTS or EMMIGRANTS or RETURNING EMMIGRANTS) DEPENDING ON other factors including HOUSING is still pending but all the data is now ready. The decision will be taken soon depending on some more litterature review.

The government of Canada promotes immigration as source of economic stability. However, although each year new permanent residents arrive
to Canada, there are people leaving the country. In this study, I am trying to figure out if some internal reasons are pushing people to
leave the country (EMMIGRANTS). Morever, I will investigate if these reasons (or factors) are pushing some people (RETURNING EMMIGRANTS) to come back to Canada.

So from Statistics Canada, I dowloaded the following data:

1) number of emmigrants, quarterly, from 1976 to 2022.
2) number of returning emmigrants, quarterly, from 1976 to 2022.
3) number of incidents (violations of law, crimes, etc..), yearly, from 1998 to 2022.
4) the measure of core inflation based on a weighted median approach, monthly, from 1990 to 2022.
5) the median income of individuals, yearly, from 1976 to 2022.
6) the unemployement rate of persons over 15, yearly, from 1990 to 2022.

The data was organized in excel and than imported (in total of 6 tables) to DB browser. Then, I used some of what I have learned from the SQL
course to create new tables, join some tables on the column year, find the years for which the number of emmigrants and RETURNING EMMIGRANTS are maximum 
and minimum and many other queries..

The next step would be to study the relation between the depedent variables (EMMIGRANTS or RETURNING EMMIGRANTS) and the independent
variables (incidents, inflation, income and unemployement, and at this step, WE COULD ADD THE DATA ABOUT THE HOUSING).

The SQL queries could be find below:











DROP TABLE IF EXISTS total_returning_emmigrants_table_temp;

CREATE TEMP TABLE total_returning_emmigrants_table_temp AS
SELECT year, SUM(number) AS total_returning_emmigrants_per_year
FROM returning_emmigrants
GROUP BY year;

DROP TABLE IF EXISTS total_returning_emmigrants_table;

CREATE TABLE total_returning_emmigrants_table AS 
SELECT *
FROM total_returning_emmigrants_table_temp;

DROP TABLE IF EXISTS total_emmigrants_table_temp;

CREATE TEMP TABLE total_emmigrants_table_temp AS
SELECT year, SUM(number) AS total_emmigrants_per_year
FROM emmigrants
GROUP BY year;

DROP TABLE IF EXISTS total_emmigrants_table;

CREATE TABLE total_emmigrants_table AS 
SELECT *
FROM total_emmigrants_table_temp;

--SELECT year, max(total_emmigrants_per_year) 
--FROM total_emmigrants_table
--SELECT year, min(total_emmigrants_per_year) 
--FROM total_emmigrants_table
--SELECT year, max(total_returning_emmigrants_per_year) 
--FROM total_returning_emmigrants_table
--SELECT year, min(total_returning_emmigrants_per_year) 
--FROM total_returning_emmigrants_table
--SELECT  avg(total_emmigrants_per_year) 
--FROM total_emmigrants_table
--SELECT avg(total_returning_emmigrants_per_year) 
--FROM total_returning_emmigrants_table




DROP TABLE IF EXISTS inflation_temp_result;
CREATE TEMP TABLE inflation_temp_result AS
  SELECT year, AVG(cpi_change) AS average_cpi_per_year
  FROM inflation
  GROUP BY year;

DROP TABLE IF EXISTS inflation_per_year;  
CREATE TABLE inflation_per_year AS
SELECT *
FROM inflation_temp_result;


--SELECT *
--FROM inflation_per_year

--SELECT tri.year, total_returning_emmigrants_per_year,average_cpi_per_year,income, rate
--FROM total_returning_emmigrants_table AS tri
--INNER JOIN incidents AS i
 -- ON tri.year = i.year
--INNER JOIN inflation_per_year AS ipy
 -- ON tri.year = ipy.year
--INNER JOIN median_income AS mi
 -- ON tri.year = mi.year
--INNER JOIN unemployement_over15 AS u
 -- ON tri.year = u.year;

DROP TABLE IF EXISTS new_result_1;
CREATE TEMP TABLE new_result_1 AS 
SELECT te.year, total_emmigrants_per_year,average_cpi_per_year,income as median_income, rate as unemployement_rate
FROM total_emmigrants_table AS te
INNER JOIN incidents AS i
ON te.year = i.year
INNER JOIN inflation_per_year AS ipy
ON te.year = ipy.year
INNER JOIN median_income AS mi
ON te.year = mi.year
INNER JOIN unemployement_over15 AS u
ON te.year = u.year;

DROP TABLE IF EXISTS emmigrants_with_factors_per_year_table;
CREATE TABLE emmigrants_with_factors_per_year_table AS
SELECT *
FROM new_result_1;


--SELECT year as year_where_max_emmigrants
--FROM total_emmigrants_table
--WHERE total_emmigrants_per_year= (SELECT MAX(total_emmigrants_per_year) FROM total_emmigrants_table)
--SELECT year as year_where_max_incidents
--FROM incidents
--WHERE number= (SELECT MAX(number) FROM incidents)
--SELECT year as year_where_max_inflation
--FROM inflation_per_year
--WHERE average_cpi_per_year= (SELECT MAX(average_cpi_per_year) FROM inflation_per_year)
--SELECT year as year_where_min_income
--FROM median_income
--WHERE income= (SELECT MIN(income) FROM median_income)
--SELECT year as year_where_max_unemployement
--FROM unemployement_over15
--WHERE rate= (SELECT MAX(rate) FROM unemployement_over15)

--SELECT year as year_where_max_returning_emmigrants
--FROM total_returning_emmigrants_table
--WHERE total_returning_emmigrants_per_year= (SELECT MAX(total_returning_emmigrants_per_year) FROM total_returning_emmigrants_table)
--SELECT year as year_where_min_incidents
--FROM incidents
--WHERE number= (SELECT MIN(number) FROM incidents)
--SELECT year as year_where_min_inflation
--FROM inflation_per_year
--WHERE average_cpi_per_year= (SELECT MIN(average_cpi_per_year) FROM inflation_per_year)
--SELECT year as year_where_max_income
--FROM median_income
--WHERE income= (SELECT MAX(income) FROM median_income)
--SELECT year as year_where_min_unemployement
--FROM unemployement_over15
--WHERE rate= (SELECT min(rate) FROM unemployement_over15)



