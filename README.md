HR Employee Attrition Analysis

This project analyzes HR employee attrition data using Apache Spark (PySpark) and saves the processed data to a PostgreSQL database. The analysis includes basic data cleaning, renaming columns for clarity, and running SQL queries to extract insights such as average age, the most popular department, common education level, and median distance from home.

This project aims to:

Load HR employee attrition data from a CSV file.

Clean and transform the data (e.g., drop irrelevant columns, rename columns, remove duplicates, and handle null values).

Perform various SQL-based analyses using Spark SQL to gather insights.

Save the final processed DataFrame into a PostgreSQL database for further use.

Prerequisites

Ensure the following dependencies are installed and configured before running the code:

Java 8 (for PySpark)

Apache Spark (installed locally or in your environment)

PostgreSQL Database (for saving the output data)

Python 3.x (with PySpark and other required libraries)

PostgreSQL JDBC driver (for Spark to connect to the PostgreSQL database)

The following Python libraries are required:

bash
Copy
Edit
pip install pyspark
pip install psycopg2
Setup

Install Java 8: Ensure Java 8 is installed on your machine and set the JAVA_HOME environment variable.

Set up Apache Spark: Download and install Apache Spark, or configure Spark in your environment if using a cloud-based service like Databricks or AWS EMR.

Set up PostgreSQL: Ensure your PostgreSQL database is running, and create a database where the processed data will be saved.

In your script, replace the database connection details with your own:

python
Copy
Edit
url = "jdbc:postgresql://your-database-url:5432/postgres"
properties = {
    "user": "postgres",
    "password": "your-password",
    "driver": "org.postgresql.Driver"
}
Running the Code

Place the HR-Employee-Attrition.csv file in the specified path on your machine or modify the Hr_Employee variable to point to the correct file path.

Run the script. It will:

Read the CSV file.

Clean the data (drop redundant columns, rename columns, remove duplicates, handle null values).

Perform analysis using Spark SQL to get insights.

Save the cleaned and processed data to PostgreSQL.

bash
Copy
Edit
python your_script.py
SQL Queries

The following SQL queries are executed on the cleaned data:

Average Age: Finds the average age of employees.

sql
Copy
Edit
SELECT AVG(age) AS avg_age FROM attrition_view
Most Popular Department: Finds the department with the most employees.

sql
Copy
Edit
SELECT Department, COUNT(*) AS count FROM attrition_view GROUP BY Department ORDER BY count DESC LIMIT 1
Most Common Education Level: Finds the most common level of education.

sql
Copy
Edit
SELECT education_field, COUNT(*) AS count FROM attrition_view GROUP BY education_field ORDER BY count DESC LIMIT 1
Median Distance from Home: Finds the median distance from home using the percentile_approx function.

sql
Copy
Edit
SELECT percentile_approx(distance_from_home, 0.5) AS median_dist FROM attrition_view
Saving Data
The processed data is saved to a PostgreSQL database. Ensure that you provide the correct URL, username, and password for your PostgreSQL instance. The DataFrame is written to a table named HR_att.

python
Copy
Edit
Attrition_df.write.jdbc(url=url, table="HR_att", mode="overwrite", properties=properties)
License
This project is licensed under the MIT License - see the LICENSE file for details.
