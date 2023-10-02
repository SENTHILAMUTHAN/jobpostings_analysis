# Jobpostings_analysis
  Job postings analysis case study
## Table of Contents
- [Case study overview](#case-study-overview)
- [Data sources](#data-sources)
- [Tools](#tools)
-  [Data cleaning/Preperation](#data-cleaningpreperation)
-  [Exploratory Data Analysis(EDA)](#exploratory-data-analysiseda)
-  [Result/Findings](#resultfindings)
-  [Dashboard(images)](#dashboardimages)

## Case study overview
 This project seeks to offer in-depth insights into the current data analyst job market by analyzing recent trends and statistics. Through an examination of job listings, various work arrangements, the months with the highest hiring activity, and the leading employers, this analysis will provide valuable information that can benefit both job seekers and employers operating in the field of data analytics.
 The primary Data source used for this analysis was downloaded from the kaggle and been uploaded in this repository by the name "actualkaggledata.csv" which contains Dataset of jobpostings on Linkedin
 
## Tools
- Excel - Clean and transform the data to prepare for analysis
- SQL(BQ) - Conduct descriptive analysis to get  a better sense of the data layout and find the needful answers.
- PowerBI - Creating a overall dashboard
- tableau - Creating seperate worksheets for seeing a clear trends

## Data cleaning/Preperation
 1. Actual dataset didnt have Dates and  so it was generated by "=RANDBETWEEN()" function in excel. The dates are between 1/01/2023 to 23/09/2023.
 2. Companies having 1 employee were replaced with Random numbers  between the range of (11 - 50 ) and (100 to 150)
 3. In the industry coulumn values of "Not Available " has been replaced with  "Information Technology & Services"
 4. In the level coulumn values of "Not Available " has been replaced with "Entry level"
 5. Creating a Dataset in BQ by the name "jobanalysis" and uploaded the cleaned file to the table named "cleaned"

## Exploratory Data Analysis(EDA)
 1. EDA involves analysis of the dataset to find 
     - Last 30 days job count by company, job type, city ,state
     - Last 30 to 60 days job count by company, job type,  city ,state
     - Last 60 to 90 days job count by company, job type,  city ,state
 2. populate the table with following column_names
     - name
     - designation
     - City
     - State
     - industry
     - work_type
     - level
     - involvement
     - totaljob_postings
     - jobpostings_last30days
     - jobpostings_30to60days
     - jobpostings_60to90days
  
     


    ```
     SELECT DISTINCT name,designation,City,State,industry,work_type,level,involvement,totaljob_postings,
     jobpostings_last30days,
     (jobpostings_last60days-jobpostings_last30days)AS jobpostings_30to60days,
     (jobpostings_last90days-jobpostings_last60days)AS jobpostings_60to90days
     from (
     SELECT DISTINCT name,designation,City,State,industry,count(distinct job_ID)as totaljob_postings,
     sum(case when  date >= DATE_SUB(CURRENT_DATE(), INTERVAL 3 MONTH) then 1 else 0 end) jobpostings_last3months,
     sum(case when  date >= DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY) then 1 else 0 end) jobpostings_last30days,
     sum(case when  date >= DATE_SUB(CURRENT_DATE(), INTERVAL 60 DAY) then 1 else 0 end) jobpostings_last60days,
     sum(case when  date >= DATE_SUB(CURRENT_DATE(), INTERVAL 90 DAY) then 1 else 0 end) jobpostings_last90days,work_type,level,involvement
     FROM `project-1-trail-131997.jobanalysis.cleaned`
     --where  designation="Data Analyst"
     GROUP BY name,designation,City,State,industry,work_type,level,involvement)
     order by totaljob_postings DESC
     ```

      ![Map](https://github.com/SENTHILAMUTHAN/jobpostings_analysis/assets/138884128/61be62b7-0b64-45db-9f4c-84555296399e)

      ![Monthwise](https://github.com/SENTHILAMUTHAN/jobpostings_analysis/assets/138884128/6784d8bf-72ce-4c2d-a2f6-ac6898fb9b1c)
   
      ![30days](https://github.com/SENTHILAMUTHAN/jobpostings_analysis/assets/138884128/48bc7497-682b-47e1-9691-7009bdc8dc23)

      ![30-60days](https://github.com/SENTHILAMUTHAN/jobpostings_analysis/assets/138884128/09505ca5-79d0-4555-987c-e821c733c6a9)

      ![60-90days](https://github.com/SENTHILAMUTHAN/jobpostings_analysis/assets/138884128/7b4b9dfa-4bc0-4cac-a484-c3e0082b1545)



## Result/Findings 
1. **Most Sought-After Job Designation:** "Data analyst" is the most sought-after job designation among companies. This suggests a strong demand for professionals with skills in data analysis, which is in line with the growing importance of data-driven decision-making across various industries.

2. **Full-Time Positions:** Approximately 90% of job postings are for full-time positions. This indicates that companies are looking for dedicated and committed data analysts to join their teams, rather than relying heavily on part-time or contract workers for these roles.

3. **On-Site vs. Remote Work:** Both on-site and remote work options have a roughly equal number of job postings. This shows that the job market for data analysts is flexible in terms of work arrangements, allowing candidates to choose between working in a physical office or remotely, depending on their preferences and circumstances.

4. **Peak Activity in May:** The month of May saw the highest activity in terms of job postings and applicant numbers. This could be attributed to various factors, such as the end of the academic year for graduates, companies planning for the next fiscal year, or specific industry trends that drive hiring during that time.

5. **Top Job Poster:** "Epam Anywhere Business" posted the highest number of job postings. This suggests that this company has a significant need for data analysts or is actively expanding its data analytics team.

Overall, this information provides insights into the job market for data analysts and can be useful for job seekers looking to enter or advance in this field


## Dashboard(images)
![Dashboard](jobanalysisdashboardimage.PNG)

- Overall Job postings analysis
  ![jobanalysisdashboardimage](https://github.com/SENTHILAMUTHAN/jobpostings_analysis/assets/138884128/89eef3eb-ec99-4ddc-a198-75568964f76d)

