Q1. Find the titles of all movies directed by Steven Spielberg.  

```sql
select mID, title
   ...> from Movie
   ...> where director = 'Steven Spielberg';
```
![[Pasted image 20251202121659.png]]

Q2. Find all years that have a movie that received a rating of 4 or 5, and 
sort them in increasing order.  

```sql
select DISTINCT m.year
   ...> from Movie m
   ...> JOIN Rating r ON r.mID = m.mID
   ...> where r.stars IN (4, 5)
   ...> order by m.year;
```

![[Pasted image 20251202122327.png|100]]

Q3. Find the titles of all movies that have no ratings.  

```sql
select title
   ...> from Movie
   ...> where mID not in (
   ...>   select mID
   ...>   from Rating
   ...> );
```

![[Pasted image 20251202123035.png]]

Q4. Some reviewers didn't provide a date with their rating. Find the names of all reviewers who have ratings with a NULL value for the date.  

```sql
select re.name
   ...> from Reviewer re
   ...> join Rating r on re.rID = r.rID
   ...> where r.ratingDate is null;
```

![[Pasted image 20251202123419.png]]

Q5. Write a query to return the ratings data in a more readable format: reviewer name, movie title, stars, and ratingDate. Also, sort the data, first by reviewer name, then by movie title, and lastly by number of stars. 

```sql
select re.name, m.title, r.stars, r.ratingDate
   ...> from Rating r
   ...> join Movie m on m.mID = r.mID
   ...> join Reviewer re on re.rID = r.rID
   ...> order by re.name, m.title, r.stars;
```

![[Pasted image 20251202123910.png]]

Q6. For all cases where the same reviewer rated the same movie twice and gave it a higher rating the second time, return the reviewer's name and the title of the movie.  

```sql
select re.name, m.title
   ...> from Rating r1
   ...> join Rating r2 on
   ...>   r1.mID = r2.mID
   ...>   and r1.rID = r2.rID
   ...>   and r1.ratingDate < r2.ratingDate
   ...>   and r1.stars < r2.stars
   ...> join Reviewer re
   ...>   on r1.rID = re.rID
   ...> join Movie m
   ...>   on r1.mID = m.mID;
```

![[Pasted image 20251202125124.png|200]]

Q7. For each movie that has at least one rating, find the highest number of stars that movie received. Return the movie title and number of stars. Sort by movie title.  

```sql
 select  m.title, MAX(r.stars)
   ...> from Movie m
   ...> join Rating r on r.mID = m.mID
   ...> group by m.mID
   ...> order by m.title;
```

![[Pasted image 20251202165819.png|200]]

Q8. For each movie, return the title and the 'rating spread', that is, the difference between highest and lowest ratings given to that movie. Sort by rating spread from highest to lowest, then by movie title.  

```sql
select m.title, (MAX(r.stars) - MIN(r.stars)) as Rating_Spread
   ...> from Movie m
   ...> join Rating r on m.mID = r.mID
   ...> group by m.mID
   ...> order by Rating_Spread DESC, m.title;
```
![[Pasted image 20251202175837.png]]

Q9. Find the difference between the average rating of movies released before 1980 and the average rating of movies released after 1980. (Make sure to calculate the average rating for each movie, then the average of those averages for movies before 1980 and movies after. Don't just calculate the overall average rating before and after 1980.)  

![[Pasted image 20251202195711.png|400]]



Q10. Find the names of all reviewers who rated Gone with the Wind.  

```sql
select re.name
   ...> from Rating r
   ...> join Reviewer re on r.rID = re.rID
   ...> join Movie m on m.mID = r.mID
   ...> where m.title = 'Gone with the Wind';
```

![[Pasted image 20251202182739.png]]

Q11. For any rating where the reviewer is the same as the director of the movie, return the reviewer name, movie title, and number of stars.  

```sql
select re.name, m.title, r.stars
   ...> from Rating r
   ...> join Reviewer re on r.rID = re.rID
   ...> join Movie m on m.mID = r.mID
   ...> where re.name = m.director;
```
![[Pasted image 20251202183209.png|200]]

Q12. Return all reviewer names and movie names together in a single list, alphabetized. (Sorting by the first name of the reviewer and first word in the title is fine; no need for special processing on last names or removing "The".)  

```sql
select name as combined_name
   ...> from Reviewer
   ...> UNION
   ...> select title as combined_name
   ...> from Movie
   ...> order by combined_name;
```
![[Pasted image 20251202183738.png|200]]\
Q13. Find the titles of all movies not reviewed by Chris Jackson.

```sql
 select title
   ...> from Movie
   ...> where mID NOT IN (
   ...>   select r.mID
   ...>   from Rating r
   ...>   join Reviewer re on r.rID = re.rID
   ...>   where re.name = 'Chris Jackson'
   ...> );
```
or
![[Pasted image 20251202195837.png|300]]

![[Pasted image 20251202184522.png]]

Q14. For all pairs of reviewers such that both reviewers gave a rating to the same movie, return the names of both reviewers. Eliminate duplicates, don't pair reviewers with themselves, and include each pair only once. For each pair, return the names in the pair in alphabetical order.  

```sql
select distinct
   ...>   re1.name as reviewer1,
   ...>   re2.name as reviewer2
   ...> from Rating r1
   ...> join Rating r2
   ...>   on r1.mID = r2.mID
   ...>   and r1.rID < r2.rID
   ...> join Reviewer re1 on r1.rID = re1.rID
   ...> join Reviewer re2 on r2.rID = re2.rID
   ...> order by reviewer1, reviewer2;
```

![[Pasted image 20251202193615.png]]


Q15. For each rating that is the lowest (fewest stars) currently in the database, return the reviewer name, movie title, and number of stars.  

```sql
select re.name, m.title, r.stars
   ...> from Rating r
   ...> join Reviewer re on r.rID = re.rID
   ...> join Movie m on m.mID = r.mID
   ...> where r.stars = (
   ...>   select MIN(r1.stars)
   ...>   from Rating r1
   ...> );
```

![[Pasted image 20251202194131.png|300]]


Q16. List movie titles and average ratings, from highest-rated to lowest-rated. If two or more movies have the same average rating, list them in alphabetical order.  

```sql
select m.title, AVG(r.stars) as avg_rating
   ...> from Rating r
   ...> inner join Movie m
   ...>   on r.mID = m.mID
   ...> group by m.title
   ...> order by avg_rating, m.title;
```
![[Pasted image 20251202200125.png|300]]

Q17. Find the names of all reviewers who have contributed three or more ratings.  

```sql
select re.name
   ...> from Rating r
   ...> inner join Reviewer re
   ...>   on r.rID = re.rID
   ...> group by re.rID
   ...> having COUNT(*) > 2;
```

![[Pasted image 20251202200823.png]]


Q18. Some directors directed more than one movie. For all such directors, return the titles of all movies directed by them, along with the director name. Sort by director name, then movie title.  

```sql
select m.title, m.director
   ...> from Movie m
   ...> where m.director IN (
   ...>   select director
   ...>   from Movie
   ...>   where director is not NULL
   ...>   group by director
   ...>   having count(*) > 1
   ...> )
   ...> order by m.director, m.title;
```
![[Pasted image 20251202201715.png]]

Q19. Find the movie(s) with the highest average rating. Return the movie title(s) and average rating.  

```sql
select m.title, AVG(r.stars) as avg_rating
   ...> from Rating r
   ...> join Movie m
   ...>   on m.mID = r.mID
   ...> group by m.mID, m.title
   ...> having avg_rating = (
   ...>   select MAX(movie_avg)
   ...>   from (
   ...>     select AVG(stars) as movie_avg
   ...>     from Rating
   ...>     group by mID
   ...>   )
   ...> );
```
![[Pasted image 20251202205325.png]]


Q20. For each director, return the director's name together with the title(s) of the movie(s) they directed that received the highest rating among all of their movies, and the value of that rating. Ignore movies whose director is NULL.

```sql
select m.director, m.title, MAX(r.stars) as highest_rating
   ...> from Movie m
   ...> inner join Rating r on m.mID = r.mID
   ...> where m.director is not null
   ...> group by m.director, m.mID, m.title
   ...> having highest_rating = (
   ...>   select MAX(r2.stars)
   ...>   from Rating r2
   ...>   inner join Movie m2
   ...>     on r2.mID = m2.mID
   ...>   where m2.director = m.director
   ...> );
```

![[Pasted image 20251202210616.png]]

