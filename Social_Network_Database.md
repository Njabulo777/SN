Social Network Database
================
Njabulo
2023-01-14

**These are some of the the questions that I answered in the Relational
Databases Course offered by Stanford University on Edx. The course had a
database that was queried in the rubric. I decided to create the same
database in my local instance of MySQL and query it locally using
Rmarkdown. The details of the database and the schema are as described
below:**

*Students at your hometown high school have decided to organize their
social network using databases. So far, they have collected information
about sixteen students in four grades, 9-12. Here’s the schema:*

**Highschooler ( ID, name, grade )** *There is a high school student
with unique ID and a given first name in a certain grade.*

**Friend ( ID1, ID2 )** *The student with ID1 is friends with the
student with ID2. Friendship is mutual, so if (123, 456) is in the
Friend table, so is (456, 123).*

**Likes ( ID1, ID2 )** *The student with ID1 likes the student with ID2.
Liking someone is not necessarily mutual, so if (123, 456) is in the
Likes table, there is no guarantee that (456, 123) is also present.*

``` r
library(odbc)
library(RMySQL)
library(ggeasy)
library(tinytex)
library(latexpdf)
library(kableExtra)
library(dplyr)
```

Here is the list of tables in the database I created and named **sn**

``` r
dbListTables(con)
```

    ## [1] "friend"       "highschooler" "likes"

**This query gets all the columns of the highschooler table and saves it
in an R dataframe called by the same name.**

``` sql

SELECT*
FROM highschooler;
```

**The highschooler table is shown below as a dataframe**

``` r
highschooler %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:right;">
ID
</th>
<th style="text-align:left;">
name
</th>
<th style="text-align:right;">
grade
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
1025
</td>
<td style="text-align:left;">
John
</td>
<td style="text-align:right;">
12
</td>
</tr>
<tr>
<td style="text-align:right;">
1101
</td>
<td style="text-align:left;">
Haley
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:right;">
1247
</td>
<td style="text-align:left;">
Alexis
</td>
<td style="text-align:right;">
11
</td>
</tr>
<tr>
<td style="text-align:right;">
1304
</td>
<td style="text-align:left;">
Jordan
</td>
<td style="text-align:right;">
12
</td>
</tr>
<tr>
<td style="text-align:right;">
1316
</td>
<td style="text-align:left;">
Austin
</td>
<td style="text-align:right;">
11
</td>
</tr>
<tr>
<td style="text-align:right;">
1381
</td>
<td style="text-align:left;">
Tiffany
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:right;">
1468
</td>
<td style="text-align:left;">
Kris
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:right;">
1501
</td>
<td style="text-align:left;">
Jessica
</td>
<td style="text-align:right;">
11
</td>
</tr>
<tr>
<td style="text-align:right;">
1510
</td>
<td style="text-align:left;">
Jordan
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:right;">
1641
</td>
<td style="text-align:left;">
Brittany
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:right;">
1661
</td>
<td style="text-align:left;">
Logan
</td>
<td style="text-align:right;">
12
</td>
</tr>
<tr>
<td style="text-align:right;">
1689
</td>
<td style="text-align:left;">
Gabriel
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:right;">
1709
</td>
<td style="text-align:left;">
Cassandra
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:right;">
1782
</td>
<td style="text-align:left;">
Andrew
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:right;">
1911
</td>
<td style="text-align:left;">
Gabriel
</td>
<td style="text-align:right;">
11
</td>
</tr>
<tr>
<td style="text-align:right;">
1934
</td>
<td style="text-align:left;">
Kyle
</td>
<td style="text-align:right;">
12
</td>
</tr>
</tbody>
</table>

**The following query get all the columns from the friend table and
saves it as a dataframe called by the same name.**

``` sql
SELECT*
FROM friend
```

**This is what the friend table looks like.**

``` r
friend %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:right;">
ID1
</th>
<th style="text-align:right;">
ID2
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
1510
</td>
<td style="text-align:right;">
1381
</td>
</tr>
<tr>
<td style="text-align:right;">
1510
</td>
<td style="text-align:right;">
1689
</td>
</tr>
<tr>
<td style="text-align:right;">
1689
</td>
<td style="text-align:right;">
1709
</td>
</tr>
<tr>
<td style="text-align:right;">
1381
</td>
<td style="text-align:right;">
1247
</td>
</tr>
<tr>
<td style="text-align:right;">
1709
</td>
<td style="text-align:right;">
1247
</td>
</tr>
<tr>
<td style="text-align:right;">
1689
</td>
<td style="text-align:right;">
1782
</td>
</tr>
<tr>
<td style="text-align:right;">
1782
</td>
<td style="text-align:right;">
1468
</td>
</tr>
<tr>
<td style="text-align:right;">
1782
</td>
<td style="text-align:right;">
1304
</td>
</tr>
<tr>
<td style="text-align:right;">
1468
</td>
<td style="text-align:right;">
1101
</td>
</tr>
<tr>
<td style="text-align:right;">
1468
</td>
<td style="text-align:right;">
1641
</td>
</tr>
<tr>
<td style="text-align:right;">
1101
</td>
<td style="text-align:right;">
1641
</td>
</tr>
<tr>
<td style="text-align:right;">
1247
</td>
<td style="text-align:right;">
1911
</td>
</tr>
<tr>
<td style="text-align:right;">
1247
</td>
<td style="text-align:right;">
1501
</td>
</tr>
<tr>
<td style="text-align:right;">
1911
</td>
<td style="text-align:right;">
1501
</td>
</tr>
<tr>
<td style="text-align:right;">
1501
</td>
<td style="text-align:right;">
1934
</td>
</tr>
<tr>
<td style="text-align:right;">
1316
</td>
<td style="text-align:right;">
1934
</td>
</tr>
<tr>
<td style="text-align:right;">
1934
</td>
<td style="text-align:right;">
1304
</td>
</tr>
<tr>
<td style="text-align:right;">
1304
</td>
<td style="text-align:right;">
1661
</td>
</tr>
<tr>
<td style="text-align:right;">
1661
</td>
<td style="text-align:right;">
1025
</td>
</tr>
<tr>
<td style="text-align:right;">
1381
</td>
<td style="text-align:right;">
1510
</td>
</tr>
<tr>
<td style="text-align:right;">
1689
</td>
<td style="text-align:right;">
1510
</td>
</tr>
<tr>
<td style="text-align:right;">
1709
</td>
<td style="text-align:right;">
1689
</td>
</tr>
<tr>
<td style="text-align:right;">
1247
</td>
<td style="text-align:right;">
1381
</td>
</tr>
<tr>
<td style="text-align:right;">
1247
</td>
<td style="text-align:right;">
1709
</td>
</tr>
<tr>
<td style="text-align:right;">
1782
</td>
<td style="text-align:right;">
1689
</td>
</tr>
<tr>
<td style="text-align:right;">
1468
</td>
<td style="text-align:right;">
1782
</td>
</tr>
<tr>
<td style="text-align:right;">
1316
</td>
<td style="text-align:right;">
1782
</td>
</tr>
<tr>
<td style="text-align:right;">
1304
</td>
<td style="text-align:right;">
1782
</td>
</tr>
<tr>
<td style="text-align:right;">
1101
</td>
<td style="text-align:right;">
1468
</td>
</tr>
<tr>
<td style="text-align:right;">
1641
</td>
<td style="text-align:right;">
1468
</td>
</tr>
<tr>
<td style="text-align:right;">
1641
</td>
<td style="text-align:right;">
1101
</td>
</tr>
<tr>
<td style="text-align:right;">
1911
</td>
<td style="text-align:right;">
1247
</td>
</tr>
<tr>
<td style="text-align:right;">
1501
</td>
<td style="text-align:right;">
1247
</td>
</tr>
<tr>
<td style="text-align:right;">
1501
</td>
<td style="text-align:right;">
1911
</td>
</tr>
<tr>
<td style="text-align:right;">
1934
</td>
<td style="text-align:right;">
1501
</td>
</tr>
<tr>
<td style="text-align:right;">
1934
</td>
<td style="text-align:right;">
1316
</td>
</tr>
<tr>
<td style="text-align:right;">
1304
</td>
<td style="text-align:right;">
1934
</td>
</tr>
<tr>
<td style="text-align:right;">
1661
</td>
<td style="text-align:right;">
1304
</td>
</tr>
<tr>
<td style="text-align:right;">
1025
</td>
<td style="text-align:right;">
1661
</td>
</tr>
</tbody>
</table>

**The following is a query that gives all the columns of the likes table
and outputs a dataframes that goes by the same name.**

``` sql
SELECT*

FROM likes
```

**This is what the likes table looks like.**

``` r
likes %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:right;">
ID1
</th>
<th style="text-align:right;">
ID2
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
1689
</td>
<td style="text-align:right;">
1709
</td>
</tr>
<tr>
<td style="text-align:right;">
1709
</td>
<td style="text-align:right;">
1689
</td>
</tr>
<tr>
<td style="text-align:right;">
1782
</td>
<td style="text-align:right;">
1709
</td>
</tr>
<tr>
<td style="text-align:right;">
1911
</td>
<td style="text-align:right;">
1247
</td>
</tr>
<tr>
<td style="text-align:right;">
1247
</td>
<td style="text-align:right;">
1468
</td>
</tr>
<tr>
<td style="text-align:right;">
1641
</td>
<td style="text-align:right;">
1468
</td>
</tr>
<tr>
<td style="text-align:right;">
1316
</td>
<td style="text-align:right;">
1304
</td>
</tr>
<tr>
<td style="text-align:right;">
1501
</td>
<td style="text-align:right;">
1934
</td>
</tr>
<tr>
<td style="text-align:right;">
1934
</td>
<td style="text-align:right;">
1501
</td>
</tr>
<tr>
<td style="text-align:right;">
1025
</td>
<td style="text-align:right;">
1101
</td>
</tr>
</tbody>
</table>

# The following are some of the questions and the respective queries that seek to answer them.

## Find the names of all students who are friends with someone named Gabriel.

``` sql
WITH gabriel_id AS (
SELECT 
    Id
FROM
    Highschooler
WHERE
    name = 'Gabriel'),
gabriel_friends_id as
(SELECT 
    ID2
FROM
    friend
WHERE
    ID1 IN (SELECT 
            *
        FROM
            gabriel_id))
SELECT 
    name
FROM
    highschooler
WHERE
    ID IN (SELECT 
            *
        FROM
            gabriel_friends_id)
```

**The results of the querry are presented below as an R dataframe called
Querry1.**

``` r
Query1 %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
name
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Cassandra
</td>
</tr>
<tr>
<td style="text-align:left;">
Andrew
</td>
</tr>
<tr>
<td style="text-align:left;">
Jessica
</td>
</tr>
<tr>
<td style="text-align:left;">
Jordan
</td>
</tr>
<tr>
<td style="text-align:left;">
Alexis
</td>
</tr>
</tbody>
</table>

## For every student who likes someone 2 or more grades younger than themselves, return that student’s name and grade, and the name and grade of the student they like.

``` sql
WITH liking_student AS
(SELECT 
    ID1, name, grade, ID2 AS liked_student_id
FROM
    likes
        JOIN
    highschooler ON ID1 = ID),
liked_student as 
(SELECT 
    ID2, name AS liked_name, grade AS liked_grade
FROM
    likes
        JOIN
    highschooler ON ID2 = ID)
SELECT 
    name, grade, liked_name, liked_grade
FROM
    liking_student
        JOIN
    liked_student ON liked_student_id = ID2
WHERE
    grade - liked_grade >= 2;
```

**The result of the query is stored in a data frame called Querry2 and
displayed below.**

``` r
Query2 %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
name
</th>
<th style="text-align:right;">
grade
</th>
<th style="text-align:left;">
liked_name
</th>
<th style="text-align:right;">
liked_grade
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
John
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:left;">
Haley
</td>
<td style="text-align:right;">
10
</td>
</tr>
</tbody>
</table>

## For every pair of students who both like each other, return the name and grade of both students. Include each pair only once, with the two names in alphabetical order.

``` sql
WITH combined AS
(SELECT 
    ID1,
    name AS liking_name,
    grade AS liking_grade,
    ID2,
    concat(ID1,"-",ID2) AS ID1_likes_ID2,
    concat(ID2,"-",ID1) AS ID2_likes_ID1
FROM likes JOIN highschooler ON ID1 = ID),
mutual_likes_filtered AS 
(SELECT 
    ID2_likes_ID1
FROM
    combined)
SELECT 
    liking_name,
    liking_grade,
    name AS mutually_likedname,
    grade AS mutually_likedgrade
FROM
    combined
        JOIN
    highschooler ON ID2 = ID
WHERE
    ID1_likes_ID2 IN (SELECT 
            *
        FROM
            mutual_likes_filtered)
        AND Liking_name < name;
```

**The results are saved in a data frame called Query3 and displayed
below**

``` r
Query3 %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
liking_name
</th>
<th style="text-align:right;">
liking_grade
</th>
<th style="text-align:left;">
mutually_likedname
</th>
<th style="text-align:right;">
mutually_likedgrade
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Cassandra
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:left;">
Gabriel
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:left;">
Jessica
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;">
Kyle
</td>
<td style="text-align:right;">
12
</td>
</tr>
</tbody>
</table>

## Find all students who do not appear in the Likes table (as a student who likes or is liked) and return their names and grades. Sort by grade, then by name within each grade.

``` sql
SELECT 
    name, grade
FROM
    highschooler
WHERE
    ID NOT IN (SELECT 
            ID1
        FROM
            likes UNION SELECT 
            ID2
        FROM
            likes)
ORDER BY grade , name;
```

**The results are saved in a dataframe called Query4 and displayed
below**

``` r
Query4 %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
name
</th>
<th style="text-align:right;">
grade
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Jordan
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:left;">
Tiffany
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:left;">
Logan
</td>
<td style="text-align:right;">
12
</td>
</tr>
</tbody>
</table>

## For every situation where student A likes student B, but we have no information about whom B likes (that is, B does not appear as an ID1 in the Likes table), return A and B’s names and grades.

``` sql

WITH student_A AS 
(SELECT 
    name AS name_A, grade AS grade_A, ID2
FROM
    likes
        JOIN
    highschooler ON ID1 = ID
WHERE
    ID2 NOT IN (SELECT 
            ID1
        FROM
            likes))
SELECT 
    name_A, grade_A, name AS name_B, grade AS grade_B
FROM
    Student_A
        JOIN
    highschooler ON ID2 = ID;
```

**The results are saved in dataframe named Query5 and displayed below**

``` r
Query5 %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
name_A
</th>
<th style="text-align:right;">
grade_A
</th>
<th style="text-align:left;">
name_B
</th>
<th style="text-align:right;">
grade_B
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Alexis
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;">
Kris
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:left;">
Brittany
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:left;">
Kris
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:left;">
Austin
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;">
Jordan
</td>
<td style="text-align:right;">
12
</td>
</tr>
<tr>
<td style="text-align:left;">
John
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:left;">
Haley
</td>
<td style="text-align:right;">
10
</td>
</tr>
</tbody>
</table>

## Find names and grades of students who only have friends in the same grade. Return the result sorted by grade, then by name within each grade.

``` sql
WITH student AS
(SELECT 
    ID1, name, grade, ID2
FROM
    friend
        JOIN
    highschooler ON ID1 = ID),
friends AS
(SELECT 
    ID2 AS friend_Id, name AS friend_name, grade AS friend_grade
FROM
    friend
        JOIN
    highschooler ON ID2 = ID)
SELECT 
    name, grade
FROM
    student
        JOIN
    friends ON ID2 = friend_id
GROUP BY ID1
HAVING AVG(grade) = AVG(friend_grade)
ORDER BY grade , name;
```

``` r
Query6 %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
name
</th>
<th style="text-align:right;">
grade
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Jordan
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:left;">
Brittany
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:left;">
Haley
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:left;">
Kris
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:left;">
Gabriel
</td>
<td style="text-align:right;">
11
</td>
</tr>
<tr>
<td style="text-align:left;">
John
</td>
<td style="text-align:right;">
12
</td>
</tr>
<tr>
<td style="text-align:left;">
Logan
</td>
<td style="text-align:right;">
12
</td>
</tr>
</tbody>
</table>

## For each student A who likes a student B where the two are not friends, find if they have a friend C in common (who can introduce them!). For all such trios, return the name and grade of A, B, and C.

``` sql
With pair_likes AS
(SELECT 
    ID1, h1.name AS student_A, h1.grade AS student_A_grade, ID2, h2.name AS student_B, h2.grade AS student_B_grade, concat(ID1,"-",ID2) AS like_pair
FROM
    likes,
    highschooler h1,
    highschooler h2
WHERE
    ID1 = h1.ID AND ID2 = h2.ID),
    pair_friends AS
(SELECT 
    ID1, h1.name AS friend_A, h1.grade AS friend_A_grade, ID2, h2.name AS friend_B, h2.grade AS friend_B_grade, concat(ID1,"-",ID2) AS friend_pair
FROM
    friend,
    highschooler h1,
    highschooler h2
WHERE
    ID1 = h1.ID AND ID2 = h2.ID),
    
student_A_potential_C AS 
(SELECT 
    student_A,
    student_A_grade,
    pf.ID2 AS pc2_ID,
    friend_B AS pc_name_a,
    friend_B_grade AS pc_grade_a,
    pl.ID2 AS lk_ID
FROM
    pair_likes pl
        JOIN
    pair_friends pf ON pl.ID1 = pf.ID1
WHERE
    like_pair NOT IN (SELECT 
            friend_pair
        FROM
            pair_friends)),

student_B_potential_C AS
(SELECT 
    pl.ID2 AS lk_ID,
    student_B,
    student_B_grade,
    pf.ID2 AS pc1_ID,
    friend_B AS potential_c_b,
    friend_B_grade AS pc_grade_b
FROM
    pair_likes pl
        JOIN
    pair_friends pf ON pl.ID2 = pf.ID1
WHERE
    like_pair NOT IN (SELECT 
            friend_pair
        FROM
            pair_friends))

SELECT 
    student_A,
    student_A_grade,
    student_B,
    student_B_grade,
    pc_name_a AS Student_C,
    pc_grade_b AS Student_C_grade
FROM
    student_A_potential_C ac
        JOIN
    student_B_potential_C bc ON pc1_ID = pc2_ID
WHERE
    ac.lk_ID = bc.lk_ID;
```

**The results were saved in datafarme named Query7 and are displayed
below.**

``` r
Query7 %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
student_A
</th>
<th style="text-align:right;">
student_A\_grade
</th>
<th style="text-align:left;">
student_B
</th>
<th style="text-align:right;">
student_B\_grade
</th>
<th style="text-align:left;">
Student_C
</th>
<th style="text-align:right;">
Student_C\_grade
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Andrew
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:left;">
Cassandra
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:left;">
Gabriel
</td>
<td style="text-align:right;">
9
</td>
</tr>
<tr>
<td style="text-align:left;">
Austin
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;">
Jordan
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:left;">
Andrew
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:left;">
Austin
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;">
Jordan
</td>
<td style="text-align:right;">
12
</td>
<td style="text-align:left;">
Kyle
</td>
<td style="text-align:right;">
12
</td>
</tr>
</tbody>
</table>

## Find the difference between the number of students in the school and the number of different first names.

``` sql
SELECT count(ID)-count(distinct name) AS answer
FROM highschooler;
```

**The results were saved in a dataframe called Query8 and is displaed
below.**

``` r
Query8 %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:right;">
answer
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
2
</td>
</tr>
</tbody>
</table>

## Find the name and grade of all students who are liked by more than one other student.

``` sql

SELECT 
    name, grade
FROM
    highschooler
WHERE
    ID IN (SELECT 
            ID2
        FROM
            likes
        GROUP BY ID2
        HAVING COUNT(ID2) > 1);
```

**The results of the query were saved in a data frame called Query9 and
are shown below**

``` r
Query9 %>% kable() %>% kable_classic()
```

<table class=" lightable-classic" style="font-family: &quot;Arial Narrow&quot;, &quot;Source Sans Pro&quot;, sans-serif; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
name
</th>
<th style="text-align:right;">
grade
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Kris
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:left;">
Cassandra
</td>
<td style="text-align:right;">
9
</td>
</tr>
</tbody>
</table>
