# JOIN

1. Show the matchid and player name for all goals scored by Germany. To identify German players
```sql
SELECT matchid, player FROM goal 
  WHERE teamid = 'GER'
```

2. Show id, stadium, team1, team2 for just game 1012
```sql
SELECT id,stadium,team1,team2
  FROM game
WHERE id= 1012
```

3. Show the player, teamid, stadium and mdate for every German goal.
```sql
SELECT player, teamid, stadium, mdate
  FROM game JOIN goal ON (id=matchid)
WHERE teamid= 'GER'
```

4. Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'
```sql
SELECT team1, team2, player FROM game JOIN goal ON (id=matchid)
WHERE player LIKE 'Mario%'
```

5. Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10
```sql
SELECT player, teamid, coach, gtime
  FROM goal JOIN eteam ON (teamid= id) 
 WHERE gtime<=10
```

6. List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.
```sql
SELECT mdate, teamname FROM game JOIN eteam ON(team1 = eteam.id)
WHERE coach= 'Fernando Santos'
```

7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'
```sql
SELECT player FROM game JOIN goal ON (id= matchid)
WHERE stadium = 'National Stadium, Warsaw'
```

8. Show the name of all players who scored a goal against Germany.
List each continent and the name of the country that comes first alphabetically.
```sql
SELECT DISTINCT(player) FROM game JOIN goal ON (id= matchid)
WHERE (team1 = 'GER' or team2 = 'GER') and (teamid <> 'GER')
```

9. Show teamname and the total number of goals scored.
```sql
SELECT teamname, COUNT(player) FROM goal JOIN eteam ON (teamid= id)
GROUP BY teamname
 ```
 
10. Show the stadium and the number of goals scored in each stadium.
```sql
SELECT stadium, COUNT(player) FROM game JOIN goal ON (id= matchid)
GROUP BY stadium
```

11. For every match involving 'POL', show the matchid, date and the number of goals scored.
```sql
SELECT matchid, mdate, COUNT(mdate) FROM game JOIN goal ON (id= matchid)
WHERE team1 ='POL' or team2 = 'POL'
GROUP BY matchid, mdate
```

12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'
```sql
SELECT matchid, mdate, COUNT(player) FROM game JOIN goal ON (id = matchid)
WHERE teamid= 'GER'
GROUP BY matchid, mdate
 ```
 
13. List every match with the goals scored by each team as shown. Sort your result by mdate, matchid, team1 and team2.
```sql
SELECT mdate, 
team1, 
SUM(CASE WHEN team1 = teamid THEN 1 ELSE 0 END), 
team2, 
SUM(CASE WHEN team2 = teamid THEN 1 ELSE 0 END) 
FROM game LEFT JOIN goal ON (id=matchid)
GROUP BY mdate, matchid, team1, team2
```