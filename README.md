# Introduction and purpose

The database has been designed for efficient access and analysis across songs, artists, users and usage of Sparkify.
Sparkify can use it to understand trends and preferences across their user base, improve their suggestion engine, as well as cater for changing server traffic using time data. 

# Design

Design consists of 5 tables, each with a unique primary key and every cell containing only single values. The star schema design - split between songs, artist, users, time (dimensions) and songplay (fact) tables reflects the categories of data collected by Sparkify making the access intuitive and logical.

### Fact Table:
**songplays** - records in log data associated with song plays i.e. records with page NextSong
songplay_id PK varchar, start_time timestamp, user_id varchar, level varchar, song_id varchar, artist_id varchar, session_id varchar, location varchar, user_agent varchar

### Dimension Tables:
**users** - Sparkify users
user_id PK varchar, first_name varchar, last_name varchar, gender varchar, level varchar

**songs** - songs in the database
song_id PK varchar, title varchar, artist_id varchar, year int, duration numeric

**artists** - information about artists in the database
artist_id PK varchar, name varchar, artist_location varchar, artist_latitude numeric, artist_longitude numeric

**time** - starting time timestamp for songplays split between specific time units
start_time timestamp, hour int, day int, week int, month int, year int, weekday int

# Files

**create_tables.py** - file setting up the database, as well as fact and dimension tables
**etl.ipynb** - Jupyter notebook allowing to test individual components of the program and analyse the dataset
**etl.py** - main file used to read and process available data
**sql_queries.py** - file containing SQL queries for dropping and creating tables, as well as a template for data insertion
**test.ipynb** - Jupyter notebook used to test and explore data loaded 

# Sample queries

SELECT t.hour, COUNT(*) num_of_plays FROM songplays s JOIN time t ON s.start_time = t.start_time GROUP BY t.hour ORDER BY t.hour  --> number of sessions 
SELECT a.artist_name, COUNT(*) num_of_plays FROM songplays s JOIN artists a ON a.artist_id = s.artist_id WHERE s.artist_id IS NOT NULL GROUP BY a.artist_name ORDER BY num_of_plays DESC LIMIT 10 --> top 10 artists

# How to use

Run below programs sequentially in the terminal:
1. create_tables.py
2. etl.py



