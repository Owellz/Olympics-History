# Olympics-History
Mention the total no of nations who participated in each olympics game?
SELECT noc, COUNT(DISTINCT Year) AS total_participation
FROM employer.athlete_eventss
GROUP BY noc
ORDER BY total_participation desc;

Which year saw the highest and lowest no of countries participating in olympics?
SELECT year, COUNT(DISTINCT noc) as num_participating_nations
FROM employer.athlete_eventss
GROUP BY year
ORDER BY num_participating_nations DESC
LIMIT 1;

SELECT year, COUNT(DISTINCT noc) as num_participating_nations
FROM employer.athlete_eventss
GROUP BY year
ORDER BY num_participating_nations ASC
LIMIT 1;



Which nation has participated in all of the olympic games?
SELECT noc, COUNT(DISTINCT Year) AS total_participation
FROM employer.athlete_eventss
GROUP BY noc
ORDER BY total_participation desc;


Identify the sport which was played in all summer olympics.

SELECT DISTINCT sport, season FROM employer.athlete_eventss
WHERE season = 'summer'
GROUP BY sport;

Which Sports were just played only once in the olympics?
SELECT sport, COUNT(*) FROM employer.athlete_eventss
GROUP BY sport 
HAVING COUNT(*) =1;

Fetch the total no of sports played in each olympic games.
SELECT sport, COUNT(*) FROM employer.athlete_eventss
GROUP BY sport 
HAVING COUNT(*);


Fetch details of the oldest athletes to win a gold medal.
SELECT name, sex, height, weight, noc, games, year, season, city, sport, event, age, medal 
FROM employer.athlete_eventss
HAVING age BETWEEN 20 AND 50
AND medal = 'gold'
ORDER BY age DESC
LIMIT 5;


Find the Ratio of male and female athletes participated in all olympic games.
SELECT
    SUM(CASE WHEN Sex = 'M' THEN 1 ELSE 0 END) AS Male_Count,
    SUM(CASE WHEN Sex = 'F' THEN 1 ELSE 0 END) AS Female_Count,
    SUM(CASE WHEN Sex = 'M' THEN 1 ELSE 0 END) / 
SUM(CASE WHEN Sex = 'F' THEN 1 ELSE 0 END) AS Male_Female_Ratio
FROM
    employer.athlete_eventss
WHERE
    Games IS NOT NULL;

Fetch the top 5 athletes who have won the most gold medals.
SELECT name, COUNT(medal) AS  Gold_Medals 
FROM employer.athlete_eventss
WHERE Medal = 'Gold'
GROUP BY name
ORDER BY Gold_medals DESC
LIMIT 5;

Fetch the top 5 athletes who have won the most medals (gold/silver/bronze).
SELECT name, COUNT(*) AS  Most_Medals 
FROM employer.athlete_eventss
GROUP BY Name
ORDER BY Most_medals DESC
LIMIT 5;

Fetch the top 5 most successful countries in olympics. Success is defined by no of medals won.
This query will group all the medals by the name of the athlete using the GROUP
 BY clause. The COUNT(*)
 function will count the total number of medals won by each athlete, regardless of their type. The ORDER BY clause will sort the results in descending order based on the number of total medals, and the LIMIT clause will limit the output to the top 5 athletes.
SELECT NOC, COUNT(*) AS  Most_Successful_by_medals 
FROM employer.athlete_eventss
GROUP BY noc
ORDER BY Most_Successful_by_medals DESC
LIMIT 5;

List down total gold, silver and broze medals won by each country.
This query uses the SUM function with CASE statements to count the number of gold, silver, 
and bronze medals won by each country. 
The CASE statements check the value of the Medal_Type column and return a 1 if the medal is of the specified type, or a 0 otherwise. 
The SUM function then adds up all the 1s and 0s for each country to give the total number of medals of each type won by that country. The GROUP BY clause groups the results by the Country column, so that the totals are calculated for each country
SELECT 
NOC,
SUM(CASE WHEN medal = 'Gold' THEN 1 ELSE 0 END) AS Gold_meda,
SUM(CASE WHEN medal = 'Silver' THEN 1 ELSE 0 END) AS Silver_meda,
SUM(CASE WHEN medal = 'Bronze' THEN 1 ELSE 0 END) AS Bronze_meda
FROM employer.athlete_eventss
GROUP BY NOC;


Identify which country won the most gold, most silver and most bronze medals in each olympic games.
Identify which country won the most gold, most silver, most bronze medals and the most medals in each olympic games.
SELECT NOC,
SUM(CASE WHEN medal = 'Gold' THEN 1 ELSE 0 END) AS Gold_meda,
SUM(CASE WHEN medal = 'Silver' THEN 1 ELSE 0 END) AS Silver_meda,
SUM(CASE WHEN medal = 'Bronze' THEN 1 ELSE 0 END) AS Bronze_meda
FROM employer.athlete_eventss
GROUP BY noc
ORDER BY noc DESC;
