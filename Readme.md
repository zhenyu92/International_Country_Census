# International Country Census Data Insights Powered by Google Data Studio
This project is a part of the learning milestone of a Udemy course delivered by [Chris Levy](https://www.udemy.com/sql-for-data-science-with-google-big-query/). 

### Author
[Derrick Chan](https://github.com/zhenyu92)

[Derrick's Linkedin](https://www.linkedin.com/in/zychan/)

### Project Status: [Completed]

### Project Objective
The study is on the dateset of public international country census. To produce a dashboard which highlights interesting data points, metrics, and visualizations from the database.

### Environment Prerequisites
`Google Big Query` on `Google Cloud Platform` for data querying 

`Google Data Studio` for data visualization

### Instruction
Database can be accessed from the Big Query public data set:
`bigquery-public-data.census_bureau_international.country_names_area`
`bigquery-public-data.census_bureau_international.midyear_population`
`bigquery-public-data.census_bureau_international.birth_death_growth_rates`
`bigquery-public-data.census_bureau_international.mortality_life_expectancy`
`bigquery-public-data.census_bureau_international.age_specific_fertility_rates`


##### Dataset Query
```
SELECT
  c.country_name,
  c.country_code,
  c.country_area,
  CAST(CONCAT(CAST(p.year AS string),'-01','-01') AS date) AS year,
  p.midyear_population AS population,
  b.crude_birth_rate,
  b.crude_death_rate,
  b.growth_rate,
  b.net_migration,
  m.infant_mortality,
  m.life_expectancy,
  f.total_fertility_rate
FROM
  `bigquery-public-data.census_bureau_international.country_names_area` c
LEFT JOIN
  `bigquery-public-data.census_bureau_international.midyear_population` p
ON
  c.country_code = p.country_code
LEFT JOIN
  `bigquery-public-data.census_bureau_international.birth_death_growth_rates` b
ON
  p.country_code = b.country_code
  AND p.year = b.year
LEFT JOIN
  `bigquery-public-data.census_bureau_international.mortality_life_expectancy` m
ON
  m.country_code = b.country_code
  AND b.year = m.year
LEFT JOIN
  `bigquery-public-data.census_bureau_international.age_specific_fertility_rates` f
ON
  f.country_code = m.country_code
  AND f.year = m.year
ORDER BY
  c.country_name,
  p.year
```

### Import & Tuning in Google Data Studio
Screenshot of the Dashboard: 
![alt text](https://github.com/zhenyu92/International_Country_Census/blob/master/International_Country_Census-1.jpg "Logo Title Text 1")
