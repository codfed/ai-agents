# ai-agents

This repository is a chronolgy of my journey into building AI Agents

## trending-wikipedia-ollama

Use Ollama endpoint to get context surrounding why the top 10 articles on Wikipedia were trending

The cool:

- I now have a scaffold/example for connecting to a local instance of Phi-3 Mini or llama3.2b
- Minimal dependencies! A simple `pip install requests ollama` went a long way!
- It saves files as it is running to help in debugging and iterating
- The results surprise me! Using an SLM for context on why something was trending yesterday is not going to be too accurate. I was pleastly surprised how much it got right from just the article's extract and it's own training data.

The uncool:

- Periodically the Wikipedia response will not include a `mostread` element
- SLM response prone to hallucination since we're looking at articles trending YESTERDAY
- the 2024 deaths article causes Phi-3 Mini to respond with helpful advice on how to better prompt it(reference this in the 2024-12-25 files)

What to iterate on:

- Figure out periodic discrepency in Wikipedia Response
- Handle the response to 2024 deaths article
- Experiment which LLM or tooling will be best for getting info about currently trending topics
