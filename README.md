# data-engineering-db-docker
Documents/data_engineering_db
  
if error: docker login then pull
    
    docker pull postgres 
   
 container name- data.engineering-postgres, image name- postgres 
    
    docker run --name data-engineering-postgres -e POSTGRES_PASSWORD=secret -d postgres

  create db named postgers-db
    
     docker exec -u postgres data-engineering-postgres createdb postgres-db

get insude the database

    winpty docker exec -it data-engineering-postgres psql -U postgres -d postgres-db psql

# SQL

## Commands:

### Creating Database:

```sql
CREATE DATABASE db;
```

### Connecting to db

```sql
\c db
```

### Create users table

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    date_of_birth DATE
);
```

### Inserting Fake Data

```sql
INSERT INTO users (first_name, last_name, email, date_of_birth) VALUES
('John', 'Doe', 'john.doe@example.com', '1990-01-01'),
('Jane', 'Smith', 'jane.smith@example.com', '1992-05-15'),
('Alice', 'Johnson', 'alice.johnson@example.com', '1985-10-20'),
('Bob', 'Williams', 'bob.williams@example.com', '1998-07-30'),
('Emily', 'Clark', 'emily.clark@example.com', '1987-02-14'),
('Michael', 'Robinson', 'michael.robinson@example.com', '1995-06-05'),
('Sarah', 'Lewis', 'sarah.lewis@example.com', '1989-03-25'),
('David', 'Walker', 'david.walker@example.com', '1992-11-12'),
('Sophia', 'Hall', 'sophia.hall@example.com', '1996-08-08'),
('James', 'Allen', 'james.allen@example.com', '1984-04-20'),
('Olivia', 'Young', 'olivia.young@example.com', '1993-12-30'),
('Chris', 'King', 'chris.king@example.com', '1990-09-15'),
('Grace', 'Wright', 'grace.wright@example.com', '1997-05-10'),
('William', 'Scott', 'william.scott@example.com', '1986-07-22');
```

### Creating films Table,

```sql
CREATE TABLE films (
    film_id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    release_date DATE,
    price DECIMAL(5,2),
    rating VARCHAR(10),
    user_rating DECIMAL(2,1) CHECK (user_rating >= 1 AND user_rating <= 5)
);
```

### Inserting Data to films:

```sql
INSERT INTO films (title, release_date, price, rating, user_rating) VALUES
('Inception', '2010-07-16', 12.99, 'PG-13', 4.8),
('The Shawshank Redemption', '1994-09-23', 9.99, 'R', 4.9),
('The Godfather', '1972-03-24', 14.99, 'R', 4.7),
('The Dark Knight', '2008-07-18', 11.99, 'PG-13', 4.8),
('Pulp Fiction', '1994-10-14', 10.99, 'R', 4.6),
('The Matrix', '1999-03-31', 9.99, 'R', 4.7),
('Forrest Gump', '1994-07-06', 8.99, 'PG-13', 4.5),
('Toy Story', '1995-11-22', 7.99, 'G', 4.4),
('Jurassic Park', '1993-06-11', 9.99, 'PG-13', 4.3),
('Avatar', '2009-12-18', 12.99, 'PG-13', 4.2),
('Blade Runner 2049', '2017-10-06', 13.99, 'R', 4.3),
('Mad Max: Fury Road', '2015-05-15', 11.99, 'R', 4.6),
('Coco', '2017-11-22', 9.99, 'PG', 4.8),
('Dunkirk', '2017-07-21', 12.99, 'PG-13', 4.5),
('Spider-Man: Into the Spider-Verse', '2018-12-14', 10.99, 'PG', 4.9),
('Parasite', '2019-10-11', 14.99, 'R', 4.6),
('Whiplash', '2014-10-10', 9.99, 'R', 4.7),
('Inside Out', '2015-06-19', 9.99, 'PG', 4.8),
('The Grand Budapest Hotel', '2014-03-28', 10.99, 'R', 4.4),
('La La Land', '2016-12-09', 11.99, 'PG-13', 4.5);
```

### Creating film_category table:

```sql
CREATE TABLE film_category (
    category_id SERIAL PRIMARY KEY,
    film_id INTEGER REFERENCES films(film_id),
    category_name VARCHAR(50) NOT NULL
);
```

### Inserting Data:

```sql
INSERT INTO film_category (film_id, category_name) VALUES
(1, 'Sci-Fi'),
(1, 'Thriller'),
(2, 'Drama'),
(3, 'Crime'),
(3, 'Drama'),
(4, 'Action'),
(4, 'Thriller'),
(5, 'Crime'),
(5, 'Drama'),
(6, 'Sci-Fi'),
(6, 'Action'),
(7, 'Drama'),
(7, 'Romance'),
(8, 'Animation'),
(8, 'Family'),
(9, 'Action'),
(9, 'Adventure'),
(10, 'Sci-Fi'),
(10, 'Adventure'),
(11, 'Sci-Fi'),
(11, 'Drama'),
(12, 'Action'),
(12, 'Adventure'),
(13, 'Animation'),
(13, 'Family'),
(14, 'War'),
(14, 'Drama'),
(15, 'Animation'),
(15, 'Action'),
(16, 'Drama'),
(16, 'Thriller'),
(17, 'Drama'),
(17, 'Music'),
(18, 'Animation'),
(18, 'Family'),
(19, 'Comedy'),
(19, 'Drama'),
(20, 'Drama'),
(20, 'Music');
```

### Inner Join Example:

```sql
SELECT f.title, a.actor_name
FROM films f
INNER JOIN film_actors fa ON f.film_id = fa.film_id
INNER JOIN actors a ON fa.actor_id = a.actor_id;
```

### Left Join Example

```sql
SELECT f.title, a.actor_name
FROM films f
LEFT JOIN film_actors fa ON f.film_id = fa.film_id
LEFT JOIN actors a ON fa.actor_id = a.actor_id;
```

### Creating Actors Table:

```sql
CREATE TABLE actors (
    actor_id SERIAL PRIMARY KEY,
    actor_name VARCHAR(255) NOT NULL
);
```

### Creating film_actors Table:

```sql
CREATE TABLE film_actors (
    film_id INTEGER REFERENCES films(film_id),
    actor_id INTEGER REFERENCES actors(actor_id),
    PRIMARY KEY (film_id, actor_id)
);
```

### Inserting data into actors table:

```sql
INSERT INTO actors (actor_name) VALUES
('Leonardo DiCaprio'),  -- Associated with Inception
('Tim Robbins'),        -- Associated with The Shawshank Redemption
('Marlon Brando'),      -- Associated with The Godfather
('Christian Bale'),     -- Associated with The Dark Knight
('John Travolta'),      -- Associated with Pulp Fiction
('Keanu Reeves'),       -- Associated with The Matrix
('Tom Hanks'),          -- Associated with Forrest Gump
('Tom Hanks'),          -- Associated with Toy Story (Tom Hanks appears twice for demonstration purposes)
('Sam Neill'),          -- Associated with Jurassic Park
('Sam Worthington'),    -- Associated with Avatar
('Ryan Gosling'),       -- Associated with Blade Runner 2049
('Tom Hardy'),          -- Associated with Mad Max: Fury Road
('Anthony Gonzalez'),   -- Associated with Coco
('Fionn Whitehead'),    -- Associated with Dunkirk
('Shameik Moore'),      -- Associated with Spider-Man: Into the Spider-Verse
('Song Kang-ho'),       -- Associated with Parasite
('Miles Teller'),       -- Associated with Whiplash
('Amy Poehler'),        -- Associated with Inside Out
('Ralph Fiennes'),      -- Associated with The Grand Budapest Hotel
('Emma Stone');         -- Associated with La La Land
```

### Inserting data into film_actors table:

```sql
INSERT INTO film_actors (film_id, actor_id) VALUES
(1, 1),
(2, 2),
(3, 3),
(4, 4),
(5, 5),
(6, 6),
(7, 7),
(8, 8),
(9, 9),
(10, 10),
(11, 11),
(12, 12),
(13, 13),
(14, 14),
(15, 15),
(16, 16),
(17, 17),
(18, 18),
(19, 19),
(20, 20);
```

### Left Join with Alias:

```sql
SELECT 
    f.film_id, 
    f.title, 
    a.actor_name
FROM 
    films f
LEFT JOIN 
    film_actors fa ON f.film_id = fa.film_id
LEFT JOIN 
    actors a ON fa.actor_id = a.actor_id
ORDER BY 
    f.film_id;
```

### Inner Join with Alias

```sql
SELECT 
    f.film_id, 
    f.title, 
    a.actor_name
FROM 
    films f
INNER JOIN 
    film_actors fa ON f.film_id = fa.film_id
INNER JOIN 
    actors a ON fa.actor_id = a.actor_id
ORDER BY 
    f.film_id;
```

### Union:

```sql
SELECT title AS name
FROM films
UNION
SELECT actor_name AS name
FROM actors
ORDER BY name;
```

### Union All:

```sql
SELECT title AS name
FROM films
UNION ALL
SELECT actor_name AS name
FROM actors
ORDER BY name;
```

**Subquery in the `SELECT` Clause**:

- Retrieve each film's title along with the name of one of its actors.

```sql
SELECT title,
       (SELECT actor_name
        FROM actors a
        JOIN film_actors fa ON a.actor_id = fa.actor_id
        WHERE fa.film_id = f.film_id
        LIMIT 1) AS actor_name
FROM films f;
```

**Subqueries with `IN`**:

- Retrieve films that have either Leonardo DiCaprio or Tom Hanks as actors.

```sql
SELECT title
FROM films
WHERE film_id IN
(SELECT fa.film_id
 FROM film_actors fa
 JOIN actors a ON a.actor_id = fa.actor_id
 WHERE a.actor_name IN ('Leonardo DiCaprio', 'Tom Hanks'));
```
