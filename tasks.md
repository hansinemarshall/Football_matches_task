# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
<!-- SELECT COUNT(*) FROM matches WHERE season = 2017;
-- count = 7810


```

2) Find all the matches featuring Barcelona.

```sql
<!-- SELECT * FROM matches WHERE hometeam LIKE 'Barcelona' OR awayteam LIKE 'Barcelona';
-- returns 608 rows 


```

3) What are the names of the Scottish divisions included?

```sql
<!-- SELECT * FROM divisions WHERE country LIKE 'Scotland';
-- returns Scottish Premiership, Scottish Championship, Scottish League One  


```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql
<!-- SELECT code FROM divisions WHERE name LIKE 'Bundesliga'
-- returns D1 
-- SELECT COUNT(*) FROM matches WHERE division_code = 'D1' AND (hometeam LIKE 'Freiburg' OR awayteam LIKE 'Freiburg');
-- returns 374


```

5) Find the teams which include the word "City" in their name. 

```sql
<!-- SELECT DISTINCT hometeam FROM matches WHERE hometeam LIKE '%City%' UNION SELECT DISTINCT awayteam FROM matches WHERE awayteam LIKE '%City%';  
-- returns bath, man, edinburgh, bristol


```

6) How many different teams have played in matches recorded in a French division?

```sql
<!-- SELECT code FROM divisions WHERE country LIKE 'France';
-- returns F1 and F2
-- SELECT COUNT(DISTINCT hometeam) FROM matches WHERE division_code = 'F1' OR division_code ='F2' UNION SELECT COUNT(DISTINCT awayteam) FROM matches WHERE division_code = 'F1' OR division_code ='F2';
-- returns 61

```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
<!-- SELECT COUNT(*) FROM matches WHERE (hometeam = 'Huddersfield' OR hometeam = 'Swansea') AND (awayteam = 'Huddersfield' OR awayteam = 'Swansea');
-- returns 12 (number of times the teams have played each other)


```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
<!-- SELECT code FROM divisions WHERE name = 'Eredivisie';
-- returns N1
--SELECT COUNT(*) FROM matches WHERE division_code = 'N1' AND ftr = 'D' AND (season BETWEEN 2010 AND 2015);
-- returns 431


```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. When two matches have the same total the match with more home goals should come first.

```sql
<!-- SELECT code FROM divisions WHERE name = 'Premier League';
-- returns E0

-- SELECT hometeam, awayteam, fthg, ftag, ftr FROM matches WHERE division_code = 'E0' ORDER BY (fthg + ftag) DESC, fthg DESC ;
-- returns all matches in premier league sorted by total goals scores (fthg + ftag) and then by  goals scored by home team in descending oder (unsure how to order between fthg and ftag within these total score groups e.g. 3-6 comes before 0-9)


```

10) In which division and which season were the most goals scored?

```sql
<!-- SELECT SUM(fthg + ftag), division_code, season FROM matches GROUP BY division_code, season ORDER BY SUM(fthg + ftag) DESC LIMIT 1;
-- returns 1 row: | sum (total goals scored) = 1592 | division_code EC | season 2013
-- SELECT * FROM divisions WHERE code = 'EC';
-- returns National League, England 
-- 1592 goals were score in National League of England in 2013 season


```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)