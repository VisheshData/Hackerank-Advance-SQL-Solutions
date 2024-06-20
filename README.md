# Hackerank-Advance-SQL-Solutions
Solutions to Hackerank Advanced SQL questions

## SQL Project Planning question
link- https://www.hackerrank.com/challenges/sql-projects/problem

My solution:

```sql
With Project_Start_Date as(
SELECT
            Start_Date,
            ROW_NUMBER() OVER (ORDER BY Start_Date) as Rank_Start
    FROM    Projects
    WHERE   Start_Date NOT IN(SELECT End_Date FROM Projects)

),

Project_End_Date as (
    SELECT
        End_Date,
        ROW_NUMBER() OVER (ORDER BY End_Date) as Rank_End
FROM    Projects
WHERE   End_Date NOT IN(SELECT Start_Date FROM Projects)
)

SELECT
        s.Start_Date,
        e.End_Date
FROM    Project_Start_Date s
inner join Project_End_Date e on e.rank_end=s.rank_start 

ORDER BY 
DATEDIFF(day,Start_Date,End_Date),
Start_Date
