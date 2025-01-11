# ai-agents

This repository is a chronolgy of my journey into building AI Agents

## What's trending on wikipedia

It's easy to figure out what's trending on Wikipedia using the API. I wanted to know WHY. So I played around with various methods to figuring this out.

The basic steps are:

1. Get trending Wikipedia Data
2. Use LLM prompting to determine why they are trending
3. Export findings to easily digestible HTML list

Iterations:

1. Proof of Concept using locally run Phi-3/Ollama
2. Passing context from each article's text to ChatGPT in the prompt
3. Implement Arize's Phoenix product to assist in tuning my prompts
4. Use LangChain Memory to determine if there's any relation between trending articles
5. Limit the list to only the newly trending articles, refine prompting

This is very accurate in determining why the article is trending due to an anniversary, movie release, or the death of a public figure and their next of kin. It has no knowledge of trending news and misses reasons for trending articles that have not been updated yet.

Future iterations:

- Get this to run automatically in AWS and save to a static hosted HTML page
- Add context from trending news
