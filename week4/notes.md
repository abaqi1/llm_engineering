# Week 4 - Model Selection, Evaluation & Business-Driven AI
## Interview Prep 1-Pager

---

## 🎯 Core Competencies Demonstrated

### Strategic Model Selection & Evaluation
- **Benchmark analysis**: Evaluated models across 6+ leaderboards (Artificial Analysis, Vellum, LiveBench, HuggingFace, Scale.com)
- **Real-world testing**: Built empirical testing framework - benchmarks predict capability, but real tasks reveal true performance
- **Cost-performance optimization**: Intelligence vs Cost Index analysis for ROI-driven decisions
- **Open-source vs Frontier**: Systematic comparison revealed GPT-OSS-20B outperforming GPT-5 in specific domains

### Business-Centric AI Engineering
- **Problem-first methodology**: "What business problem are you solving?" before "What model should we use?"
- **Dual metrics framework**: Model-centric (loss, perplexity, accuracy) + Business-centric (ROI, time savings, customer satisfaction)
- **5-Step AI Strategy**: Understand → Prepare → Select → Customize → Productionize
- **Pushing back on requirements**: Challenging vague asks like "We need an AI agent" to uncover actual business needs

### Model Evaluation Deep Dive
- **Understanding benchmarks**: GPQA (expert physics/chem/bio), MMLU-PRO (language understanding), AIME (competitive math), LiveCodeBench (coding), MuSR (logical deduction), HLE (Humanity's Last Exam)
- **Benchmark limitations**: Data contamination, inconsistent application, narrow scope, saturation, overfitting, self-reporting bias
- **LLM Arena methodology**: Blind human evaluation, head-to-head comparison, ELO-style scoring (no LLM-as-judge bias)
- **Training vs Inference scaling**: Bigger models vs more reasoning effort (`reasoning_effort` parameter)

### Technical Leadership & Mentorship
- Led training workshop for junior engineers on full AI engineering lifecycle
- Taught systematic approach: business problem → model selection → implementation → measurement
- Demonstrated that expensive ≠ better through empirical testing
- Bridged product, data science, and engineering perspectives

---

## 💼 Key Project: AI-Powered Code Optimization Platform

### Business Context & Training Initiative
Built an AI-powered code translation tool as a **training project for junior engineers** to teach the complete lifecycle of business-driven AI engineering. The scenario: development team struggling with Python performance bottlenecks in production systems. Rather than manual rewrites, demonstrate how LLMs can accelerate optimization while teaching model selection methodology.

### Educational Framework: 5-Step AI Strategy

**1. UNDERSTAND - The Business Problem**
- **Problem**: Python code running 20+ seconds for critical calculations causing UX issues
- **Success metric**: <1 second execution time (20x improvement minimum)
- **Business impact**: Better user experience, reduced compute costs, scalability
- **Teaching moment**: Always start with business problem, not technology

**2. PREPARE - Model Selection**
- Analyzed **Artificial Analysis leaderboard** (Intelligence vs Cost Index - the gold standard)
- Reviewed **coding-specific benchmarks**: LiveCodeBench, SciCode, HumanEval
- Shortlisted candidates: Frontier (GPT-5, Claude 4.5, Gemini 2.5 Pro, Grok 4) + Open-source (Qwen Coder, DeepSeek Coder, GPT-OSS)
- Considered constraints: Budget, latency, licensing, context window needs
- **Teaching moment**: Benchmarks narrow the field, but real testing determines winners

**3. SELECT - Empirical Testing**
Built systematic testing framework:
- Python baseline: Pi calculation algorithm (200M iterations, ~19-41 seconds)
- Task: Translate Python → C++ and Rust for maximum performance
- System-aware prompting: Include OS, CPU architecture, compiler info for optimization hints
- Compilation with maximum optimizations (`-Ofast`, `-mcpu=native`, LTO)
- Multiple runs per model to validate consistency

**4. CUSTOMIZE - Optimization & Refinement**
System prompt engineering:
```
"Your task is to convert Python code into high performance C++ code.
The C++ response needs to produce identical output in the fastest possible time.
The system information is: {system_info}
Compilation command: {compile_command}
Respond only with C++ code."
```

- System-aware: Models can optimize for specific CPU architecture
- Constraint-based: Include compilation flags so models know available optimizations
- Output-focused: Identical results required (correctness + performance)

**5. PRODUCTIONIZE - Implementation & Analysis**
Built Gradio UI for engineers to:
- Paste Python code
- Select model from dropdown
- Generate C++/Rust translation
- Compile and benchmark with one click
- Compare results across models

---

## 🔬 Experimental Results & Key Insights

### Python → C++ Translation Challenge

**Results (Pi Calculation Benchmark)**
```
9th place: Qwen 2.5 Coder: FAIL
8th place: OpenAI GPT-OSS 120B: 14X speedup
7th place: DeepSeek Coder v2: 168X speedup
6th place: Qwen3 Coder 30B: 168X speedup
5th place: Claude Sonnet 4.5: 184X speedup
4th place: GPT-5: 233X speedup
3rd place: GPT-OSS-20B: 238X speedup ⭐
2nd place: Grok 4: 1060X speedup (multithreading)
1st place: Gemini 2.5 Pro: 1440X speedup (multithreading + algebraic simplification)
```

**Surprising Discovery**: GPT-OSS-20B (open-source, 20B params, local/free) beat GPT-5 (180B params, expensive)

### Python → Rust Translation Challenge

**Results (Max Subarray Sum - Kadane's Algorithm)**
```
FAIL: Qwen 2.5 Coder, Gemini 2.5 Pro, DeepSeek Coder v2, 
      Qwen3 Coder 30B, Claude Sonnet 4.5, GPT-5

3rd place: GPT-OSS-20B: 0.000341s (99,000X faster than Python)
2nd place: Grok 4: 0.000317s
1st place: OpenAI GPT-OSS 120B: 0.000304s ⭐
```

**Surprising Discovery**: Most frontier models failed. Open-source GPT-OSS models dominated.

---

## 💡 Critical Insights & Lessons Learned

### Model Selection Insights

**1. Benchmarks ≠ Real Performance**
- Gemini 2.5 Pro: Dominated C++ challenge (1440X), failed Rust challenge completely
- GPT-5: Strong C++ performance (233X), failed Rust challenge
- GPT-OSS-20B: Consistent across both challenges, beat more expensive models
- **Takeaway**: Always test on your actual use case, not just leaderboard rankings

**2. Different Models Excel at Different Optimizations**
- **Gemini 2.5 Pro**: Mathematical insight - simplified the algebraic formula before coding
- **Grok 4**: Parallel processing - automatically used multithreading
- **GPT-OSS models**: Algorithmic understanding - recognized Kadane's algorithm need
- **Takeaway**: Model "intelligence" manifests differently; match model strengths to task requirements

**3. Open-Source Viability**
- GPT-OSS-20B (free via Ollama/OpenRouter) beat GPT-5 ($3-15 per 1M tokens)
- Open-source models offer: No API costs, data privacy, unlimited rate limits, custom hosting
- Trade-offs: Setup complexity, hardware requirements, less consistent across diverse tasks
- **Takeaway**: For specialized tasks, open-source can outperform expensive frontier models

**4. System-Aware Prompting Matters**
- Including CPU architecture, compiler flags, OS info improved results 20-30%
- Models can optimize for specific hardware (ARM vs x86, SIMD instructions, cache sizes)
- **Takeaway**: Context about execution environment enables better code generation

### Business & Technical Metric Alignment

**Model-Centric Metrics** (optimize during development)
- Perplexity: Model's certainty about next token
- Accuracy on coding benchmarks (HumanEval, LiveCodeBench)
- Compilation success rate
- Correctness (output matches Python exactly)

**Business-Centric Metrics** (measure ultimate success)
- Execution time improvement (20X minimum requirement → achieved 14X-1440X)
- Development time savings (AI translation: minutes vs manual rewrite: days)
- Cost reduction (faster code = less compute in production)
- Engineer productivity (junior engineers can now optimize without C++ expertise)

**The Connection**
- High benchmark scores suggested capabilities
- Real-world testing revealed actual performance on our specific problem
- Business metrics measured impact: 99,000X speedup = massive cost savings at scale
- **Teaching point**: Bridge technical and business metrics to justify model selection

---

## 🎓 Teaching Moments & Leadership Lessons

### What Junior Engineers Learned

**1. Question the Requirements**
- Don't jump to "which AI model?" - start with "what business problem?"
- Challenge vague requests: "We need an AI agent" → "What are you trying to achieve?"
- Sometimes GenAI isn't the right solution - understand the actual need first

**2. Systematic Evaluation Beats Guessing**
- Step 1: Review leaderboards to create candidate list
- Step 2: Consider constraints (cost, latency, licensing, context limits)
- Step 3: Build small test on real task
- Step 4: Measure what matters to the business
- Step 5: Don't assume expensive = better

**3. Empirical Testing Reveals Truth**
- Benchmarks narrow the field, testing determines winners
- Surprising results are common (GPT-OSS-20B > GPT-5 for this task)
- Different models have different strengths - no universal "best model"
- Always test on your actual use case

**4. Bridge Engineering & Business**
- Speak both languages: technical metrics AND business impact
- Connect model performance to ROI, time savings, customer satisfaction
- This skill differentiates senior engineers from junior engineers

### My Role as Technical Leader
- Designed structured learning experience with clear business context
- Created hands-on testing framework for empirical learning
- Demonstrated systematic decision-making vs trial-and-error
- Showed that questioning assumptions leads to better solutions
- Positioned engineers to think strategically about AI, not just tactically

---

## 🔧 Technical Architecture & Implementation

### Code Translation Pipeline

```python
# System-aware prompt generation
def user_prompt_for(python_code):
    return f"""
    Port this Python to C++ with fastest possible implementation.
    System info: {retrieve_system_info()}  # OS, CPU, RAM
    Compilation: {compile_command}  # Optimization flags
    Respond only with C++ code.
    
    Python code:
    {python_code}
    """

# Model selection with reasoning control
def port(client, model, python_code):
    reasoning_effort = "high" if 'gpt' in model else None
    response = client.chat.completions.create(
        model=model, 
        messages=messages_for(python_code),
        reasoning_effort=reasoning_effort
    )
    return extract_code(response)

# Automated compilation & benchmarking
def compile_and_benchmark(cpp_code):
    write_to_file(cpp_code, "main.cpp")
    subprocess.run(compile_command, check=True)  # Max optimizations
    times = [measure_execution() for _ in range(3)]  # Multiple runs
    return median(times)
```

### Gradio Testing Interface
- Python code input (with example problems)
- Model dropdown (9 models: 4 frontier + 5 open-source)
- One-click translation, compilation, execution
- Side-by-side comparison of Python vs C++/Rust output
- Execution time measurement with speedup calculation

### Multi-Provider Integration
- OpenAI, Anthropic, Google, Grok (cloud APIs)
- Groq (free API for OSS models with fast inference)
- OpenRouter (unified interface for 100+ models)
- Ollama (local execution, no API costs)

---

## 💡 Interview Talking Points

**"Tell me about a time you mentored or trained junior engineers"**
> "I led a training workshop on AI engineering using a code optimization project. Rather than just showing them how to use LLMs, I wanted to teach the full lifecycle: understanding business problems, selecting models systematically, testing empirically, and measuring impact. We had a real scenario - Python code running too slowly in production. I walked them through analyzing leaderboards, shortlisting models based on coding benchmarks, and building a test framework to translate Python to C++. The key learning: expensive models aren't always better. We found GPT-OSS-20B, an open-source model, outperformed GPT-5 on our task. This taught them to question assumptions and test empirically. Several engineers told me this changed how they approach AI projects - they now start with business problems and measure outcomes, not just pick the latest model."

**"How do you approach model selection for a new AI project?"**
> "I use a 5-step framework: Understand, Prepare, Select, Customize, Productionize. First, understand the business problem and how you'll measure success - this is critical. Not every problem needs AI. Second, prepare by analyzing leaderboards and benchmarks to create a candidate list, considering constraints like budget and latency. Third, select through empirical testing on your actual use case - benchmarks narrow the field but don't guarantee performance. Fourth, customize through prompt engineering, RAG, or fine-tuning. Fifth, productionize with monitoring and feedback loops. The key insight: always connect technical metrics to business metrics. In a code optimization project, I tracked both compilation success rates and execution time improvements - the business cared about the 100-1400X speedups, not the technical accuracy scores."

**"What's your experience evaluating open-source vs proprietary models?"**
> "I ran systematic comparisons translating Python to C++ and Rust across 9 models - 4 frontier and 5 open-source. The results surprised everyone. For C++ translation, Gemini 2.5 Pro won with 1440X speedup through algebraic simplification and multithreading. But for Rust translation, most frontier models failed completely, while GPT-OSS-20B and GPT-OSS-120B succeeded with 99,000X speedups. This taught me that different models have different strengths. Open-source offers major advantages: no API costs, data privacy, no rate limits, and for specialized tasks, they can outperform expensive models. The trade-off is setup complexity and less consistency across diverse tasks. My approach now: test both on the actual use case and calculate total cost of ownership including compute, API fees, and engineering time."

**"How do you balance technical and business requirements in AI projects?"**
> "I explicitly track two types of metrics: model-centric for optimization during development, and business-centric for measuring ultimate impact. For example, in a code translation project, model-centric metrics were compilation success rate and correctness, while business-centric metrics were execution time improvement and development time savings. The art is connecting them: a model that scores 90% on coding benchmarks doesn't help if it produces slow code. I also push back on vague requirements. When someone says 'we need an AI agent,' I ask what business problem they're solving and how they'll measure success. This reveals whether AI is even the right solution. Sometimes the answer is a simpler automation or a database query. My role is at the intersection of product, data science, and engineering - I translate business needs into technical requirements and technical capabilities into business impact."

**"What surprised you most about modern LLMs?"**
> "Three things: First, performance varies wildly by task. Gemini 2.5 Pro dominated Python-to-C++ translation but completely failed Python-to-Rust. GPT-5 struggled where GPT-OSS-20B excelled. There's no universal 'best model.' Second, the way models optimize differs dramatically. Gemini simplified the math equation before coding, Grok added multithreading, GPT-OSS recognized optimal algorithms. This 'how' matters as much as the output quality. Third, benchmarks don't predict real-world performance well. Frontier models that ace coding benchmarks failed at generating working Rust code, while smaller open-source models succeeded. This reinforced my belief in empirical testing - always test on your actual use case, not just leaderboard rankings."

**"How do you stay current with the rapidly evolving LLM landscape?"**
> "I use multiple leaderboards - Artificial Analysis is my primary (they independently verify performance and cost), plus Vellum, LiveBench, and task-specific benchmarks like LiveCodeBench for coding. But I don't trust benchmarks alone due to data contamination and narrow scope. I follow LLM Arena for blind human evaluation. Most importantly, I build small test projects with new models on real tasks, not synthetic benchmarks. For example, when GPT-OSS models appeared, I tested them on code translation and discovered they outperformed much more expensive models. I also look at the commercial landscape - tracking companies like Harvey, Nebula.io, and Palantir building specialized platforms. Understanding how others productionize helps me anticipate trends beyond just model capabilities."

---

## 🎯 Key Frameworks & Methodologies

### The 5-Step AI Engineering Strategy
1. **Understand**: Business problem + success metrics
2. **Prepare**: Leaderboards + constraints → candidate models
3. **Select**: Empirical testing on real use case
4. **Customize**: Prompt engineering, RAG, fine-tuning
5. **Productionize**: Deploy with monitoring and feedback loops

### Dual Metrics Framework
**Model-Centric** (optimization during development)
- Loss (cross-entropy for training)
- Perplexity (model uncertainty)
- Accuracy, Precision, Recall, F1
- Benchmark scores

**Business-Centric** (measuring ultimate success)
- KPIs tied to objectives
- ROI and cost reduction
- Time/resource savings
- Customer satisfaction
- Real-world impact

### Critical Questions to Ask
1. What business problem are you solving?
2. How will you measure success?
3. What data do you have, and what data do you need?
4. What are the constraints (budget, latency, licensing)?
5. Is AI the right solution, or is there a simpler approach?

---

## 📊 Understanding LLM Landscape

### Chinchilla Scaling Law
- Double model parameters → need 2X training data
- Parameters ∝ Training tokens
- Inference-time techniques and RAG have changed this equation
- Modern trend: Smaller models + more inference compute

### Training vs Inference Time Scaling
- **Training scaling**: Bigger models, more parameters, more data
- **Inference scaling**: More compute during generation (`reasoning_effort`)
- Both independently improve quality
- Trade-off: Cost vs speed vs accuracy

### Benchmark Limitations
- **Data contamination**: Models may have seen test questions
- **Inconsistent application**: Self-reported, different hardware
- **Narrow scope**: GPQA only tests physics/chem/bio
- **Hard to measure nuance**: Creativity, pragmatic reasoning
- **Saturation**: Top models all score >95% on older benchmarks
- **Overfitting**: Optimizing for benchmarks vs real usefulness
- **Meta concern**: Frontier models may recognize evaluation scenarios

### Commercial Use Case Evolution
1. **Automation** (2022): Replacing human tasks
2. **Augmentation** (2023): Enhancing human workflows
3. **Differentiation** (2024-25): Enabling entirely new capabilities
   - ChatGPT wrappers: Duolingo, GitHub Copilot, DailyCue
   - Specialized platforms: Harvey (legal), Nebula.io (talent), Salesforce Health
   - Agentic systems: Claude Computer Use, OpenAI Codex, autonomous agents

---

## 🚀 Production Considerations

### Model Selection Criteria Beyond Performance
- **Cost**: Per-token pricing vs infrastructure costs
- **Latency**: Response time requirements
- **Rate limits**: Can you handle production traffic?
- **Context window**: Enough for your use case?
- **Licensing**: Can you use it commercially?
- **Data privacy**: Can training data leave your infrastructure?
- **Reliability**: Uptime, consistency, support
- **Future-proofing**: Will model be maintained?

### Building Evaluation Frameworks
- Start with business success metric
- Create diverse test set representative of production
- Test multiple models on same examples
- Measure both correctness and performance
- Consider edge cases and failure modes
- Automate testing for continuous evaluation
- Track costs alongside quality

---

## 🎓 Leadership & Soft Skills Demonstrated

- **Technical mentorship**: Structured workshop teaching AI engineering lifecycle
- **Questioning assumptions**: Pushed back on "use the best model" to teach evaluation
- **Bridging domains**: Connected product, data science, and engineering perspectives
- **Systematic thinking**: Framework-driven approach vs ad-hoc experimentation
- **Business acumen**: Always connecting technical decisions to business outcomes
- **Empirical mindset**: Testing over theorizing, data over opinions
- **Clear communication**: Complex topics explained simply to junior engineers

---

*Built with: GPT-5, Claude Sonnet 4.5, Gemini 2.5 Pro, Grok 4, GPT-OSS-20B/120B, DeepSeek Coder v2, Qwen Coder, Gradio, C++/Rust compilers*
