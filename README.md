# SQL_COURSE
All SQL basics and intermediate level



# COUNT, DISTINCT, LIMIT


# Exploring the Database

**Let us first explore the SanFranciscoFilmLocations database using the Datasette tool:**

**SELECT * FROM FilmLocations;**

These are the column attribute descriptions from the FilmLocations table:

FilmLocations(
Title:              titles of the films, 
ReleaseYear:        time of public release of the films, 
Locations:          locations of San Francisco where the films were shot, 
FunFacts:           funny facts about the filming locations, 
ProductionCompany:  companies who produced the films, 
Distributor:        companies who distributed the films, 
Director:           people who directed the films, 
Writer:             people who wrote the films, 
Actor1:             person 1 who acted in the films, 
Actor2:             person 2 who acted in the films,
Actor3:             person 3 who acted in the films
)



# Using COUNT statement

1) Suppose we want to count the number of records or rows of the "FilmLocations" table. The query for this would be:

   **SELECT COUNT(*) FROM FilmLocations;**

2) We want to count the number of locations of the films. But we also want to restrict the output result set so that we only retrieve the number
of locations of the films written by a certain writer. The query for this can be written as:

  **SELECT COUNT(Locations) FROM FilmLocations WHERE Writer="James Cameron";**

# Using DISTINCT statement

1) Assume that we want to retrieve the titles of all films in the table so that duplicates will be discarded in the output result set.

  **SELECT DISTINCT Title FROM FilmLocations;**

2) We want to retrieve the count of release years of the films produced by a specific company so that duplicate release years of those films will be discarded in the count.

   **SELECT COUNT(DISTINCT ReleaseYear) FROM FilmLocations WHERE ProductionCompany="Warner Bros. Pictures";**


# Using LIMIT statement

1) Retrieve only the first 25 rows from the table so that rows other than those are not in the output result set.

   **SELECT * FROM FilmLocations LIMIT 25;**

2) Now, we want to retrieve 15 rows from the table starting from row 11.

   **SELECT * FROM FilmLocations LIMIT 15 OFFSET 10;**

# Practice exercises

**COUNT**
1) Retrieve the number of locations of the films which are directed by Woody Allen.

   Query Solution

   **SELECT COUNT(Locations) FROM FilmLocations WHERE Director="Woody Allen";**

3) Retrieve the number of films shot at Russian Hill.

   Query Solution

   **SELECT Count(Title) FROM FilmLocations WHERE Locations="Russian Hill";**

5) Retrieve the number of rows having a release year older than 1950 from the "FilmLocations" table.

   Query Solution

   **SELECT Count(*) FROM FilmLocations WHERE ReleaseYear<1950;**


**DISTINCT**

1) Retrieve the names of all unique films released in the 21st century and onwards, along with their release years.

   Query Solution

   **SELECT DISTINCT Title, ReleaseYear FROM FilmLocations WHERE ReleaseYear>=2001;**

2) Retrieve the directors' names and their distinct films shot at City Hall.

   Query Solution

   **SELECT DISTINCT Title, Director FROM FilmLocations WHERE Locations="City Hall";**

3) Retrieve the number of distributors who distributed films with the 1st actor, Clint Eastwood.

   Query Solution
   
   **SELECT COUNT(DISTINCT Distributor) FROM FilmLocations WHERE Actor1="Clint Eastwood";**

**LIMIT**

1) Retrieve the names of the first 50 films.

   Query Solution
   
   **SELECT DISTINCT Title FROM FilmLocations LIMIT 50;**

2) Retrieve the first 10 film names released in 2015.

   Query Solution
   
   **SELECT DISTINCT Title FROM FilmLocations WHERE ReleaseYear=2015 LIMIT 10;** 

3) Retrieve the next 3 film names that follow after the first 5 films released in 2015.

   Query Solution

   **SELECT DISTINCT Title FROM FilmLocations WHERE ReleaseYear=2015 LIMIT 3 OFFSET 5;**





