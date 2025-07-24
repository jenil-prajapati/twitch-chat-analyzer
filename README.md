# 📈 Twitch Vibe Tracker: Real-Time Sentiment Analyzer

An end-to-end Python application that provides real-time sentiment analysis for any live Twitch stream. The Vibe Tracker connects directly to Twitch chat, analyzes the emotional tone of messages, and generates a post-session visualization, offering streamers and communities powerful insights into their collective mood during a broadcast.

---

## ✨ Core Features

- **Live Data Ingestion**: Connects to any public Twitch channel's chat via WebSockets to capture messages in real-time.  
- **Instant Sentiment Scoring**: Uses NLTK's VADER model to score the sentiment of each chat message as it appears.  
- **Interactive Channel Finder**: Features a user-friendly UI within the notebook to select from top live streamers or search for any channel manually.  
- **Post-Session Trend Analysis**: After collecting a set number of messages, it generates a time-series graph to visualize the chat's sentiment trend.  
- **Data Export**: Saves the collected messages and their sentiment scores to a `.csv` file for further offline analysis.  

---

## 🛠️ Setup Guide

This project is designed for a seamless setup in **Google Colab**.

### 1. Get Twitch API Credentials
To interact with the Twitch API, you need a Client ID and Client Secret.

- Go to the [Twitch Developer Console](https://dev.twitch.tv/console/apps).
- Navigate to **Applications > Register Your Application**.
- Set the **OAuth Redirect URL** to `http://localhost`.
- Note your **Client ID** and **Client Secret**.

### 2. Configure the Notebook
The notebook uses Colab's secret manager to keep your credentials secure.

- After opening the notebook, click the 🔑 **Secrets** icon in the left sidebar.
- Add the following secrets:
  - `TWITCH_CLIENT_ID`: Your application's Client ID.
  - `TWITCH_CLIENT_SECRET`: Your application's Client Secret.
  - `TWITCH_TOKEN`: You will generate this by running the initial cells in the notebook.

### 3. Execute the Notebook
Run the cells from top to bottom. The notebook will guide you through:

- Authenticating
- Selecting a channel
- Launching the analyzer  
- The final cell will render the sentiment graph.

---

## 🏗️ System Architecture

The application follows a clean, linear data flow:

1. **API Authentication**: The script first authenticates with the Twitch API using OAuth 2.0 to validate credentials and fetch a list of top streamers.  
2. **Real-Time Data Ingestion**: A persistent WebSocket connection is established with the Twitch IRC chat server (`wss://irc-ws.chat.twitch.tv:443`) to stream live messages.  
3. **NLP Processing**: Each incoming message is immediately passed to the NLTK VADER (Valence Aware Dictionary and sEntiment Reasoner) sentiment analysis engine, which returns a compound score from -1.0 (most negative) to +1.0 (most positive).  
4. **Data Aggregation**: The timestamp, username, message, and sentiment score for each message are appended to an in-memory list.  
5. **Data Visu**
