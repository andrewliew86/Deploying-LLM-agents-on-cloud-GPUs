# Creating an open source LLM agent and deploying the model on AWS SageMaker or RunPod

Agents are large language models that are equipped with tools (e.g. search engines, Python REPL etc…) so it is no longer limited by it’s training data. The agent takes a task as input, breaks it into a set of smaller tasks and then uses these tools to complete these tasks.

Given a task, our LLM agent will:
- create a plan of action to complete the task 
- automatically search for webpages (DuckDuckGo search)
- automatically search for YouTube videos (YouTube search) 

We will be creating a basic agent in LangChain using an open-source model called Mixtral 8x7B released by Mistral AI. Unlike other models such as Llama2, Mixtral 8x7B has a Mixture-of-Experts (MoE) architecture which replaces the traditional feed-forward network layers with 8 experts and a router that decides which tokens are sent to experts for processing. The main advantage of MoE models is that not all experts are activated during inferencing meaning very efficient processing (faster and less computer resources needed than a large model like 70B). We will be using Amazon SageMaker or RunPod to deploy a quantized Mixtral 8x7B due to the relatively large GPU compute requirements (~32 GB) of the model.

## Results:
The agent performed well returning relevant results when given an appropriate query. For example, when asked "Give me a link to 2 cat videos", it responded, "To answer this question, I need to find 2 cat videos on YouTube. I will use the YouTube search tool to find these videos… I now know the final answer. Final Answer: URL..."

The inferencing time was also acceptable with an average of ~5 seconds per run and 93.41 tokens per second token for reading the prompt tokens (prompt eval) and 42.41 tokens per second for generating response (eval time) using the RunPod instance.

## Notes: 
- **Python libraries/tools**: LangChain, and 🤗
- **Cloud computing resources**: Amazon SageMaker g5.12xlarge instance or RunPod 1x RTX 5000 Ada 32 GB VRAM pod instance

