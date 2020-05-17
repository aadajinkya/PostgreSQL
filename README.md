# Problem Statement

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

Your role is to create a database schema and ETL pipeline for this analysis.


# Objectives

- Implement data modeling with PostgreSQL. 
- Define fact and dimension table for star schema for a particular analytic focus.
- Build ETL pipeline that transfers data from files into the tables in PostgreSQL using Python and SQL. 


# Dataset

### Song Dataset

This dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song

Example of what a single song file looks like:

```json
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}
```

### Log Dataset

Consists of log files in JSON format.It has activity logs based on specified configurations.

Example of what a single log file looks like:

```json
{"artist":"Pavement","auth":"Logged In","firstName":"Sylvie","gender":"F","itemInSession":0,"lastName":"Cruz","length":99.16036,"level":"free","location":"Washington-Arlington- Alexandria, DC-VA-MD-WV","method":"PUT","page":"NextSong","registration":1540266e+12,"sessionId":345,"song":"Mercy:The Laundromat","status":200,"ts":1541990258796,"userAgent":""\"Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_9_4...", "userId":"10"}
```

# Database Schema
The Schema used in this project is a Star Schema with one fact table: songplays and 4 dimension tables: users, songs, artists, time. 


## Purpose of using relational database

- The data is not big enough to use big data analysis mehtods.
- The dataset provided is structured data(json files) and thus can be modeled using relational database.
- Analysis required in the project can be easily done using SQL and can be used to answer all the questions.
- Star Schema is used as we need to do joins to get the required answer and star schema would facilitate in optimising the joins.

## Table description

### Fact table:

### songplays: records in log data associated with song plays
songplay_id int primary key, 
start_time bigint, 
user_id int, 
level text, 
song_id text, 
artist_id text, 
session_id int,
location text, 
user_agent text

### Dimension tables:

### users: users in the app
user_id int primary key,
first_name text not null, 
last_name text not null, 
gender text, 
level text

### songs: songs in music database
song_id text primary key, 
title text not null, 
artist_id text, 
year int, 
duration float not null

### artists: artists in music database
artist_id text primary key,
name text not null, 
location text, 
latitude float,
longitude float

### time: timestamps of records in songplays broken down into specific units
start_time bigint primary key,
hour int, 
day int ,
week int ,
month int,
year int, 
weekday text



# File Structure

- **sql_queries.py:** contains all your sql queries
- **create_tables.py:** drops and creates tables. You run this file to reset your tables before each time you run your ETL scripts.
- **test.ipynb:** displays the first few rows of each table to let you check your database.
- **etl.ipynb:** reads and processes a single file from song_data and log_data and loads the data into your tables.
- **etl.py:** reads and processes files from song_data and log_data and loads them into your tables.
- **README.md:** provides discussion on this project