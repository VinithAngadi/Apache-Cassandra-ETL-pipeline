# Apache-Cassandra-ETL-pipeline
=======
## Purpose of Project
The database has been built to serve the purpose of analyzing songs that users are listening to on Sparkify (music streaming app). This project has scripts to create database tables according to the desired schema, loads data from csv files and inserts into a table on Apache Cassandra cluster. Only neccessary information of users, songs and artists that are required for analysis are loaded into a final csv file. A new custom table is designed out of the final csv file for each query.

## Tools used
- Database:  Apache Cassandra
- Language: Python 3.6.3


## Files description
1. Apache-Cassandra-ETL.ipynb : Has scripts that are run to test the ETL pipeline by loading contents from data folders to Apache Cassamdra cluster.

## Data files
 song_data : Contains daily activity logs from the app for the month 11/2018.

## Table Design and ETL
 1. Retrieve the artist, song title and song's length in the music app history that was heard during  sessionId = 338, and itemInSession  = 4.
    The table has sessionId and itemInSession as it's composite keys to optimize query execution. Data is partitioned across nodes by hashing sessionId and sorted in each node by itemInSession.
 2. Retrieve only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182
    The table has (userId, sessionId) as partition keys and itemInSession as clustering keys to optimize query execution. Data is partitioned across nodes by (userId, sessionId) combo. Each node has data sorted by itemInSession, as required by the query.
 3. Retrieve every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'
    The table has (song, userid) as partition keys and itemInSession as clustering keys to optimize query execution. We cannot use only song as a unique key, hence the combination of song name and userId is required.



