# Backgrounds
---
## Sparkify 
Sparkify services music streaming app. Sparkify team is interested in which songs their users listening to, with their streaming app. 

## Analytical Goals
- Goal of analysis is to understand what songs users are listening to
- Currently, usage log data and song data are stored in a JSON format, which is hard to query on. 
- Data engineers are to design and build Postgre SQL DB using JSON data, so that Sparkify team can easily query their data. 

# Database Schema Design
---
- DB utilizes star schema 
- Fact tables
    - song plays log table 
- Dimension tables
    - songs table
    - artist table
    - user table
    - time table

# ETL Pipeline
---
- Extracting songs and artist data
    - Data for songs and artists relations are extracted from song_data (JSON format)
    - From song_data, 
        - song_id, title, artist_id, year, duration are loaded onto songs relation
        - artist_id, artist_name, artist_location, artist_latitude, artist_longitude are loaded onto artists relation
- Extracting user, time, log data
    - Data for user, time and song plays relations are extracted from log_data(JSON format)
    - From log_data,
        - ts (timestamp) data is loaded onto time relation. Hour, day, week of year, month and weekday values are extracted from ts before loaded. 
        - user_id, first_name, last_name, gender, level are loaded onto users relation
        - songplays table, which is a fact table, has ts, user_id, level, song_id, artist_id, session_id, location, user_agent as its columns 
        
# How to run ETL pipeline? 
--- 
- Executing command "python create_tables.py" will create schema
- Executing command "python etl.py" will extract data from json files and load onto database tables. 
- To check if ETL pipeline worked as intended, run cells in the test.ipynb. After running cells in the jupyter notebook, you should restart kernel in order to disconnect from the database. 
- To see details on how codes from etl.py is implemented, check etl.ipynb. 