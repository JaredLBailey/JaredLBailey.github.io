---
layout: post
title: Novel Data Interaction using a SQL Chatbot
image: "/posts/music-example.gif"
tags: [AI, SQL, Agents]
---

# Overview
My client had difficulty unlocking insights from complex databases. This was due to many end users not being fluent in SQL, which is the case for management in many industries. In order to get insights, management needed to ask specialized teams to fetch desired information, often with large lag times between initial requests and responses. To combat this difficulty I designed a user friendly query interface to allow non-coders to interact with databases directly. Leveraging the power of OpenAI, LangChain, and additional tools such as Google Search, my chatbot transforms natural language queries into precise SQL commands, providing clear responses along with the underlying reasoning and code.

Note: A sample music database is used to publically showcase this tool in order to not expose client data.

___

[See the code here](https://github.com/JaredBaileyDuke/sql-agent)

___

# The Challenge: Accessing Complex Data for the Non-Coding User
My client needed faster access to insights buried in large, multi-table databases. Since most decision makers weren’t fluent in SQL, even simple questions required routing requests to specialized teams. This created long turnaround times, context loss, and repeated back and forth to clarify what was needed.

___

# How It Works

![Music Example](https://raw.githubusercontent.com/JaredLBailey/JaredLBailey.github.io/master/img/posts/music-example.gif)

At its core, the SQL Chatbot Agent is comprised of multiple critical subtasks:

1. Natural Language Understanding: The chatbot parses user questions expressed in everyday language.
2. Agent: Decides whether the question can be answered from the database, or if a call to Google Search would provide an answer.
3. RAG: The agent references the known database structure (including table joins) in order to better process the next steps.
4. SQL Generation: The agent translates these queries into SQL commands that are executed against the database.
5. Transparent Results: Not only does the system return the final answer, but it also provides insight into the reasoning and the code that generated the result. This empowers users with full visibility into the query process.

For example, users can ask:
- “How many customers purchased AC/DC albums?”
- “Which employee (first and last name) sold the most albums, and how many were sold?”
These queries, although framed in a musical context for public demos, demonstrate the agent’s potential when applied to other data.

___

# Tech Stack and Tools
The project harnesses a blend of modern technologies:
- OpenAI: Powers the natural language understanding, enabling the chatbot to interpret and convert user questions.
- LangChain: Facilitates the chaining of language model outputs with SQL query generation, ensuring a seamless translation from natural language to SQL.
- Google Search (via SerpAPI): Augments the chatbot’s capabilities by providing external context when needed.
- SQLite Sample Database: For the public-facing demonstration, a sample database from SQLite Tutorial is used, ensuring an interactive and familiar experience.
