# Week 1 - LLM Engineering Foundations
## Interview Prep 1-Pager

---

## 🎯 Core Competencies Demonstrated

### Working with Frontier LLMs
- **Multi-provider experience**: OpenAI (GPT-4/GPT-5), Google Gemini, Meta Llama via Ollama
- **Understanding cost vs capability tradeoffs**: Cloud APIs vs local inference
- **API integration**: Built production-ready applications using REST endpoints and Python client libraries

### LLM Fundamentals
- **Tokenization**: Understand how LLMs process text (~750 words per 1000 tokens), why this impacts math/counting
- **Context windows**: Managing total tokens for input/output, cost implications
- **Stateless architecture**: LLMs have no memory - learned to maintain conversation context by passing full history
- **Prompting strategies**: Zero-shot, one-shot, multi-shot prompting with system/user role patterns

### Model Architecture Knowledge
- **Three model types**: Base (next-token predictors), Chat/Instruct (RLHF trained), Reasoning (chain-of-thought)
- **Open vs Closed models**: Evaluated tradeoffs between frontier models (GPT, Claude, Gemini) and open-source (Llama, Mixtral, Qwen)
- **Deployment options**: Cloud APIs for power, local inference (Ollama) for privacy/cost control

---

## 💼 Key Project: AI-Powered Website Analyzer & Content Generator

### Problem Statement
Built as a proof of concept - originally wanted to create sarcastic, honest website reviews for a friend. Evolved into a practical business tool for generating company brochures from website content.

### Technical Implementation
**Phase 1 - Website Summarization**
- Web scraping to extract page content
- Engineered system prompts to control tone and output format
- Streaming responses for better UX (typewriter effect)
- Markdown-formatted outputs without code blocks

**Phase 2 - Multi-Agent Workflow** (Agentic AI Design Pattern)
- **Agent 1**: Analyze all links on a webpage, intelligently select relevant ones (About, Careers, Company pages)
- **Agent 2**: Fetch and synthesize content from multiple pages into cohesive brochure
- Used structured JSON responses for agent communication
- Truncation strategy to manage context window limits (5K character cap)

### Technical Decisions
- **OpenAI Compatible Endpoints**: Single codebase works with multiple providers by changing base_url
- **Response formatting**: Used `response_format={"type": "json_object"}` for structured outputs
- **Streaming**: Implemented `stream=True` for real-time content generation
- **Local development**: Set up Ollama for free, private experimentation

### Business Applications Identified
- Marketing content generation from company websites
- Competitive analysis automation
- Personalized sales collateral
- Recruitment brochures for candidates
- Any document synthesis from multiple sources

---

## 🔧 Technical Stack & Tools

**Core Technologies**
- Python (requests, dotenv, IPython for notebooks)
- OpenAI API, Google Gemini API, Ollama
- Jupyter Lab for rapid prototyping
- tiktoken for tokenization analysis

**Development Practices**
- Environment management (conda/venv)
- API key security with .env files
- Streaming responses for better UX
- Error handling and troubleshooting

---

## 🚀 Key Learnings & Insights

### What LLMs Excel At
- **Synthesizing information** from multiple sources
- **Fleshing out skeletons** - taking structure and adding detail
- **Nuanced understanding** - tasks that would be hard to code with traditional parsing (e.g., "which links are relevant?")
- **Coding assistance** and explanation

### What to Watch Out For
- **Hallucinations** - confidently making mistakes
- **Tokenization limits** - impacts mathematical reasoning
- **Cost management** - every token in conversation history costs money
- **Rate limits** - need to handle API throttling

### Architectural Insights
- "Memory is an illusion" - every LLM call is stateless, we create the illusion by passing full context
- Cost and rate limiting becoming key differentiators as model capabilities converge
- Prompts are like having "a smart junior analyst" - need to guide and challenge outputs

---

## 💡 Interview Talking Points

**"Tell me about a project you built with AI"**
> "I built an AI-powered website analyzer that generates company brochures. Started as a fun proof of concept for sarcastic website reviews, but I recognized the business value and evolved it into a multi-agent system. The first agent intelligently selects relevant links from a homepage, the second synthesizes content from multiple pages into a cohesive brochure. I used OpenAI's API but architected it to work with multiple providers through compatible endpoints. The interesting challenge was managing context windows and engineering prompts to get consistent structured outputs."

**"How do you choose between different LLM providers?"**
> "I evaluate based on the use case. For production applications needing reliability and power, I use frontier models like GPT or Gemini. For experimentation, privacy-sensitive data, or cost control, I run open-source models locally via Ollama. I've built applications that work with multiple providers using OpenAI-compatible endpoints, so I can switch providers by changing a base URL and API key."

**"What do you understand about how LLMs work?"**
> "At the core, LLMs are next-token predictors trained on massive datasets. They use transformer architecture with billions of parameters. The 'memory' in chat applications is actually an illusion - every call is stateless, we pass the full conversation history each time. Understanding tokenization is crucial - about 750 words per 1000 tokens - which impacts both cost and capabilities. I also know there are three main types: base models, instruction-tuned models, and reasoning models, each optimized for different use cases."

**"How do you approach prompt engineering?"**
> "I separate system prompts (setting role, tone, output format) from user prompts (the actual task). I use one-shot prompting by providing examples when I need specific output formats. For structured data, I request JSON responses. I've learned to be specific about what to exclude, handle edge cases in prompts, and iterate based on outputs. For complex tasks, I chain multiple LLM calls together - an agentic design pattern."

**"What considerations do you have for production LLM applications?"**
> "Key things: API key security through environment variables, cost management by tracking token usage, error handling for rate limits and API failures, streaming for better UX, managing context window limits through truncation or summarization, and validation of structured outputs since LLMs can occasionally produce malformed JSON."

---

## 🎓 Next Steps
This was Week 1 of an 8-week LLM Engineering course. Looking forward to:
- Fine-tuning custom models
- Advanced RAG (Retrieval Augmented Generation)
- Building autonomous multi-agent systems
- Production deployment strategies

---

*Built with: OpenAI GPT-4.1-mini/GPT-5-nano, Python, Jupyter Lab, Ollama (Llama 3.2)*
