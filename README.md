**FDA Drug Adverse Events ETL Project**

This project involves extracting data on drug adverse events from the
[FDA\'s open-source data platform](https://open.fda.gov/), transforming
it using Python Pandas, and loading it into Snowflake for further
analysis and visualization. The entire ETL process is orchestrated using
Apache Airflow and Docker, with data visualization performed using
Tableau Desktop. Below are the steps and configurations required to set
up and run this project.

**Table of Contents**

1.  [[Project Overview]{.underline}](#project-overview)

2.  [[Tools and Services Used]{.underline}](#tools-and-services-used)

3.  [[API Details]{.underline}](#api-details)

4.  [[Data Extraction]{.underline}](#data-extraction)

5.  [[Data Storage]{.underline}](#data-storage)

6.  [[Data Modeling]{.underline}](#data-modeling)

7.  [[ETL Workflow]{.underline}](#etl-workflow)

8.  [[Setup Instructions]{.underline}](#setup-instructions)

9.  [[Running the Project]{.underline}](#running-the-project)

10. [[Data Visualization with Tableau
    Desktop]{.underline}](#data-visualization-with-tableau-desktop)

**Project Overview**

This project involves:

-   Designing an API to retrieve data from the FDA\'s open-source data
    platform.

-   Building a Python script to fetch and process the data.

-   Storing the data in AWS S3.

-   Modeling and storing the transformed data in Snowflake.

-   Orchestrating the entire ETL process using Airflow.

-   Visualizing the data using Tableau Desktop.

**Tools and Services Used**

-   **Python**: For scripting and data processing.

-   **Pandas**: For data manipulation and analysis.

-   **AWS S3**: As a data lake for storing raw and transformed data.

-   **Snowflake**: For data modeling and storage.

-   **Apache Airflow**: For orchestrating the ETL workflow.

-   **Astro CLI**: For managing and interacting with Airflow
    environments.

-   **Docker**: For containerizing the Airflow environment.

-   **Visual Studio Code**: As the development environment.

-   **Tableau Desktop**: For data visualization.

-   **ODBC Snowflake Driver**: For connecting Tableau to Snowflake.

**Architecture Diagram**

![A diagram of a software system Description automatically generated
with medium confidence](media/image1.png){width="6.741666666666666in"
height="3.658333333333333in"}

**API Details**

-   **Base URL**: https://api.fda.gov/drug/event.json

-   **Search Query**: receivedate:\[20200101 TO 20201231\] AND
    occurcountry:\"US\" AND \_missing\_:companynumb

The API retrieves data reported directly from consumers in the United
States in the year 2020 who had adverse reactions to suspected drugs.

**Data Extraction**

-   Build a Python script to fetch 80,000 rows using the API. Implement
    paging as the max rows the API can fetch is 1000.

-   Use Pandas to extract only the required columns and handle null
    values.

-   Handle missing values and update fields as per the data shown on the
    [FDA page.](https://open.fda.gov/apis/drug/event/)

**Data Storage**

-   Use AWS S3 as a data lake.

-   Create an S3 bucket with different folders for raw and cleaned data.

**Data Modeling**

-   Create SQL worksheets in Snowflake for designing database schema.

-   Create new schemas, databases, and tables to handle the transformed
    data from S3.

**ETL Workflow**

Create an Airflow DAG script to orchestrate the ETL process with the
following tasks:

1.  **Check API Availability**: Ensure the API is available.

2.  **Extract Data**: Fetch FDA drug adverse events data from the API,
    load it into S3, and push the S3 path to Xcom for reference.

3.  **Transform Data**: Pull the S3 path from Xcom, extract the raw data
    from S3, transform and normalize it, and load the transformed data
    into a different S3 folder.

4.  **Create Snowflake Stage**: Set up a Snowflake stage for the
    transformed data.

5.  **Load Data into Snowflake**: Copy the transformed data into
    Snowflake tables using the stage from Task 4.

**Setup Instructions**

1.  **Install Astro CLI**: A tool provided by Astronomer to help manage
    and interact with Airflow environments, allowing you to run Airflow
    locally in Docker containers.

2.  **Install Docker Desktop**: Update the .wslconfig file to use the
    maximum CPU and RAM possible (minimum 6 processors and 6GB RAM).

3.  **Update Airflow Configurations**: Modify the .env and
    requirements.txt files as shown in how_to_run file.

4.  **Start Docker Desktop**: Initialize the Astro environment using
    Astro commands in Visual Studio Code as detailed in how_to_run file.

**Running the Project**

1.  **Run Airflow in Docker**: Use Astro commands as detailed in
    how_to_run file

2.  **Access Airflow**: Navigate to http://localhost:8080.

3.  **Navigate to Airflow Connections**: Create HTTP, AWS, and Snowflake
    connections.

4.  **Trigger the Airflow DAG**.

**Data Visualization with Tableau Desktop**

Once the data is loaded into Snowflake:

1.  **Install the ODBC Snowflake Driver**: Required for Tableau Desktop
    to connect to Snowflake.

2.  **Create an Extract Connection**: Connect Tableau Desktop to
    Snowflake.

3.  **Data Modeling in Tableau**: Create a star schema and define
    relationships between the cleaned data tables.

4.  **Create Visualizations**: Use Tableau Desktop to process and
    visualize the data.

> **Checkout the visualization at** [2020_Drug_adverse_events \| Tableau
> Public](https://public.tableau.com/app/profile/ravi.shankar.p.r/viz/2020_Drug_adverse_events/Dashboard3)
>
> **Checkout how_to_run file for detail steps to run this project.**
