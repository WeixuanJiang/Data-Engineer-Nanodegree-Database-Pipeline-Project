## Project Description

Sparkify, a music streaming startup, wants to evaluate the data they've collected on songs and user activity on their new app. The analytics team is particularly curious about the music that consumers are listening to. They now lack an easy mechanism to query their data, which is stored in a directory of JSON logs on user activity on the app, as well as a directory of JSON information on the songs in the app.


## About Database

We have used two datasets: 
1. song_data
2. log_data

The sparkify db schema is designed in a star schema. Start design denotes the presence of a single Dimension Table containing business data, as well as supporting Fact Tables. One of the most important questions is what music people are listening to. Dimension Table provides an answer to this topic. 

Fact Table
songplays: song play data together with user, artist, and song info (songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent)

Dimension Tables
users: user info (columns: user_id, first_name, last_name, gender, level)
songs: song info (columns: song_id, title, artist_id, year, duration)
artists: artist info (columns: artist_id, name, location, latitude, longitude)
time: detailed time info about song plays (columns: start_time, hour, day, week, month, year, weekday)

## About Scripts

1. create_tables.py: This script connects to the database.
2. etl.py: This script uses data in ./data/song_data and ./data/log_data, load the data and process data.
3. sql_queries.py: This script stores all necessary queries such as create table, drop table and insert data.

Run sql_queries.py

    python3 sql_queries.py
    
Then run create_tables.py

    python3 create_tables.py
    
Lasty run etl.py

    python3 etl.py
    
Optional: Run test.ipynb Juppyter notebook to confirm the creation of the tables with the correct columns.
    
## Data Cleaning Process

1. Scripts get read json data from data folder
2. From each file in ./data/song_data directory, script selects songs table values to a song_data DataFrame and inserts them to songs table, and artist table values to artist_data DataFrame and inserts them to artists table.
3. From each file in ./data/logdata directory, script filters items with NextSong value in page parameter. It then processes _time_data from ts parameter value to be inserted in time table and user_data to be inserted in users table.
4. data/songdata directory also contains data which is processed into _songplay_data. User_id and artist_id fields are fetched from users and artists table using song_select query. Other parameters are selected from log_data. Formed songplay_data data is finally inserted into songplays table