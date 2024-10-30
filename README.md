
# Chatbot using LangGraph, LangChain, and Groq

This project demonstrates the construction of a chatbot pipeline using **LangGraph** for graph-based logic, **LangChain** for integration with tools like Wikipedia and Arxiv, and  **Groq** 's Llama-3 model for generating responses. The chatbot uses LangGraph’s capabilities to dynamically manage conversation flow with external API support from Wikipedia and Arxiv.

## Table of Contents

* [Installation](#installation)
* [Project Overview](#project-overview)
* [Features](#features)
* [Pipeline Details](#pipeline-details)
* [Usage](#usage)
* [Graph Visualization](#graph-visualization)

## Installation

Make sure to install all required packages:

```
!pip install -q langgraph langsmith langchain langchain_community langchain_groq arxiv wikipedia
```


## Project Overview

This project uses **LangGraph** to set up an interactive conversational agent with the following components:

1. **Wikipedia** and **Arxiv** as external data sources for answering user queries.
2. **LangGraph** to create a dynamic flow of conversation.
3. **ChatGroq** 's Llama-3 model as the main large language model to process user queries and utilize external tools when necessary.

## Features

* **Modularized Structure** : Uses LangGraph to organize nodes and edges in the graph flow.
* **Tool Integration** : Uses LangChain and LangChain_Community for invoking tools like Wikipedia and Arxiv for retrieving information.
* **Scalable Chatbot Logic** : Uses LangGraph's StateGraph to dynamically adjust flow based on input conditions.
* **Groq Integration** : Employs ChatGroq’s Llama-3 model for high-quality responses.

## Pipeline Details

### 1. **External Tool Setup**

* **Wikipedia** and  **ArxivAPIWrapper** : Tools configured to fetch specific information based on user queries. Here, Wikipedia is queried for general knowledge, while Arxiv serves research and academic query needs.

### 2. **LangGraph Application Design**

* **StateGraph** : Implements a graph-based structure where nodes and conditions control the conversation flow.
* **Tools Node** : Directs the chatbot to external tools when specific conditions (like a named entity query) are detected.
* **Chatbot Node** : Handles primary user interactions, invoking the necessary LLM responses or external tools as per the input message.

### 3. **Model Integration with Groq**

* The `ChatGroq` model (Llama-3) is used for generating responses.
* Tools are dynamically invoked based on user intent and fed into the `llm_with_tools` model, which binds tools to the core language model.

## Usage

```user_input=
events=graph.stream(
     {"messages": [("user", user_input)]},stream_mode="values"
)

for event in events:
  event["messages"][-1].pretty_print()
```




This example demonstrates the chatbot’s ability to retrieve information on "GM Syed" from Wikipedia, which is processed and presented in a conversational format.

## Graph Visualization

The graph structure of the chatbot pipeline can be visualized as follows:

```
from IPython.display import Image, display

try:
  display(Image(graph.get_graph().draw_mermaid_png()))
except Exception:
  pass
```




## Example Output

When a user asks, "Who is GM Syed?", the chatbot:

1. Calls the Wikipedia tool.
2. Displays a summary of G. M. Syed’s biography retrieved from Wikipedia.
