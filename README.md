# solutions
select from world/ sqlzoo
1.
Read the notes about this table. Observe the result of running this SQL command to show the name, continent and population of all countries.

SELECT name, continent, population FROM world
Submit SQLRestore default
result
2.
How to use WHERE to filter records. Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

SELECT name FROM world
WHERE population >= 200000000
Submit SQLRestore default
result

3.
Give the name and the per capita GDP for those countries with a population of at least 200 million.
HELP:How to calculate per capita GDP

select name,GDP/population from world
where population >= 200000000;
Submit SQLRestore default
result
4.
Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.

select name,population/1000000  from world
where continent = 'South America';
Submit SQLRestore default
result
5.
Show the name and population for France, Germany, Italy

select name, population from world
where name in ('France','Germany','Italy');
Submit SQLRestore default
result
6.
Show the countries which have a name that includes the word 'United'

select name from world 
where name like '%united%';
Submit SQLRestore default
result
7.
Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million.
Show the countries that are big by area or big by population. Show name, population and area.

select name, population, area from world
where population >= 250000000 or area >= 3000000;
Submit SQLRestore default
result
8.
Exclusive OR (XOR). Show the countries that are big by area or big by population but not both. Show name, population and area.
Australia has a big area but a small population, it should be included.
Indonesia has a big population but a small area, it should be included.
China has a big population and big area, it should be excluded.
United Kingdom has a small population and a small area, it should be excluded.

select name, population, area from world
where population >= 250000000 xor area >= 3000000;
Submit SQLRestore default
result
9.
Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.
For South America show population in millions and GDP in billions both to 2 decimal places.
Millions and billions

select name, Round(population/1000000,2) , Round(GDP/1000000000,2) from world
where continent = 'south america';
Submit SQLRestore default
result
10.
Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.
Show per-capita GDP for the trillion dollar countries to the nearest $1000.

select name, Round(GDP/population,-3) from world
where GDP > 1000000000000;
Submit SQLRestore default
result
Harder Questions
11.
The CASE statement shown is used to substitute North America for Caribbean in the third column.
Show the name - but substitute Australasia for Oceania - for countries beginning with N.

SELECT name,
       CASE WHEN continent='Oceania' THEN 'Australasia'
            ELSE continent END
From world
 WHERE name LIKE 'N%'

Submit SQLRestore default
result
12.
Show the name and the continent - but substitute Eurasia for Europe and Asia; substitute America - for each country in North America or South America or Caribbean. Show countries beginning with A or B

SELECT name, CASE 
WHEN continent IN ('Europe', 'Asia') THEN 'Eurasia'
WHEN continent IN ('North America', 'South America', 'Caribbean') THEN 'America'
ELSE continent END
FROM world
WHERE name LIKE 'A%' OR name LIKE 'B%';
Submit SQLRestore default
result
13.
Put the continents right...
Oceania becomes Australasia
Countries in Eurasia and Turkey go to Europe/Asia
Caribbean islands starting with 'B' go to North America, other Caribbean islands go to South America
Order by country name in ascending order
Test your query using the WHERE clause with the following:
WHERE tld IN ('.ag','.ba','.bb','.ca','.cn','.nz','.ru','.tr','.uk')
Show the name, the original continent and the new continent of all countries.

SELECT name, continent,
CASE WHEN continent = 'Oceania' THEN 'Australasia'
WHEN continent = 'Eurasia' OR name = 'Turkey' THEN 'Europe/Asia'
WHEN continent = 'Caribbean' AND name LIKE 'b%' THEN 'North America'
WHEN continent = 'Caribbean' AND name NOT LIKE 'b%' THEN 'South America'
ELSE continent END
FROM world
WHERE tld IN ('.ag','.ba','.bb','.ca','.cn','.nz','.ru','.tr','.uk')
ORDER BY name
Submit SQL
