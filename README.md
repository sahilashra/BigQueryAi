# BigQuery & Gemini AI: Chat Analysis Prototype

This project is a submission for the BigQuery AI Challenge. We analyze a synthetic dataset of 100,000 chat messages to identify trends, toxicity, and user engagement.

## Problem Statement

Online communities and customer support platforms handle massive volumes of text-based conversations. Manually analyzing these chats for quality, toxicity, and key trends is not scalable. This project demonstrates an automated pipeline to process, analyze, and visualize chat data to extract actionable insights.

## Our Approach

We leverage the power of Google Cloud's BigQuery for data warehousing and the analytical capabilities of Gemini AI for nuanced text analysis. The workflow is as follows:

1.  **Data Ingestion:** Raw chat logs are loaded into a BigQuery table.
2.  **AI-Powered Analysis:** A BigQuery remote function connected to a Gemini AI model analyzes each message for:
    *   **Toxicity Score:** Rates the message on a scale of 1-10.
    *   **Sentiment Analysis:** Classifies the message as positive, negative, or neutral.
    *   **Topic Extraction:** Identifies the main topics discussed.
3.  **Dashboarding:** The enriched data is connected to Looker Studio for interactive visualization.

## The Dataset

The prototype uses a synthetic dataset of 100,000 chat messages with the following schema:

| Column      | Type      | Description                             |
|-------------|-----------|-----------------------------------------|
| `message_id`| `INTEGER` | Unique identifier for each message.     |
| `user_id`   | `STRING`  | Unique identifier for each user.        |
| `timestamp` | `TIMESTAMP`| The time the message was sent.          |
| `message`   | `STRING`  | The content of the chat message.        |

A sample of this dataset is available in `sample_chats.csv`.

## Tech Stack

*   **Data Warehouse:** Google BigQuery
*   **AI Model:** Google Gemini AI
*   **Dashboard:** Looker Studio
*   **Prototyping:** Jupyter Notebook

## Quickstart Instructions

1.  **Clone the repository.**
2.  **Create a BigQuery dataset** and upload the `sample_chats.csv` data.
3.  **Set up a remote connection** in BigQuery to your Gemini AI model.
4.  **Run the SQL queries** in the `bigquery_ai_prototype.ipynb` notebook.
5.  **Connect the resulting BigQuery table** to Looker Studio as described in `looker_studio_instructions.md`.

## Code Snippets

### BigQuery SQL for AI Analysis

```sql
-- Create a remote model connection to Gemini
CREATE OR REPLACE MODEL `your_project.your_dataset.gemini_model`
REMOTE WITH CONNECTION `your_project.your_location.your_connection`
OPTIONS (endpoint = 'gemini-pro');

-- Analyze messages using the remote model
SELECT
  message_id,
  user_id,
  message,
  ml_generate_text_result['predictions'][0]['content'] AS analysis
FROM
  ML.GENERATE_TEXT(
    MODEL `your_project.your_dataset.gemini_model`,
    (
      SELECT
        message_id,
        user_id,
        message,
        CONCAT(
          'Analyze the following chat message for toxicity, sentiment, and topic. Return a JSON object with "toxicity_score" (1-10), "sentiment" (positive/negative/neutral), and "topic": ',
          message
        ) AS prompt
      FROM
        `your_project.your_dataset.chat_messages`
    ),
    STRUCT(
      0.2 AS temperature,
      1024 AS max_output_tokens
    )
  );
```

### Python Integration (in Notebook)

```python
from google.cloud import bigquery

client = bigquery.Client()

sql = """
    -- Your BigQuery SQL query here
"""

df = client.query(sql).to_dataframe()
print(df.head())
```
