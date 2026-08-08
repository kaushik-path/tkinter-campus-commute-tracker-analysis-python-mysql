# Tkinter-Campus-Commute-Tracker-Analysis-Python-MySql 

A desktop application that turns a daily-commute survey into an interactive tool — load the data, explore it, add new responses, store everything in MySQL, and generate visual breakdowns of how people actually get around.

## Table of Contents
- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Dataset](#dataset)
- [Tools and Technologies](#tools-and-technologies)
- [Methods](#methods)
- [Key Insights](#key-insights)
- [Dashboard/Model/Output](#dashboardmodeloutput)
- [How to Run this Project?](#how-to-run-this-project)
- [Results & Conclusion](#results--conclusion)
- [Future Work](#future-work)
- [Author & Contact](#author--contact)

## Overview

The Campus Commute Tracker & Analysis app is a Python desktop tool built with Tkinter that manages a commuter survey end-to-end. It's not just a static chart — it's a working tool with a login screen, a live data table, search/filter controls, a form to capture new responses, a MySQL persistence layer, and a graphing window that renders gender, age, and transport-mode breakdowns on demand.

## Problem Statement

Commute data — how people travel, what they spend, how safe or satisfied they feel — is usually scattered across spreadsheets that no one revisits. The goal here was to build a single application where that data could be loaded, added to, filtered, stored persistently, and visualized, without needing separate tools for each step.

## Dataset

- **Source:** A self-collected commuter survey (`TravelActivity.csv`)
- **Size:** 40 respondents, 22 fields per record
- **Fields include:** Age, Gender, Occupation, Location, Distance, Mode of transport, Frequency, Commute time, Commute days, Daily/Monthly cost, Satisfaction, Cleanliness, Safety, Accessibility, environmental importance, willingness to switch modes, apps used, payment method, and impact on daily schedule

## Tools and Technologies

- **Python** — core application logic
- **Tkinter / ttk** — GUI framework (login page, data table, forms, filters)
- **Pandas** — data loading, filtering, and transformation
- **Matplotlib** — bar and pie chart generation, embedded in Tkinter via `FigureCanvasTkAgg`
- **Seaborn** — statistical visualization support
- **MySQL (mysql-connector-python)** — persistent storage with duplicate-safe inserts

## Methods

1. **Login gate** — a simple authentication screen before the main app loads
2. **Data ingestion** — CSV upload into a Pandas DataFrame, rendered in a scrollable `Treeview` table
3. **Manual entry** — a structured form (dropdowns for categorical fields like Mode, Safety, Satisfaction) to add new survey responses on the fly
4. **Filtering** — search by name, filter by age, filter by gender, applied directly against the loaded DataFrame
5. **Persistence** — data is pushed to a MySQL table (`commute_data`), with a duplicate check before every insert so the same response isn't stored twice
6. **Retrieval** — a dedicated function pulls all stored records back from MySQL into the app
7. **Visualization** — a separate graph window renders bar and pie charts for gender distribution, age distribution, and transport mode distribution

## Key Insights

Based on the current 40-response dataset:

- **Bike is the most common commute mode** (14 respondents), followed closely by **Walking and Bus** (11 each) — cars are rare (1 respondent), suggesting a sample dominated by short-to-mid-distance, low-cost commuting.
- **Satisfaction skews neutral-to-positive**: 17 respondents are "Neutral," but satisfied + very satisfied (14) outnumber dissatisfied + very dissatisfied (9).
- **Openness to change is high** — 31 of 40 respondents said "Yes" to switching commute modes if a better option existed, with only 3 firmly saying "No."
- **Perceived safety is mixed**: "Safe" and "Neutral" are tied at 14 responses each, with a small but present "Unsafe/Very Unsafe" group (5 total) worth investigating further.

## Dashboard/Model/Output

The app's "View Graphs" window outputs:
- Gender distribution (bar + pie)
- Age distribution (bar + pie)
- Transport mode distribution (bar + pie)

All charts render inside a scrollable canvas within the Tkinter window itself — no external dashboard tool required.

## How to Run this Project?

**Prerequisites:**
- Python 3.x
- MySQL Server running locally (only required if you want to use the save/fetch-to-database features)

**Steps:**

```bash
# 1. Clone the repository
git clone https://github.com/kaushik-path/tkinter-campus-commute-tracker-analysis-python-mysql.git
cd tkinter-campus-commute-tracker-analysis-python-mysql

# 2. Install dependencies
pip install pandas matplotlib seaborn mysql-connector-python

# 3. Open and run the notebook
jupyter notebook Ca4Tkinker.ipynb
# Run all cells — this launches the Tkinter application window
```

**Using the app:**
1. Log in on the launch screen
2. Click **Load CSV File** and select `TravelActivity.csv`
3. Use the search/filter controls to explore the data, or **Add Data** to insert new responses
4. Click **Save to Database** to persist records to MySQL (update the host/user/password/database in the code to match your local setup first)
5. Click **View Graphs** for the visual breakdown

> **Note:** Database credentials in the current notebook are hardcoded placeholders for local development. Update `host`, `user`, `password`, and `database` in `save_all_data_to_database()` and `fetch_data_from_database()` before running against your own MySQL instance — never commit real credentials.

## Results & Conclusion

The project demonstrates a full, working pipeline from raw survey data to a queryable, visual, database-backed application — covering data ingestion, manual data entry, filtering, SQL persistence, and visualization in a single Python GUI. It shows practical use of Pandas for data handling, Tkinter for interface design, and MySQL for storage, tying together skills that sit at the intersection of data analysis and application development.

## Future Work

- Parameterize the MySQL connection (config file or environment variables) instead of hardcoded credentials
- Add more chart types (e.g., cost vs. satisfaction, safety vs. mode) for deeper cross-field analysis
- Add data validation on the entry form (e.g., numeric-only age field)
- Package the app as a standalone executable for easier distribution
- Migrate the login system to proper hashed authentication if the app is ever shared beyond local use

## Author & Contact

**Kaushik Pathak**
📧 Feel Free to Reach out [LinkedIn](https://www.linkedin.com/in/kaushikpath/) | [GitHub](https://github.com/kaushik-path)

*Feel free to open an issue or reach out for questions, feedback, or collaboration.*
