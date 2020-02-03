This file contains technical information on creating and using the database sparkifydb

## Project Description

This is a project created by Sparkify's team. Sparkify wants to analyze the data we have been collecting on songs and user activity on our music streaming app. The purpose of this project is to collect relevant data, design a database schema and insert the collected data into the PostgreSQL database sparkifydb. This database is going to be used as a single source of truth by the analytical team for BI and Machine Learning projects later on. The etl pipeline has been created using Python 3.x

## Schema for Database Design
Star schema has been used to create the database. The dabase consists of 5 tables.

***songlpays*** is a fact table containing records in log data associated with song plays. This table has the following columns: songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

users, artists, songs and time are dimensional tables
***users*** has the following columns: user_id, first_name, last_name, gender, level
***songs*** has the following columns: song_id, title, artist_id, year, duration
***artists*** has the following columns: artist_id, name, location, latitude, longitude
***time*** has the following columns: start_time, hour, day, week, month, year, weekday

## ETL Pipeline

Currently the data resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app (see the directory named data). We use the song and log datasets and createad a database dbo.sparkify optimized for queries on song play analysis.
5 files belong to this project:
create_table.py
etl.ipynb
etl.py
sql_queries.py
test.ipynb
 
The data from json files is loaded into pandas dataframes, read, checked, transformed and inserted into relevant tables. song_data files data is inderted into songs and artists tables while log_data files data is inserted into time and users tables. sonplays fact table data takes log_data records, and song_id, artist_id columns from songs and artists tables. 
create_tables.py drops and creates the tables. 
etl.py reads and processes files from song_data and log_data and loads them into the tables.
sql_queries.py contains all sql queries we have been using. It is imported into the create_tables.py and etl.py
etl.ipynb is a python notebook file that reads and processes a single file from song_data and log_data and loads the data into the tables
test.ipynb is used for testing

# Query Examples

Analytics department wants to know how many users have paid memberships and how many are using the free membership.
```
SELECT COUNT (*) FROM users WHERE level = 'paid';
SELECT COUNT (*) FROM users WHERE level = 'free';
```

Analytics department is also interested which days of the week generates most of the events, i.e. when users are the most active.

```
SELECT weekday, COUNT(*) FROM time GROUP BY weekday
```
