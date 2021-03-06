# Web Scraping

Parsing a data source: 

## Password and URL

In WebScraper.py, enter your own db password where it says ENTERPASSWORDHERE

In WebScraper.py, enter the test URL

## Docker
Python 3: 
    docker run -it --rm --name web-scraping-container -v "$PWD":. python:3 python WebScraper.py
Python 2:
    docker run -it --rm --name web-scraping-container -v "$PWD":. python:2 python WebScraper.py

OR 

docker build.

docker run --name insert_name code_given_by_docker

## Without Docker
## Prereqs

Type the following in the command line:
    pip install beautifulsoup4
    pip install PyMySQL
Install MySQL https://dev.mysql.com/downloads/installer/
^ This should also install MySQL Workbench. If not, installation instructions are at https://docs.oracle.com/cd/E19078-01/mysql/mysql-workbench/wb-installing.html

In MySQL Workbench go to
    Server -> Data Import -> Enter location of the folder the Schema dump is in
            -> Load Folder Contents 
    Select the speakfeel database
    Click Start Import

## Schema

Also available in the Database Schema SQL Text File

+---------------+-------------+------+-----+---------+----------------+

| Field         | Type        | Null | Key | Default | Extra          |

+---------------+-------------+------+-----+---------+----------------+

| player_id     | bigint(7)   | NO   | PRI | NULL    | auto_increment |

| jersey_number | bigint(7)   | YES  |     | NULL    |                |

| first_name    | varchar(30) | YES  |     | NULL    |                |

| last_name     | varchar(30) | YES  |     | NULL    |                |

| team          | varchar(30) | YES  |     | NULL    |                |

| pos           | varchar(30) | YES  |     | NULL    |                |

+---------------+-------------+------+-----+---------+----------------+

Since player_id's are auto-incremented, player_id's will only increase in subsequent web scrapes
if data where deleted and you want to reset where the player_id starts, run:

ALTER TABLE speakfeel.teams AUTO_INCREMENT = 1;

in the MySQL Workbench

To view your current table, use:

SELECT * from speakfeel.teams;

## Methodology

1) Associate every team name with it's respective table 
    store as string since the team name could be anything
2) Get the header names of the lowest level header in each table (since there can be multi level headers)
3) Headers aren't always in the same order, so we store a dictionary showing which column each header name is in
4) Using that dictionary, we can map each SQL database field to a value in the table
5) For every table, loop over every row. We create a dictionary that represents a record in the database. Each database field is associated with a value from the website's table
    a. split all names into first and last names
    b. look for special attributes in the tag, such as colspan, where the value in that tag can apply to more than one cell
    c. store each field in the appropriate column in the SQL database
	
Now, we have a database of players!

## Running the file

open WebScraper.py, and run Python in the terminal

## Output

Shows my Output when scraping from the Webpage

## Acknowledgments
* Jeffrey to answering my questions
* Lechuan and Kelly for interviewing
* YouTube tutorials
* Walmart, for selling cheap muffins
