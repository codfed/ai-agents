# ai-agents

This repository is a chronolgy of my journey into building AI Agents

## trending-wikipedia-ollama

Use Phi-3 Ollama to generate context surrounding why the top 10 articles on Wikipedia were trending

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

- In the prompt, I pass the date as the full date with UTC info. Sometimes the response converts this to a standard human date, others it shows the full time code with it. Button this up.
- Figure out periodic discrepency in Wikipedia Response
- Handle the response to 2024 deaths article
- Experiment which LLM or tooling will be best for getting info about currently trending topics

## trending-wikipedia-chatgpt-context-window

Use `gpt-4-turbo` to figure out why top 10 articles are trending on Wikipedia by passing the entire article through the context window.

The cool:

- Much better results than Phi-3
- Used tiktoken to get a feel for how many tokens each article takes

The uncool:

- While it accurately identified Greg Gumbel's reason for trending to be his death, the next most popular article was his brother, Bryant Gumbel's. And it couldn't give any specific answers about it.
- Ran into Tokens Per Minute limits with my free account
- This cost $7 to run this for two days, and neither of those made it to 10 articles before the limit was hit. So $7 for 15 articles. Or around $0.50 per article

What to iterate on:

- Determin the most useful part of the article to pass.... I imagine in general the updated information is either in the description or the info box. Both of which are at the very top of the raw text file.
- Sort out the TPM errors
