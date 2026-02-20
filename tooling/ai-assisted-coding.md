# Guide To AI-Assisted Coding

**AI**: Artificial Intelligence

**LLM**: Large-Language Model

**CLI**: Command Line Interface

**IDE**: Integrated Development Environment

**ARC**: Advanced Research Computing

This guide is a collection of advice and tips based on the experience of ARC staff.
ARC's position is that we encourage curiosity, exploration and experimentation, including with AI-assisted coding tools.
We hope this guide can act as a gateway for anyone interested in this area.

***Disclaimer***:

* With the fast-moving world that we live in, it is also likely this guide will become outdated very quickly.
   Take note of the last modified timestamp.
* We are not responsible for any mishaps or destructive actions caused by the tools discussed in this guide.
  Always remember: “Artificial Intelligence is no excuse for Human Stupidity”*

These are some general guidelines and pointers around AI-assisted coding tools, based on the individual experiences of ARC staff.
It is intended to be a collaborative document and we invite any ARC staff interested in this topic to contribute. Feel free to open a pull request to improve the content.
ARC staff should use the [#community-ai-assisted-coding](https://ucl-arc.slack.com/archives/C090RT38Q83) channel to discuss anything they are unsure about.

## Getting started

Read the [ISD AI Practices in Software Development](https://liveuclac.sharepoint.com/:u:/r/sites/TL/SitePages/ISD-AI-Practices-in-Software-Development.aspx?csf=1&web=1&e=AGwGcZ) for a comprehensive overview of AI/LLMs and how to use them responsibly. The European Commission’s [Living guidelines on the responsible use of generative AI in research](https://research-and-innovation.ec.europa.eu/document/2b6cf7e5-36ac-41cb-aab5-0d32050143dc_en) is also worth a read.

## Some general do’s and don’ts

- Use AI tools to *support* your coding, not as a replacement. Assume that anything it writes is wrong, and critically review it with this mindset
- Use AI for repetitive, low-stakes tasks, or to generate some boilerplate so you don’t have to start from a blank screen - treat it as a glorified autocomplete
- Use AI for pull-request reviews, e.g. [GitHub’s copilot](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/request-a-code-review/use-code-review) - useful for catching typos and inconsistencies that are easier to miss by the human eye. But DON’T rely on AI review only to approve pull requests, always have a human reviewer as well
- DON’T commit any AI-generated code that you don’t understand or couldn’t have written yourself
- DON’T [use AI agents to produce 22k-line pull requests and dump them on unsuspecting open-source maintainers](https://github.com/tshort/StaticCompiler.jl/pull/180)
- DON'T use AI agents to produce large pull requests and dump them on your collaborators either
- [DON’T feel like you *need* to use AI](https://colton.dev/blog/curing-your-ai-10x-engineer-imposter-syndrome/)

## Tools

There are a lot of tools out there. At the time of writing (December 2025), AI agents are all the rage and this is what most of the tools listed below rely on. AI agents go beyond the simple chatbot interfaces such as ChatGPT, and provide more automation by integrating with your other tools, like your IDE, to carry out tasks for you (like editing code). You prompt them in a way similar to chatbots, but you can also provide them with more specific guidelines for your particular project (sort of like a contributing guide, but for agents instead of humans). [Agents.md](https://agents.md/) is an attempt at standardising this across agent providers, though not every provider supports it yet ([Claude is a notable example](https://github.com/anthropics/claude-code/issues/6235)).

### Model providers and platforms

The actual Large Language Models that power AI tools. Too many to list and keep track of, but some popular choices are:
- [Claude (Anthropic)](https://platform.claude.com/docs/en/resources/overview): popular for coding
- [GPT (OpenAI)](https://platform.openai.com/docs/models): popular for more general tasks, like writing
- [Ollama](https://docs.ollama.com/): allows you to run [open-weight](https://opensource.org/ai/open-weights) models locally
- [LM Studio](https://lmstudio.ai/): similar to Ollama allowing you to discover and run open-weight models locally
- [Gemini (Google)](https://ai.google.dev/gemini-api/docs/models)
- [GitHub Copilot](https://github.com/features/copilot): integrated with GitHub
- [Microsoft Copilot](https://copilot.microsoft.com/): not to be confused with the previous, integrated with Microsoft services. Probably not very relevant for coding


Choosing a model for your task often comes down to personal preference and experimentation

### IDEs with AI Agent support

- [Cursor](https://cursor.com/): “The best way to code with AI” (according to their website)
- [Windsurf](https://windsurf.com/): “The best AI for coding” (also, according to their website)
- [Zed](https://zed.dev/): “Love your editor again” (not as AI-centric as the two above, but with excellent support)
- [Antigravity](https://antigravityai.org/): Google's VScode based agentic IDE

### CLIs

These let you run and interact with AI agents straight from your terminal and let them carry out tasks you would do from a terminal. And yes, you can absolutely nuke your filesystem with them if you’re not careful.
- [Claude Code](https://claude.com/product/claude-code)
- [OpenAI Codex](https://openai.com/codex/)
- [GitHub Copilot](https://github.com/features/copilot/cli)
