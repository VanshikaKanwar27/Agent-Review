#**Yelp AgentSociety: Predictive Rating System**

Developed by: Vanshika (Student ID: w11421407)

Framework: CrewAI & Ollama (Qwen2.5:7b)

**Project Overview**
This repository contains a deterministic data analysis pipeline built with CrewAI and powered by a local instance of the Qwen2.5:7b model via Ollama. 
The system is designed to perform high-precision profiling and rating prediction on Yelp datasets while strictly adhering to a grounded execution loop.

**Technical Architecture**
The pipeline utilizes a multi-agent orchestration strategy to ensure data integrity and prevent hallucinations.
By leveraging local computation, it maintains privacy and provides a cost-effective alternative to cloud-based LLM services.

**LLM Model: Qwen2.5:7b (Running locally via Ollama at http://localhost:11434)**

**Embedding Model: BAAI/bge-small-en-v1.5**

**Orchestration: CrewAI (Sequential Process)**

**Inference Settings: Temperature 0.0 (Strictly deterministic)**

 **Multi-Agent Workflow**
The analysis is performed by three specialized agents defined in config/agents.yaml that operate in a sequential chain:

**User Profiler**: Responsible for retrieving historical data and reviewing habits for a specific user.
It synthesizes past review sentiments and category preferences.

**Item Analyst**: Conducts a detailed features analysis of the target business, including its attributes (e.g., WiFi, Parking), categories, and location data.

**Prediction Modeler**: Synthesizes the outputs from the Profiler and Analyst to predict the star rating and generate a realistic review text that matches the user's established persona.

**Custom Tools**
To guarantee accuracy, the system uses high-precision tools implemented in crew.py for exact data retrieval:

**search_user_data**: Performs an exact ID match against the user dataset to retrieve raw JSON records.

**search_item_data**: Retrieves exact business features by item ID.

**search_review_data**: Filters historical review data to provide the LLM with grounded examples of past interactions.

**Output:** 
The final prediction is saved to report.json in the root directory.
This file contains the predicted stars and text fields, formatted for automated evaluation and MSE (Mean Squared Error) calculation.
