# Data Analytics Capstone
### Chaz Darvish

## Speedrun Efficiency Analysis

This project aims to perform a time series analysis on the top scoring speedruns from speedrun.com. The goal is to determine when these speedruns reach a point of "efficiency" using a piecewise linearfit. Then, a jackknife resample is used to get a 99% confidence interval on that efficiency point.

### Files in the Repository

This project includes several files that are used for different purposes:

1. `environments.yml`: This file contains the conda environment configuration. It lists all the Python packages that are required to run the notebook.

2. `speedrun_data.csv`: This is the main data file for the project. It contains the speedrun data that is analyzed in the notebook.

3. `speedrun_notebook.ipynb`: This is the Jupyter notebook file where all the data analysis is performed. It includes all the code, as well as explanations and visualizations.

4. `efficiency_data.csv` (deprecated): This is a deprecated metadata file that was used in an earlier version of the project for a trend analysis. It's not used in the current analysis but is kept in the repository for reference.

### Table of Contents
1. Game Selection
2. Libraries
3. API Variables
4. Functions
5. API Run Data
6. Data Preparation
7. Efficiency Point Plot Based on Linear Fit
8. Metrics
9. Jackknife Resampling
10. Graphing Jackknife Confidence Interval

### 1. Game Selection
'Elden Ring' is selected for analysis. The game can be changed, using the url of that game's page. For this example: `https://www.speedrun.com/eldenring`

### 2. Libraries
Libraries such as `os`, `time`, `json`, `datetime`, `requests`, `pandas`, `matplotlib`, `numpy`, `pwlf`, and `sklearn` are imported.

### 3. API Variables
Variables for the API GET statement are defined.  These variables include the base URL for the speedrun.com API, the status of the runs we’re interested in (verified), the platform for the runs (PC), the order in which we want the runs (by date), the direction of the order (ascending), and the maximum number of results per page.

### 4. Functions
1. `get_game_id(game_name)`: This function retrieves the game ID for a specific game from the speedrun.com API. It sends a GET request to the API and returns the game ID.
   
2. `get_categories(game_id)`: This function retrieves the categories for a specific game from the speedrun.com API. It sends a GET request to the API and returns a dictionary of categories for the game.
   
3. `get_runs_for_category(game_id, category_id, category_name, category_type)`: This function retrieves the runs for a specific category of a game from the speedrun.com API. It sends a GET request to the API and returns a list of runs for the category.
   
4. `efficiency_graph(game_name, top_category, top_type, csv_df, my_pwlf)` is defined to plot the efficiency point.

5. `jackknife_efficiency_graph(jackknife_efficiency_points, ci_lower_date, ci_upper_date, elbow_date)` is defined to plot the jackknife resampled efficiency points.

### 5. API Run Data
The game ID and the categories for the game are obtained. The runs for each category are retrieved and stored in a DataFrame.

### 6. Data Preparation
The data is prepared for linear fit. The DataFrame is filtered to only include runs from the top category and top category type. A piecewise linear fit is initialized with the date and top score data.

### 7. Efficiency Point Plot Based on Linear Fit
The efficiency point is graphed based on the linear fit.

### 8. Metrics
Exploratory data analysis is performed on metrics such as the number of runs to the efficiency point, the percentage of runs complete at efficiency, the number of days to the efficiency point, the total number of days in the data, the percentage of days to efficiency out of total days, the score at efficiency, and the latest top score.

### 9. Jackknife Resampling
Jackknife resampling is performed to determine the confidence level of the efficiency point.

### 10. Graphing Jackknife Confidence Interval
We graph the Jackknife resampled efficiency points and the 99% confidence interval using the `jackknife_efficiency_graph(jackknife_efficiency_points, ci_lower_date, ci_upper_date, elbow_date)` function.