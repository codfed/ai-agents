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
- This cost $3 to run this for two days, and neither of those made it to 10 articles before the limit was hit. So $3 for 15 articles. Or around $0.20 per article

What to iterate on:

- Determine the most useful part of the article to pass.... I imagine in general the updated information is either in the description or the info box. Both of which are at the very top of the raw text file.
  ^^^^ Did that, only passed the first 5000 characters through the context window.. Same quality of results but for $0.01 per article
- Sort out the TPM errors
- Play with different models

## trending-wikipedia-chatgpt-phoenix-tracing

Want to level up my prompt evaluation game. Pretty simple to get started, immediately paid of in being able to easily see the entire prompt that was sent. It's all available to me through print statements and log files... but it is so nice to be able to easily click through each prompt to see the entire call and response.

## trending-wikipedia-langchain-memory

The most egregious shortcoming in the projects so far has been next-of-kin in celebrity deaths.

- Greg Gumbel died, his brother Bryant Gumbel trended but said nothing of his brother's passing
- Jeff Baena died, his widow, Aubrey Plaza began to trend. It identified Jeff's death but did not mention anything of her late husband's passing

Decided to try out LangChain's memory feature for this

- Run trending analysis as a chain with memory
- Pass that memory to a new conversation chain
- Look for relation to other articles in the memory

The cool:

- It worked!

The uncool:

- I can't get the damn thing to shut up.... I really only want one concise sentence to show
- If it doesn't know, I want it to tell me or not reply at all

What to iterate on:

- Response-tuning
- Keep responses short
- Give tight answer if there is no identified similar articles

## Newly Trending Wikipedia Langchain Memory

Each trending Wikipedia article is accompanied by its view data for the previous 4 days. Trending articles are sticky, so as I've been working on this I'm getting tired of seeing (and paying for) the analysis of the same articles.

I started this with the intention of using an LLM call determine if the articles were only trending on the most recent days. The results were not consistent or predictable. This is where coming at this as an engineer is a huge advantage... in less than the time it would have taken me to test two more prompts I had a reliable Python function that did exactly what I wanted.

With this cleaner data output I'm feeling like I have the output getting closer to the realm of useful, interesting, and easily palatable!

I've also updated this to keep a master log of all days it's been run for.

What to iterate on:

- Clean up the prompt output on the relation to other articles
- Get this to run on it's own once a day, host the results as a static site

## Newly Trending Wikipedia with news context

One day, none of the new articles had any rational reason to be trending. So I incoporated a call to Google News through Serper.dev.

I figured I'd have to do some looping through the results and make some more structure but on my first iteration I just passed the entire json response to ChatGPT and it worked perfectly!

Takeaways:

- Very pleasantly surprised with how well ChatGPT handled a prompt with raw json from the news api
- Impressed with ChatGPT's ability to reply with an html structure
- LangChain Memory stopped giving meaningful context....

What to iterate on

- Remove LangChain memory
