1.	Identify trends in gross reproduction rate in India over time.

   ```SQL
SELECT year, gross_reproduction_rate
FROM `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`
WHERE country_name = 'India'
ORDER BY gross_reproduction_rate, year;
```
![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/e9843117-56b4-4f35-b46f-00b175c51d2f)

2. 	Identify countries with the highest fertility rate in 2020.

   ```SQL
    SELECT country_name, SUM(total_fertility_rate) AS total_fertility_rate
    FROM `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`
    WHERE year = 2020
    GROUP BY country_name
    ORDER BY total_fertility_rate DESC
    LIMIT 10;
  ```
   ![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/5d14a203-91e4-44db-8254-8a323c5fe05a)

   3.	Identify countries with the highest crude birth rate in 2020.

   ```SQL
SELECT country_name, crude_birth_rate
FROM `bigquery-public-data.census_bureau_international.birth_death_growth_rates`
WHERE year = 2020
ORDER BY crude_birth_rate DESC
LIMIT 10;
```
![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/b26515dd-4097-4c2f-ab50-7aac2bf4ecef)

4.	Identify countries with the highest growth rate in 2021.

   ```SQL
SELECT country_name, growth_rate
FROM `bigquery-public-data.census_bureau_international.birth_death_growth_rates`
WHERE year = 2021
ORDER BY growth_rate DESC
LIMIT 10;
```
![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/b7cc548a-c7cf-4e61-92db-c7c9cc705b14)

5.	Identify countries with the highest net migration rate in 2021.

   ```SQL
SELECT country_name, net_migration
FROM `bigquery-public-data.census_bureau_international.birth_death_growth_rates`
WHERE year = 2021
ORDER BY net_migration DESC
LIMIT 10;
```
![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/83ae14a0-8cf8-434e-8146-7c853f12d4d3)

6.	Identify trends in fertility rate of 15-19 age group of India over time.

   ```SQL
SELECT fertility_rate_15_19, year
FROM `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`
WHERE country_name = 'India'
ORDER BY fertility_rate_15_19, year;
```
![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/838c2121-8b60-453a-8fc5-d72b4f572935)

7.	Find the 10 countries with largest area.

   ```SQL
SELECT country_name, country_area
FROM `bigquery-public-data.census_bureau_international.country_names_area`
ORDER BY country_area DESC
LIMIT 10;
```
![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/0449c419-86d5-480a-a03a-93c33d9d49bc)

8.	Filter countries based on a minimum area threshold.

   ```SQL
SELECT country_name, country_area
FROM `bigquery-public-data.census_bureau_international.country_names_area`
WHERE country_area > 1000000  -- Filter for countries with area greater than 1 million square kilometers
ORDER BY country_area DESC;
```
![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/4fc37381-06e1-4b2b-b2b9-d7e393ff3526)

9.	Identify countries with high fertility rates in 20-24 age group and declining population growth rates.

    ```SQL
  	SELECT `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`.country_name, SUM(fertility_rate_20_24) AS total_fertility_rate, growth_rate
    FROM `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`
    JOIN `bigquery-public-data.census_bureau_international.birth_death_growth_rates`
    ON `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`.country_name = `bigquery-public-data.census_bureau_international.birth_death_growth_rates`.country_name AND `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`.year = `bigquery-public-data.census_bureau_international.birth_death_growth_rates`.year
    WHERE `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`.year = 2020
    UP BY country_name, fertility_rate_20_24, growth_rate
    HAVING fertility_rate_20_24 > 2 AND growth_rate < 1;
    ```
    ![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/bf031a06-4e10-4cb7-b2f0-77f341fa61cc)

   10.	Analyze the relationship between fertility rates and birth rates by country.

  ```SQL 
       SELECT `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`.country_name, fertility_rate_20_24, `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`.year, crude_birth_rate
       FROM `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`
       JOIN `bigquery-public-data.census_bureau_international.birth_death_growth_rates`
       ON `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`.country_name = `bigquery-public-data.census_bureau_international.birth_death_growth_rates`.country_name AND `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`.year = `bigquery-public-data.census_bureau_international.birth_death_growth_rates`.year
       GROUP BY country_name, fertility_rate_20_24, year, crude_birth_rate
       ORDER BY country_name, fertility_rate_20_24, year;
   ```
![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/9e147d24-6291-4981-a610-25a8e144b194)

11.	 Explore the impact of population growth rate on gross reproduction rate in different countries.

   ```SQL
   	SELECT `bigquery-public-data.census_bureau_international.birth_death_growth_rates`.country_name, growth_rate, gross_reproduction_rate
    FROM `bigquery-public-data.census_bureau_international.birth_death_growth_rates`
    JOIN `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`ON `bigquery-public-data.census_bureau_international.birth_death_growth_rates`.country_name = `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`.country_name
    ORDER BY growth_rate, gross_reproduction_rate;
   ```
   ![image](https://github.com/AlkaJoy/Bigquery/assets/158851023/6dded8f0-750e-437e-a786-eecd90130083)

    


       


    












