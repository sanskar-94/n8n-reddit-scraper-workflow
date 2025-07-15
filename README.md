# n8n Reddit Data Scraper Workflow 🤖

This repository contains an n8n workflow designed to automatically scrape and categorize Reddit posts from specified subreddits. It leverages Google Gemini AI for intelligent summarization and filters posts based on upvote ratios before storing the relevant data in Airtable.

## Problem Statement

Manually tracking popular or relevant posts across multiple Reddit subreddits can be time-consuming. This workflow automates the process, allowing users to efficiently extract, summarize, and store high-engagement content for further analysis or archiving.

## Features ✨

* **Scheduled Scraping**: Automatically fetches new posts at predefined intervals.
* **Multi-Subreddit Support**: Configured to scrape from "technology", "Finance", and "ArtificialInteligence" subreddits.
* **AI-Powered Summarization**: Utilizes Google Gemini to generate concise, one-line summaries of Reddit posts.
* **Upvote Ratio Filtering**: Only processes posts with an upvote ratio greater than 0.93 to focus on high-quality content.
* **Airtable Integration**: Stores extracted data (title, author, score, upvote ratio, summary) into organized Airtable bases.

## Workflow Overview 📊

The workflow operates as follows:
1.  **Schedule Trigger**: Initiates the workflow at a set time (e.g., daily at 11 AM).
2.  **Reddit Nodes**: Fetches the latest 3 "new" posts from the configured subreddits (Technology, Finance, Artificial Intelligence).
3.  **AI Agent Nodes**: For each post, an AI Agent (powered by Google Gemini) is prompted to extract specific details and generate a summary if the upvote ratio is above 0.93. Otherwise, it returns a "skip" flag.
4.  **Code Nodes**: Parses the JSON output from the AI Agent, handling potential formatting issues and ensuring valid JSON.
5.  **If Nodes**: Checks the "skip" flag. If `skip` is false (meaning the upvote ratio was high enough and data was extracted), it proceeds.
6.  **Airtable Nodes**: Creates new records in designated Airtable bases ("Tech", "Finance", "Artificial Intelligence") with the extracted post details.

## Setup 🛠️

1.  **Import the workflow.json file** into your n8n instance.
2.  **Ensure you have the necessary credentials configured in n8n**:
    * Reddit OAuth2 API
    * Google Gemini (PaLM) API
    * Airtable Personal Access Token
3.  **Verify Airtable Base and Table IDs**: The workflow is configured to use Airtable Base ID `appVHHKsatng2Tsle` and specific table IDs for "Artificial Intellingence" (`tbl3kAVn8kywaT8kf`), "Tech" (`tblgLpuWVk7MheR3B`), and "Finance" (`tblGEZJtkkDJ5RDwM`). Adjust these in the Airtable nodes if your Airtable setup differs.

---

### Workflow Screenshot:

![n8n Reddit Data Scraper Workflow](screenshot.png)
