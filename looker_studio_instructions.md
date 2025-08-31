# Looker Studio Dashboard Instructions

This document explains how to connect your BigQuery analysis results to Looker Studio to create an interactive dashboard.

## Prerequisites

*   You have successfully run the `bigquery_ai_prototype.ipynb` notebook.
*   The analysis results are stored in a BigQuery table.

## Steps to Connect BigQuery to Looker Studio

1.  **Go to Looker Studio:** Navigate to [https://lookerstudio.google.com/](https://lookerstudio.google.com/).

2.  **Create a new Data Source:**
    *   Click on the **"Create"** button in the top left corner and select **"Data Source"**.
    *   Select the **"BigQuery"** connector.
    *   Authorize Looker Studio to access your BigQuery data if prompted.

3.  **Select Your Project and Table:**
    *   In the left panel, select the Google Cloud Project you used for the hackathon.
    *   Select the BigQuery dataset where your analysis results are stored.
    *   Select the table containing the analyzed chat messages.

4.  **Configure the Data Source:**
    *   Looker Studio will automatically detect the schema of your table.
    *   Ensure that the data types are correct (e.g., `toxicity_score` as a number, `sentiment` as a string).
    *   Click the **"Connect"** button in the top right corner.

5.  **Create a New Report:**
    *   After connecting the data source, click the **"Create Report"** button.
    *   You will be taken to the report editor with your BigQuery data available.

## Placeholder Dashboard URL

Once your report is created and published, you can share it with the judges. Here is a placeholder URL to include in your submission:

[https://lookerstudio.google.com/your-dashboard](https://lookerstudio.google.com/your-dashboard)

## Example Dashboard Components

Here are some ideas for charts and graphs to include in your dashboard:

*   **Toxicity Trend:** A time series chart showing the average toxicity score over time.
*   **Sentiment Distribution:** A pie chart showing the percentage of positive, negative, and neutral messages.
*   **Top Topics:** A bar chart showing the most frequently discussed topics.
*   **Message Table:** A table displaying the raw messages, allowing judges to see the AI analysis for each one.
