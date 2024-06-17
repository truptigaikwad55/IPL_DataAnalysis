IPL Data Analysis Project
Overview
This project involves analyzing Indian Premier League (IPL) data using Apache Spark with Scala. The goal is to derive insights and perform various analyses on the IPL matches data. We use Spark SQL for querying the data and perform statistical analysis to understand player performances, match outcomes, and other key metrics.

Project Structure
css
Copy code
IPL_Data_Analysis/
├── data/
│   ├── ball_by_ball.csv
│   ├── matches.csv
│   ├── players.csv
│   └── teams.csv
├── src/
│   ├── main/
│   │   ├── scala/
│   │   │   ├── DataCleaning.scala
│   │   │   ├── ExploratoryAnalysis.scala
│   │   │   └── PlayerPerformanceAnalysis.scala
│   │   └── resources/
│   └── test/
│       └── scala/
├── notebooks/
│   ├── DataCleaning.ipynb
│   ├── ExploratoryAnalysis.ipynb
│   └── PlayerPerformanceAnalysis.ipynb
├── README.md
├── build.sbt
└── project/
    ├── build.properties
    └── plugins.sbt
Datasets
ball_by_ball.csv: Contains ball-by-ball data for each match.
matches.csv: Contains details about the matches played.
players.csv: Contains information about the players.
teams.csv: Contains information about the teams.
Analysis Performed
Data Cleaning:

Handling missing values.
Correcting data types.
Removing duplicates.
Exploratory Data Analysis (EDA):

Analyzing distributions of runs scored, wickets taken, and other metrics.
Identifying trends over different seasons.
Player Performance Analysis:

Calculating average runs per ball and total wickets taken in the powerplay.
Identifying the most economical bowlers and best-performing batsmen.
Sample Query
Here's an example of a query used to identify the most economical bowlers in the powerplay overs (overs 1-6):

scala
Copy code
val economicalBowlersPowerplay = spark.sql("""
    SELECT p.Player_Name, AVG(b.Runs_Scored) AS avg_runs_per_ball,
    COUNT(b.bowler_wicket) AS total_wickets
    FROM ball_by_ball b
    JOIN player_match pm ON b.Match_id = pm.Match_Id AND b.Bowler = pm.Player_Id
    JOIN player p ON pm.Player_Id = p.Player_Id
    WHERE b.Over_id <= 6
    GROUP BY p.Player_Name
    HAVING COUNT(*) > 120
    ORDER BY avg_runs_per_ball, total_wickets DESC
""")
How to Run
Clone the Repository:

bash
Copy code
git clone https://github.com/yourusername/IPL_Data_Analysis.git
cd IPL_Data_Analysis
Set Up Environment:

Ensure you have Scala and Spark installed.
Open the project in IntelliJ IDEA.
Build the Project:

Use sbt to build the project:
bash
Copy code
sbt clean compile
Run the Analyses:

Data Cleaning:
scala
Copy code
sbt "runMain com.example.DataCleaning"
Exploratory Analysis:
scala
Copy code
sbt "runMain com.example.ExploratoryAnalysis"
Player Performance Analysis:
scala
Copy code
sbt "runMain com.example.PlayerPerformanceAnalysis"
Use Jupyter Notebooks (optional):

Open and run the notebooks in the notebooks/ directory to interactively explore and analyze the data.
Results
The results of the analysis include:

Identification of top-performing players.
Insights into team performance trends.
Visualizations of key metrics over different seasons.
Contributing
If you'd like to contribute to this project, please fork the repository and use a feature branch. Pull requests are warmly welcome.

License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgements
Thanks to the IPL for providing the data.
Special thanks to the contributors and the open-source community.
