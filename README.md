# Bitovi Blog AI Agent - n8n RAG Workflow

## Overview

This n8n workflow automates the ingestion, processing, and indexing of Bitovi's blog articles. An AI agent then leverages this data, using a RAG pipeline, to provide contextually relevant and source-referenced answers to user queries.

## Core Features

*   **Automated Blog Ingestion:** Periodically fetches and processes new or updated articles from the Bitovi blog via its sitemap.
*   **Storage Solution:**
    *   **PostgreSQL:** Stores structured article metadata.
    *   **Supabase (with pgvector):** Stores vector embeddings of article content chunks for efficient semantic search.
*   **Intelligent RAG Pipeline:**
    *   **Semantic Search:** Utilizes the Supabase vector store for queries requiring contextual understanding of blog content.
    *   **Text-to-SQL Querying:** Empowers the agent to query the PostgreSQL for metadata-based questions (e.g., latest articles, counts by topic/author).
    *   **Topic Discovery:** A dedicated tool allows the agent to list all unique blog topics, aiding in query formulation and user guidance.
*   **Grounded & Referenced Responses:** The agent is designed to provide answers derived solely from the blog content and to include source URLs for verification.

## Workflow Structure

The n8n workflow is divided into two main parts:

1.  **Article Ingestion & Processing:**
    *   **Fetch & Filter:** Identifies new or updated articles.
    *   **Store Metadata:** Saves article details (URL, title, author, dates, topics, markdown content) to PostgreSQL.
    *   **Vectorize & Index:** Chunks markdown content, generates embeddings using OpenAI, and stores them in Supabase for RAG.
2.  **RAG AI Agent Interface:**
    *   **Input:** User queries are received via a Webhook.
    *   **Agent Orchestration:** A central AI Agent node (leveraging an OpenAI chat model) interprets queries, selects appropriate tools (Semantic Search, Text-to-SQL, List Topics), and synthesizes responses.
    *   **Memory:** Incorporates chat memory for conversational context.
    *   **Output:** Delivers response to the user, including source links.

## Technical Stack

*   **Workflow Automation:** n8n
*   **Structured Database:** PostgreSQL
*   **Vector Database:** Supabase (utilizing the pgvector extension)
*   **LLM & Embeddings:** OpenAI API

## Running the Project

### Prerequisites

1.  **n8n Instance:** A running n8n instance (self-hosted as per exercise guidelines).
2.  **PostgreSQL Database:** Accessible PostgreSQL server.
3.  **Supabase Project:** A Supabase project with the `pgvector` extension.
4.  **OpenAI API Key:** An API key for OpenAI (for embeddings and the chat model).
5.  **Environment Variables/Credentials:** Configure n8n credentials for PostgreSQL, Supabase, and OpenAI.

### Setup

1.  **Import Workflow:** Import the provided n8n workflow JSON file into your n8n instance.
2.  **Configure Credentials:** Ensure all necessary credentials (Postgres, Supabase, OpenAI) are correctly set up and linked within the imported workflow nodes.
3.  **Database Schema Setup:** Make sure to run the initial nodes to set up database tables.
4.  **Initial Data Ingestion:** Manually trigger the "Schedule Trigger" node in the workflow to populate the databases for the first time.
<!---
## Demonstration

Please refer to the submitted demo video 
-->
