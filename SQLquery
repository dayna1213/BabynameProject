-- Classifying first_names as 'Classic', 'Semi-classic', 'Semi-trendy', or 'Trendy'
SELECT first_name, sum(num),
    CASE WHEN count(year) > 80 THEN 'Classic'
         WHEN count(year) > 50 THEN 'Semi-Classic'
         WHEN count(year) > 20 THEN 'Semi-Trendy'
         ELSE 'Trendy' END AS popularity_type
FROM baby_names
GROUP BY first_name
ORDER BY first_name;

-- Top-ranked female names since 1920
SELECT RANK() OVER(ORDER BY SUM(num) DESC) AS name_rank,
    first_name, SUM(num)
FROM baby_names
WHERE sex = 'F'
GROUP BY first_name 
LIMIT 10;


-- Top-ranked female name ending with ‘a’ since 2015
SELECT first_name
FROM baby_names
WHERE sex = 'F' and year > 2015 
    and first_name LIKE '%a'
GROUP BY first_name
ORDER BY sum(num) DESC;


-- when did the previous result became famous
SELECT year, first_name, num,
    sum(num) OVER(ORDER BY year) as cumulative_olivias
FROM baby_names
WHERE first_name LIKE 'Olivia'
ORDER BY year;

-- Top male names over the years 
SELECT b.year, b.first_name, b.num
FROM baby_names AS b
INNER JOIN (
    SELECT year, MAX(num) as max_num
    FROM baby_names
    WHERE sex = 'M'
    GROUP BY year) AS subquery 
ON subquery.year = b.year 
    AND subquery.max_num = b.num
ORDER BY year DESC;

-- Top male name that has been #1 for the largest number of years 
WITH top_male_names AS (
    SELECT b.year, b.first_name, b.num
    FROM baby_names AS b
    INNER JOIN (
        SELECT year, MAX(num) num
        FROM baby_names
        WHERE sex = 'M'
        GROUP BY year) AS subquery 
    ON subquery.year = b.year 
        AND subquery.num = b.num
    ORDER BY YEAR DESC
    )
SELECT first_name, COUNT(first_name) as count_top_name
FROM top_male_names
GROUP BY first_name
ORDER BY COUNT(first_name) DESC;
