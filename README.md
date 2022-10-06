# Data-Modeling-with-Postgres
Udacity Project

Introduction

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

Schema

The project went with the star schema for the database modeling. I first made the songplays table that is going to be the fact table. After that I created 4 additional tables (dimension tables), songs, artists, time and users. With these schema the query performance will be better as it only has a small number of tables and a clear join paths. It is easily understood and has a built in referential integrity via primary keys per table. 

ETL Pipeline

First we created our tables and defined an insert function. Next, we extracted the data from the song_data, trimmed the unnecessary columns and inserted all the data into the songs and artists table. After that we then extracted the data from log_data and just like what we did with the song_data, trimmed the unnecessary columns and inserted them all into their respective tables. Once that is complete we then used those data to form the songplays table which will serve as our fact table. 

Files Description

The project is divided into 6 files:

create_tables.py: this is the python script that creates the database and tables that will be used. 
etl.ipnyb: this is the jupyter notebook used to test the code before implementing it in the main script. 
etl.py: this is the python script that when run, reads the song_data and log_files and inserts the values in the tables.
sql_queries.py: this is the python script that defines the functions used by the create table script.
test.ipnyb: this is the jupyter notebook used to check if the code did what it was meant to do. 
readme.md: this is the summary and instructions for the project.

How to Run

At the console run the create_tables.py script. After that, run the etl.py. You can always use and run the test.ipnyb 
as long as you dont forget to restart that kernel as only one connection to the database can be done.

Uses

There are a variety of ways the company can use these database. One example I can think of is if they want to personalize their recommendations based on what their users are listening to. A sample query could look like this

SELECT users.user_id, songs.song_id, artist.artist_id FROM users
JOIN songplays ON songplays.user_id = songs.user_id
JOIN songs ON songplays.song_id = songs.song_id
WHERE users.user_id = random user number
GROUPBY artist_id



