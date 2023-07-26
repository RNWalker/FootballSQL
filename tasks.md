# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
SELECT * FROM matches WHERE season='2017';


```

2) Find all the matches featuring Barcelona.

```sql
SELECT * FROM matches WHERE hometeam = 'Barcelona' OR awayteam ='Barcelona';


```

3) What are the names of the Scottish divisions included?

```sql
SELECT name FROM divisions WHERE country = 'Scotland';


```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql
SELECT COUNT(matches.id) AS match_count
FROM matches
INNER JOIN divisions ON matches.division_code = divisions.code
WHERE matches.awayteam = 'Freiburg' OR matches.hometeam = 'Freiburg'
AND divisions.name = 'Bundesliga';


```

5) Find the teams which include the word "City" in their name. 

```sql
SELECT DISTINCT * FROM matches WHERE awayteam LIKE('%City%') OR hometeam LIKE('%City%');


```

6) How many different teams have played in matches recorded in a French division?

```sql
SELECT COUNT(DISTINCT team_name) AS number_of_teams
FROM (
    SELECT hometeam AS team_name FROM matches
    JOIN divisions ON matches.division_code = divisions.code
    WHERE divisions.country = 'France'
    UNION
    SELECT awayteam AS team_name FROM matches
    JOIN divisions ON matches.division_code = divisions.code
    WHERE divisions.country = 'France'
) AS teams;


```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
SELECT * FROM matches 
WHERE (awayteam ='Swansea' OR awayteam='Huddersfield') AND (hometeam = 'Swansea' OR hometeam ='Huddersfield');


```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
SELECT COUNT(*)AS draw_count
FROM matches 
WHERE ftr='D' AND division_code IN(SELECT code FROM divisions WHERE name='Eredivisie')
AND season BETWEEN '2010' AND '2015';


```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. When two matches have the same total the match with more home goals should come first.

```sql
SELECT * FROM matches
INNER JOIN divisions ON matches.division_code = divisions.code
WHERE divisions.name = 'Premier League'
ORDER BY(fthg + ftag) DESC
CASE WHEN ftr = 'H' THEN 0 ELSE 1 END;


```

10) In which division and which season were the most goals scored?

```sql
<!-- Copy solution here -->


```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)