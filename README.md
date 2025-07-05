# Customer Insights Automation with Trustpilot and AI

This workflow automates the process of gathering and analyzing customer reviews from Trustpilot to generate detailed insights. It scrapes reviews for a specified company, uses a Python script with a K-means clustering algorithm to group similar feedback, and then leverages a Large Language Model (LLM) to summarize these clusters. The final, actionable insights are exported to a Google Sheet.

## Overview

Understanding customer feedback is crucial, but manually sifting through hundreds of reviews is time-consuming. [cite_start]This workflow solves that problem by providing a fully automated solution to discover popular feedback, opinions, and pain points from a large number of reviews[cite: 13, 18]. It identifies key topics and sentiments, allowing businesses to make data-driven decisions.

## Features

* [cite_start]**Web Scraping:** Fetches the latest reviews directly from a company's Trustpilot page[cite: 9].
* [cite_start]**Vector Storage:** Stores review data in a Qdrant vector database for similarity searches[cite: 10].
* [cite_start]**AI-Powered Clustering:** Applies a K-means clustering algorithm using a Python script to group similar reviews[cite: 13, 19].
* [cite_start]**Insight Generation:** Uses a state-of-the-art LLM to analyze each cluster and extract granular insights, sentiment, and suggested improvements[cite: 15, 20].
* [cite_start]**Data Export:** Appends the final, structured insights into a Google Sheet for easy access and reporting[cite: 6].
* [cite_start]**Subworkflow Architecture:** Separates the data ingestion and insight generation processes into two parts for better organization and demonstration[cite: 16].

## How It Works

1.  [cite_start]**Step 1: Starting Fresh:** The workflow begins by clearing any existing records for the selected company from the Qdrant vector store to ensure a fresh analysis[cite: 7, 8].
2.  **Step 2: Scraping TrustPilot:** It uses an HTTP Request node to scrape the most recent reviews from the company's Trustpilot page. [cite_start]The HTML node extracts key data points like author, rating, title, text, and date[cite: 9].
3.  **Step 3: Storing in Qdrant:** The extracted reviews are processed, converted into vector embeddings using OpenAI, and stored in a Qdrant collection. [cite_start]This allows for powerful similarity searches and filtering[cite: 10].
4.  **Step 4: Triggering the Insight Subworkflow:** A subworkflow is triggered to begin the analysis phase. [cite_start]This separation is optional but helps to demonstrate the two-part process[cite: 16].
5.  [cite_start]**Step 5: Filtering and Fetching Reviews:** The subworkflow queries the Qdrant database to find relevant reviews within a specific date range[cite: 11, 12].
6.  [cite_start]**Step 6: Clustering with Python:** The vector embeddings of the reviews are fed into a Python script that applies the K-means clustering algorithm, grouping similar reviews into clusters[cite: 13].
7.  [cite_start]**Step 7: Fetching Reviews by Cluster:** The workflow retrieves the full review data for each identified cluster[cite: 14].
8.  **Step 8: Generating Insights:** Each cluster of reviews is passed to an LLM (OpenAI's GPT-4o-mini) via the "Information Extractor" node. [cite_start]The LLM summarizes the reviews, determines the overall sentiment, and suggests improvements[cite: 15].
9.  [cite_start]**Step 9: Writing to Google Sheets:** The generated insights, along with the raw review data, are formatted and appended to a Google Sheet[cite: 6].

## Technologies Used

* n8n
* Qdrant
* Python (scikit-learn for K-means)
* OpenAI (for embeddings and insight generation)
* Google Sheets

## Setup & Configuration

1.  **Qdrant:** Set up a Qdrant instance and create a collection named `trustpilot_reviews`. Add your Qdrant API credentials in n8n.
2.  **OpenAI:** Add your OpenAI API key to the `Embeddings OpenAI` and `OpenAI Chat Model` nodes.
3.  **Google Sheets:** Authenticate your Google account and provide the Sheet ID in the `Export To Sheets` node.
4.  [cite_start]**Company ID:** In the `Set Variables` node, change the `companyId` value to the Trustpilot handle of the company you want to analyze (e.g., `www.freddiesflowers.com`)[cite: 4, 21].
5.  [cite_start]**Python Environment:** The Code Node will automatically download the required Python packages on the first run, which may cause a slight delay[cite: 117].

## How to Use

* Run the main workflow by clicking 'Test workflow' from the n8n editor.
* The first part will scrape and store the reviews, then trigger the insights subworkflow.
* Check the specified Google Sheet for the final report. You can find a sample sheet [here](https://docs.google.com/spreadsheets/d/e/2PACX-1vQ6ipJnXWXgr5wlUJnhioNpeYrxaIpsRYZCwN3C-fFXumkbh9TAsA_JzE0kbv7DcGAVIP7az0L46_2P/pubhtml).

**Of course. Here is a short, professional description you can add to the end of each README file.

-----

## 🚀 Need Custom Automation? Let's Talk\!

If you're looking to implement powerful business automations, custom integrations, or full-stack projects like this one, I'm available for consulting. Let's discuss how I can help you streamline your business processes.

Schedule a free 15-minute coffee chat to explore your project needs.


[Book a chat with me😁](https://cal.com/closegem/coffee-chat)
