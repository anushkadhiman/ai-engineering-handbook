# Agentic AI

Agentic AI refers to autonomous systems that **use reasoning, planning, and tools to achieve complex, multi-step goals with minimal human intervention.** Unlike reactive generative AI, agentic AI is proactive, capable of taking independent actions, learning from feedback, and collaborating with other agents or humans to optimize workflows.

Agentic AI systems often **use frameworks where an orchestrator agent manages, coordinates, and assigns tasks to specialized agents**, acting as a virtual team.

Here are some key characteristics and component,

- **Autonomy:** Operates independently, setting its own sub-goals to reach a larger objective.
- **Proactivity:** Anticipates needs and acts before being prompted, rather than just responding to queries.
- **Tool Usage:** Connects with APIs, databases, and software to execute tasks (e.g., booking flights, sending emails).
- **Architecture:** Composed of perception (environment awareness), cognition (reasoning and planning), and action layers.
- **Memory:** Maintains context over long, multi-step tasks.

**How Agentic AI is different from Generative AI?**
Generative AI focuses on creating content (text, images) based on a single prompt whereas Agentic AI focuses on completing tasks, managing workflows, and taking actions to achieve a goal.

Here are some common use cases,

- **Business Operations:** Managing supply chains, inventory, and logistics.
- **Software Development:** Debugging code, managing software lifecycles.
- **Customer Service:** Providing personalized, proactive support.
- **Personal Assistance:** Planning, booking, and managing complex schedules.

---

## Prompt chaining

Prompt chaining is an AI engineering technique that **breaks complex, multi-step tasks into a sequence of smaller, manageable prompts, where the output of one prompt becomes the input for the next.** This method enhances LLM performance, improves accuracy, enables better control over, and allows for handling tasks that exceed context limits.

**How it Works:** It operates **like an assembly line, passing intermediate results forward to build a final, higher-quality output**, often used for summarizing, drafting, and refining content.

**What are some benefits?**

- **Improved Accuracy:** Reduces hallucinations by guiding the model through logical, step-by-step reasoning.
- **Overcomes Context Limits:** Breaks large tasks into smaller chunks that fit within model token limits.
- **Better Debugging:** Makes it easier to identify exactly which step in a process failed, as each step is isolated.
- **Enhanced explainability and transparency:** breaking the process into steps lets users see how decisions are made, helping build trust in the AI.

**Use Cases:**

- **Content Creation:** Generate an outline, then write sections, then edit in a sequence.
- **Data Processing:** Extract data, clean it, analyze it, and then visualize it in separate steps.
- **Software Development:** Write pseudo-code, generate code, test, and debug in a chain.

**Implementation Example:**

**Step 1:** "Summarize this article."
**Step 2:** "Based on this summary, list the 3 main takeaways."
**Step 3:** "Draft a social media post based on these takeaways".

---

## Routing

Routing is a design pattern **acting as an intelligent traffic controller that classifies user queries and directs them to the most appropriate specialized agent, tool, or workflow**. It optimizes performance and costs by routing complex tasks to advanced models and simple tasks to cheaper ones.

**Definition & Purpose:** Routing acts as a decision layer that determines the best path for a request, enhancing system scalability, efficiency, and accuracy. It moves beyond rigid, linear execution to dynamic, context-aware handling.

**Here are some key approaches include to Routing:**

- **LLM-based:** Uses an LLM to analyze intent and context for dynamic routing.
- **Rule-based:** Uses predefined logic, such as if/else statements, for simple, predictable routing.
- **Semantic (Embedding-based):** Calculates the cosine similarity between the query embedding and pre-computed route descriptions to select the best handler.

**Routing Patterns:**

- **Single-agent routing:** Directs a request to one specialized agent.
- **Multi-agent routing:** Directs to one of many agents.
- **Hierarchical routing:** A top-level router delegates tasks to sub-agents.

**Benefits:**

- **Cost Efficiency:** Using smaller, faster models for simple tasks and larger models only when necessary.
- **Specialization:** Allows for the use of domain-specific agents.
- **Modularity:** Makes it easier to add or update specialized agents without rebuilding the entire system.

**Use Cases:**

- **Customer Support:** Routing queries to specialized support agents (billing, technical, sales).
- **Task Decomposition:** Breaking down complex user requests into smaller, manageable sub-tasks.
- **Intent Classification:** Identifying the user's intent to determine the proper response or action.

---

## Parallelization

Parallelization **improves speed and efficiency by running multiple, independent AI agents or tool calls simultaneously rather than sequentially**. A planner or coordinator agent breaks complex tasks into subtasks, which are executed in parallel to reduce latency, often using scatter-gather patterns.

**What parallelization actually does?**

- **Reduced Latency:** By executing non-dependent tasks at the same time, the total time taken is reduced to the duration of the longest single task.
- **Scatter-Gather Pattern:** A central agent (planner/manager) breaks down a large request, distributes sub-tasks to specialized agents, and merges their outputs into a final result.
- **Independent Task Execution:** This approach is best for tasks that do not rely on each other, such as searching multiple databases or fetching multiple web pages.
- **Tool/API Optimization:** Multiple read-only tools can be invoked in parallel, whereas state-modifying tools usually require sequential execution.

Here are some common use cases and benefits,

- **Research & Data Collection:** Launching multiple agents to scan different websites, expert reviews, and inventory systems simultaneously.
- **Software Development:** Using multiple agents for parallelized coding, testing, and debugging tasks.
- **Improved Resource Utilization:** Better utilization of computational resources, leading to higher efficiency and better handling of concurrent requests.
- **Fault Tolerance & Voting:** Running multiple agents for the same task to compare results, which increases robustness.

---

## Reflection

Reflection is a powerful design pattern where **autonomous agents evaluate, critique, and refine their own generated outputs, code, or plans before finalizing them**. By acting as a self-correcting feedback loop—often using a second "critic" agent—this process significantly improves accuracy, reduces errors in complex tasks like coding or writing, and enables higher-quality, multi-step problem solving.

- **The Process:** Instead of simply generating a final answer, an agent produces an initial output, reviews it for errors or weaknesses, and regenerates a better version.
- **"System 2" Thinking:** This approach mimics human critical thinking, allowing models to move beyond immediate, reactive, or "System 1" responses to more considered, methodical reasoning.

**Self-Correction Techniques:**

- **Self-Critique:** The agent analyzes its own output.
- **Tool-Assisted Reflection:** The agent uses external tools (e.g., executing code to check for errors or searching the web for fact-checking).
- **Multi-Agent Critique:** One agent generates content, while a second agent acts as a critic to provide feedback.
- This technique is highly effective for writing, code generation, data analysis, and complex planning.
- **Pros and Cons:** While it increases accuracy (e.g., boosting SQL query success rates), it requires more compute time and cost due to multiple iterations.

---

## Tool use (function calling)

Agentic AI function calling enables Large Language Models (LLMs) to act as **autonomous agents by dynamically invoking external tools, APIs, and databases using structured data (JSON)**. Instead of just generating text, **the AI decides which function to call based on user input, executes it, and uses the output for multi-step tasks, such as booking meetings or querying live data**.

- **Dynamic Decision-Making:** Agents analyze natural language, identify the need for external information, and select the appropriate tool.
- **Structured Output (JSON):** The model translates user requests into precise, machine-readable JSON objects that specify tool names and parameters.
- **Actionable Intelligence:** Function calling moves AI from passive reasoning to active, real-world execution (e.g., sending emails, updating databases).
- **Multi-Step Workflows:** Agents can orchestrate complex, sequential operations, such as checking a calendar, finding a meeting spot, and booking it.

**The Function Calling Workflow**

- **Request:** User submits a request, such as "What is the weather in India?".
- **Decision:** The LLM recognizes the limitation of its training data and identifies a get_weather(location) function.
- **Parameter Extraction:** The LLM extracts "India" as the parameter for the function.
- **Execution:** The application runs the function, calling the live API.
- **Return & Respond:** The tool's output is sent back to the LLM, which formulates a final, natural language answer.

**Best Practices for Implementation**

- **Descriptive Naming:** Use clear names and detailed descriptions for functions so the AI understands their purpose.
- **Low Temperature:** Set the model's temperature to 0 to ensure deterministic, consistent, and confident function choices.
- **Strong Typing:** Use specific data types (strings, integers, enums) for parameters to reduce errors.
- **Validation:** Implement guardrails to validate function outputs before taking critical actions.

---

## Planning

Planning in Agentic AI is **the process where an AI agent breaks down a complex, high-level goal into a sequence of smaller, manageable steps (sub-goals) before execution**. Unlike reactive AI, these agents use reasoning — often driven by Large Language Models (LLMs) — to anticipate future states, utilize external tools, and adjust strategies iteratively, enhancing reliability and efficiency in complex, multi-step tasks.

Here are some key components and approaches,

- **Goal Decomposition:** Breaking down a major request (e.g., "organize a conference") into smaller tasks (venue booking, agenda setting, speaker invitations).
- **Plan-and-Execute Pattern:** A structure where the AI first generates a full, detailed plan, then executes it, ensuring high traceability and reliability.
- **Interleaved Decomposition (ReAct):** A more dynamic, iterative method where the agent plans a step, acts, observes the results, and then adapts the plan.
- **Reflection & Self-Correction:** The agent evaluates its own actions and results, using feedback to correct its path if the initial plan fails.

There are various techniques for effective planning as follows,

- **Chain-of-Thought (CoT) Reasoning:** Prompting the agent to "think step-by-step" improves logical, multi-step reasoning.
- **Goal-Oriented Action Planning:** Selecting the best tools (APIs, databases) for each task in the sequence.
- **Memory Integration:** Retaining context from past steps to inform future decisions, preventing redundant efforts.

**Benefits**

- **Improved Accuracy:** Better at handling multi-step tasks, such as in logistics or complex coding projects, often outperforming basic LLM prompting.
- **High Adaptability:** Agents can update their plans when they receive new, unexpected information.
- **Independence:** Reduces the need for constant human supervision in long-running tasks.

---

## Multi-agent system

Multi-agent systems involve **multiple specialized AI agents collaborating, negotiating, and sharing knowledge to solve complex problems**, often coordinated by an orchestrator to increase efficiency, scalability, and performance.

Here are some key components of agentic multi-agent systems,

- **Autonomy:** Agents act independently to make decisions without constant human oversight.
- **Specialization:** Individual agents are trained or programmed to excel at specific sub-tasks within a larger workflow.
- **Collaboration/Orchestration:** Agents communicate and share data (like tool outputs or experiences) to work towards a common, complex goal.
- **Action-Oriented (Agentic Automation):** These systems bridge AI decision-making with execution tools (APIs, software) to perform actual work, not just provide answers.

**Advantages over Single-Agent Systems**

- **Improved Efficiency:** Specialization allows for faster, more optimized, and parallel task execution.
- **Scalability:** Systems can handle more complex, interdependent, and unpredictable tasks.
- **Flexibility:** Modular design allows for replacing or updating individual agents without disrupting the entire system.

**Typical Use Cases**

- **Complex Workflow Automation:** Managing end-to-end processes like software development (e.g., one agent writes code, another tests, another documents).
- **Negotiation & Transactions:** Using different agents to represent buy and sell sides in a market simulation.
- **Data Analysis & Decision Making:** Specialized agents gathering, analyzing, and reporting on data from multiple, disparate, and unstructured sources.

---

## Memory Management

Agentic AI memory management involves techniques like **short-term, long-term, and semantic storage (e.g., vector databases, knowledge graphs) to enable AI agents to retain context, learn from past interactions, and make informed decisions**. It operates through a **4-stage pipeline—extraction, storage, update, and retrieval—to overcome limited context windows**, ensuring agents are reliable, personalized, and capable of multi-step reasoning.

Here are some key types of agentic memory

- **Short-Term Memory (Context/Working Memory):** Temporary storage for active tasks, chat history, or session-specific data.
- **Long-Term Memory (Persistent/Knowledge):** Information stored for extended periods, such as user preferences or historical data, often using vector databases for semantic search.
- **Semantic Memory:** Structured understanding of entities and their relationships, typically managed via knowledge graphs.
- **Procedural Memory:** Knowledge of how to execute tasks or use tools.

**Memory Management Techniques**

- **Four-Stage Pipeline:** Extracting key info, storing it, updating it when new data arrives, and retrieving relevant context.
- **Summarization:** Condensing long conversations into concise summaries to save on context window usage.
- **Vector Embeddings:** Representing data in a multi-dimensional space to enable semantic retrieval of relevant memories.
- **Knowledge Graphs:** Mapping relationships to allow for deep, multi-hop reasoning and tracking changes over time.
- **Agentic Memory as a Service:** Centralized, shared memory systems that allow multiple agents to access and update common knowledge.

**Benefits of Robust Memory**

- **Context Continuity:** Maintaining continuity in long-term, multi-session tasks.
- **Personalization:** Adapting behavior based on past interactions with a user.
- **Improved Decision Making:** Learning from past mistakes and successes, enabling reflection loops.
- **Scalability:** Enabling agents to operate effectively on large datasets.

---

## Learning and Adaptation

Agentic AI systems use **continuous learning and adaptation to function autonomously in dynamic environments, moving beyond static, predefined rules to improve performance over time**. They employ online learning, memory management, and feedback loops to update knowledge, optimize tool usage, and personalize interactions based on past experiences and real-time data.

**Mechanisms for Adaptation:**

- **Feedback Loops & Memory:** Agents use memory (short-term, long-term, and episodic) and feedback to refine their decision-making and correct errors.
- **Reinforcement Learning (RL):** Agents maximize long-term rewards using algorithms like Deep Q-Networks and Proximal Policy Optimization.
- **Self-Reflection & Evaluation:** Agents assess their own performance and modify behaviors to avoid repeating mistakes.

**Adaptation Strategies:**

- **Domain Adaptation:** Adjusting behavior when transitioning to new environments or tasks.
- **User Personalization:** Learning individual user preferences to tailor interactions.
- **Skill Acquisition:** Developing new capabilities through practice and experience.
- **Framework for Adaptation:** Research suggests a framework classifying adaptation into agent-focused (improving the model) and tool-focused (improving interaction with external tools), often using Reinforcement Learning to turn failures into training data, such as Direct Preference Optimization (DPO).

**Benefits:**
These capabilities enable AI to deliver higher proactivity, improved efficiency, and better handling of complex, changing tasks. For instance, an e-commerce agent can analyze customer behavior in real-time to adjust recommendations, or an educational agent can personalize learning paths.

---

## Goal Setting and Monitoring

Agentic AI operates by **taking high-level human objectives and autonomously breaking them into smaller, executable tasks to achieve specific outcomes. Through continuous monitoring, these agents track progress against set goals, adjusting strategies and using tools (APIs, software) to overcome obstacles in real-time.**

**Goal Setting**

- **Definition:** Humans provide the "what," and AI defines the "how" (planning, scheduling, and prioritizing).
- **Proactive Action:** Unlike reactive chatbots, agentic AI acts autonomously, identifying necessary actions without constant, step-by-step human instruction.
- **Contextual Understanding:** Goals are set within defined, often complex, parameters such as budget, time, and compliance constraints.
- **Iterative Refinement:** Agents can re-evaluate goals as new information emerges, refining strategies.

**Monitoring and Governance**

- **Real-time Tracking:** Systems monitor key metrics and intermediate steps, ensuring the agent is on track to meet the objective.
- **Performance Dashboards:** Tools provide visibility into AI actions, decisions, and data usage.
- **Guardrails & Safety:** Continuous monitoring prevents "over-optimization" (e.g., maximizing efficiency at the cost of safety or regulations) and allows for human intervention.
- **Feedback Loops:** Agents use feedback to learn from outcomes, improving future performance.

**Examples**

- **Customer Support:** An agent aims to "resolve billing inquiry." It monitors conversation context, fetches data, and updates billing, escalating only if necessary.
- **Project Management:** An agent tracks milestones, identifies bottlenecks, and adjusts timelines based on real-time project data.
- **Logistics:** An agent optimizes routes and schedules to ensure on-time delivery while adhering to fuel cost constraints.

---

## Exceptional Handling

Exceptional handling in agentic AI **involves detecting, diagnosing, and mitigating runtime errors (tool failures, API issues) to prevent system crashes and ensure reliability**.

- **Proactive Detection & Diagnosis:** Modern agents don't just fail; they identify the root cause of an error (e.g., ConnectionTimeoutException) and classify it to determine the appropriate response.
- **Self-Correction & Retries:** Agents can autonomously attempt to fix issues, such as retrying a failed tool call or adapting their plan if a step fails.
- **Graceful Degradation & Fallbacks:** If a primary tool is unavailable, the agent might switch to a less capable tool or use cached data to provide partial results instead of failing completely.
- **State Management & Rollback:** When an error occurs during a multi-step task, agents must preserve context and, if necessary, roll back to a stable, previous state.
- **Human-in-the-Loop Escalation:** When an agent cannot resolve a problem, it escalates to a human agent, providing them with the context needed for intervention, which is crucial for high-stakes, enterprise-grade AI.
- **Preventing Cascading Failures:** Robust frameworks ensure that an exception in one module does not cause the entire system to crash or fail.

**Examples of Agentic Recovery**

- **Customer Service Bot:** If a backend database is down, the agent detects the API error and notifies the user to try again later instead of crashing.
- **Automated Trading:** If a trade fails due to "market closed," the bot logs the error and adjusts its strategy, rather than repeatedly attempting the same action.

---

## Reasoning Techniques

Agentic AI reasoning techniques **enable AI agents to solve complex, multi-step problems autonomously through planning, tool use, reflection, and iterative loops**.

Here are some key agentic reasoning techniques. These systems enhance reliability by self-correcting and using external tools, acting as "investigators" rather than just predictors.

- **ReAct (Reason + Act):** Combines reasoning traces and task-specific actions (like searching a database or using a calculator) in an alternating, iterative fashion to solve problems dynamically.
- **Chain-of-Thought (CoT):** Forces the model to generate intermediate reasoning steps before arriving at a final answer, which improves performance on logic and math tasks.
- **Planning & Decomposition:** Breaks large, complex goals into smaller, manageable subtasks, which are then assigned to specific tools or agents.
- **Reflection & Self-Correction:** Agents evaluate their own output, check for errors, and refine their actions based on previous results.
- **Tool Use/Function Calling:** Agents autonomously decide when and how to use external tools (APIs, search engines, code interpreters) to gather data or process information, rather than relying solely on pre-trained knowledge.
- **Multi-Agent Collaboration:** Multiple agents with specialized roles interact and share knowledge to solve problems, such as a planner agent working with a researcher agent.

**Classical Reasoning Methods in Agents**
Agents often apply traditional logical methods to ground their decisions:

- **Deductive Reasoning:** Applying general rules to specific cases (e.g., "If A, then B"). It is frequently used for compliance and enforcing business rules.
- **Inductive Reasoning:** Forming generalizations based on specific observations. This is the core of predictive analytics and fraud detection.
- **Abductive Reasoning:** Inferring the most likely explanation for incomplete observations. It is vital for medical diagnosis and IT troubleshooting.
- **Analogical Reasoning:** Solving new problems by finding parallels with known past scenarios.

**Core Components of the Reasoning Loop**
Agentic AI operates through a cyclical process rather than a single-shot response:

- **Plan:** Determine the steps necessary to achieve the goal.
- **Observe:** Review output from actions.
- **Act:** Execute tools to retrieve data.
- **Adapt:** Refine the plan based on observations.

---

## Guardrail and safety techniques

Guardrail and safety techniques in Agentic AI are essential, **multi-layered security measures—including input filtering, output moderation, human-in-the-loop (HITL) checks, and structural constraints—designed to ensure AI agents operate within ethical, compliant, and functional boundaries**. These prevent prompt injections, data leaks, and unauthorized actions.

Here are some guardrail techniques,

- **Input Filtering (Pre-execution):** Acts as a first line of defense to catch malicious prompt injections, jailbreaks, and unsafe content before they reach the agent's reasoning engine.
- **Output Moderation:** Scans generated responses for PII (personally identifiable information), toxic content, or hallucinations before they reach the user.
- **Action/Tool Constraints:** Restricts what tools or APIs an agent can call, requiring human authorization for high-risk operations (e.g., sending emails, executing trades).
- **Human-in-the-Loop (HITL):** A mandatory oversight mechanism where, for critical, uncertain, or sensitive decisions, the agent is paused, and a human must approve the action.
- **Deterministic Rule-Based Systems:** Predefined logic, schemas, and structural constraints that force the AI to operate within strict boundaries regardless of its reasoning process.
- **Monitoring and Behavioral Analysis:** Continuous, real-time tracking of agent actions to detect anomalies or "hallucinations" (unusual, unsafe behavior) as they happen.
- **Data Privacy Guardrails:** Automated redaction or anonymization of sensitive data in inputs and outputs to ensure compliance and prevent data breaches.

**Best Practices for Implementation**

- **Modular Design:** Create reusable guardrail components that can be applied across different AI workflows.
- **Collaborative Development:** Involve legal, security, and data teams to align guardrails with business and regulatory risks.
- **Continuous Evaluation:** Use red teaming to test and refine agent safety, ensuring the system can adapt to new security threats.

---

## Evaluation and monitoring

Evaluation and monitoring in Agentic AI involves **continuously assessing autonomous, multi-step workflows for task success, tool accuracy, and safety, rather than just output quality**.

Some key techniques include "LLM-as-a-Judge" for automated evaluation, tracing agent decisions to identify reasoning errors, and monitoring for drift/hallucinations to ensure reliability in production.

Evaluation goes beyond chatbots, measuring the process of reaching a goal, not just the final text.

- **Task Success Rate:** Does the agent achieve the final objective?
- **Tool/Action Accuracy:** Did the agent select and use the correct tool (e.g., API, database) for the step?
- **Trajectory/Path Efficiency:** Did the agent take an optimal path, or did it get stuck in loops?
- **Safety and Compliance:** Measures for hallucination rates, toxic content, and adherence to security guardrails.
- **Cost and Latency:** Tracking token usage, computational resources, and time-to-first-token.

**Evaluation Methods**

- **Offline Evaluation (Pre-deployment):** Using "golden datasets" of expected behaviors to test agents in simulation, ensuring they follow instructions before going live.
- **LLM-as-a-Judge:** Using a more advanced, larger model to evaluate the outputs and intermediate steps of the agent.
- **Human-in-the-Loop (HITL):** Incorporating human feedback to audit results, especially for high-stakes or ambiguous tasks.
- **Trajectory Evaluation:** Analyzing the entire sequence of actions (thought, action, observation) rather than just the final answer.

**Monitoring in Production**

- **Real-time Observability:** Detailed logging of steps, tool calls, and LLM prompts to troubleshoot why an agent failed.
- **Drift Detection:** Identifying if the agent’s performance degrades over time due to changing user inputs or external data changes.
- **Constraint Monitoring:** Ensuring the agent stays within defined operational boundaries (e.g., not exceeding spending limits or violating safety rules).

**Challenges**
Evaluating agents is complex because they are dynamic and often multi-turn, meaning one error in an early step can cascade through the entire workflow, making it difficult to pinpoint the root cause of failure.

---

## Advanced prompting for agentic AI

Advanced prompting for agentic AI involves techniques that enable autonomous agents to reason, plan, and use tools to complete complex, multi-step tasks.

- **ReAct (Reasoning and Acting):** Combines, in a prompt, the agent's reasoning process with action steps (e.g., using a calculator, searching the web, running code) to solve problems.
- **Chain-of-Thought (CoT):** Prompts the model to break down complex problems into smaller, logical, step-by-step reasoning steps before providing the final answer.
- **Tree-of-Thoughts (ToT):** Extends CoT by exploring multiple reasoning paths (branches) at each step, evaluating them, and selecting the best path for complex, non-linear planning.
- **Reflexion (Self-Reflection):** Asks the model to critique and rewrite its own outputs, allowing for self-correction and reduction of errors without human intervention.
- **RAG (Retrieval-Augmented Generation):** Prompts the agent to retrieve external, up-to-date documents to ground its answers, reducing hallucinations.
- **Meta Prompting:** Instructs the AI to analyze the query first, and then suggest its own best method or structure for solving the task.
- **Prompt Chaining:** Breaks a complex workflow into smaller, sequential prompts, where the output of one step becomes the input for the next.
- **Few-Shot Prompting:** Provides 1–5 examples in the prompt to teach the agent specific formats, styles, or logic, improving consistency in task execution.

**Structural Approaches for Agentic Prompts**

- **Dynamic Prompting:** Adapts prompts automatically using templates, user context, or metadata.
- **Negative Prompting:** Explicitly tells the AI what to avoid, which is crucial for safety and accuracy in sensitive tasks that can act as a gaurdrail.

**Benefits of Advanced Prompting in Agentic AI**

- **Improved Accuracy:** Reduces errors and hallucinations through structured reasoning.
- **Autonomous Workflow:** Enables agents to handle multi-step, complex, and unpredictable tasks independently.
- **Explainability:** Provides a clear trace of the agent's thought process and reasoning steps.
- **Tool Usage:** Allows agents to interact with external tools and APIs for real-time data.

---

### Context drift

Context drift is the **gradual degradation of an AI model's accuracy and relevance during long, multi-turn conversations or tasks, where it loses track of original user intent, constraints, or topic.** **As context windows fill up, the AI may start relying on inaccurate assumptions**, leading to inconsistent, contradictory, or off-topic, and sometimes nonsensical, responses.

**What happens when context drift?**

- **Memory Loss:** As the conversation lengthens, earlier instructions, user constraints, or critical details are "forgotten" or deprioritized, leading to contradictions.
- **Topic/Goal Misalignment**: The AI slowly shifts away from the original intent, such as changing a coding task from "Python optimization" to "C++ restructuring" without prompting.
- **Compounding Errors**: Small, initial inaccuracies compound over time, leading to significant deviations, similar to a navigation system that is 1 degree off.
- **Passive Adoption of Suboptimal Content**: The AI may start adapting to its own previously generated, suboptimal, or incorrect output, reinforcing the drift.

**What are the causes and scenarios?**

- **Limited Context Windows**: Models have a finite capacity to remember previous, which, when exceeded, causes early conversation details to be dropped.
- **Long-Form/Multi-Turn Interaction**: Complex, multi-step, or extended interactions increase the likelihood of drift.
- **Parallel Agents**: Using multiple AI agents simultaneously often leads to conflicting contexts, where each agent works off a slightly different, diverging set of assumptions.
- **Ambiguous User Prompts**: Vague instructions, missing details, or frequent context resets make it easier for the model to lose direction, produce irrelevant or inconsistent responses, and require additional clarification to stay on track.

**Mitigation Strategies**

- **Prompt Engineering/Hygiene**: Periodically restate core objectives and constraints in the prompt to "remind" the AI of the original task.
- **Modularization**: Break long tasks into smaller, independent chunks to prevent long-term dependency issues.
- **Context Resetting**: Manually clearing the session and starting a new chat when the AI's output becomes irrelevant or chaotic.
- **Externalizing Memory**: Using external tools, like vector databases, to store and recall relevant information outside the model's immediate context window.

---

### Context window overflow

Context window overflow (CWO) occurs **when the total tokens in an LLM prompt—input, system instructions, and RAG data—exceed the model's capacity**. This causes lost information, incoherent responses, and application failures**. It is a **memory limitation issue prevalent in long, multi-step tasks or RAG systems.\*\*

**What are some causes of context overflow?**

- **Excessive Input**: Passing very long documents or largse amounts of RAG data.
- **Long Conversation History**: Chatbots that do not summarize or prune past interactions.
- **System/Tool Prompts**: Large, complex instructions that consume too many tokens before user input is processed.

**Solutions and Mitigation Techniques**

- **Vector Search/RAG:** Instead of feeding all data, use vector search to retrieve only the top relevant chunks.
- **Context Compression:** Implement summarization for older conversation parts.
- **Chunking:** Break down large documents into smaller segments (e.g., 500-800 tokens) before insertion.
- **Dynamic Context Management:** Use tools that intelligently filter information and remove less essential, older data from the prompt.
- **Streaming and Monitoring:** Monitor token usage and implement streaming to manage long outputs.

---

## Prompt injection

Prompt injection is a security vulnerability where attackers embed malicious, hidden instructions into LLM inputs, overriding original system prompts to force unintended actions. It exploits the inability of LLMs to distinguish between developer commands and user input, leading to data exfiltration, system manipulation, and bypassed security.

- **Mechanism:** Attacks bypass security by mixing user-provided input with trusted system instructions, tricking the model into following the user's "new" rules.
- **Types of Injection:**
  - Direct Injection: Explicit, malicious prompts given directly to the AI.
  - Indirect Injection: Hidden commands in external data, such as websites, documents, or emails, which the LLM processes.

- **Impact and Risks:**
  - Data Leakage: Accessing confidential information.
  - Action Manipulation: Forcing the AI to perform unauthorized actions or bypass authentication.
  - Content Fraud: Spreading misinformation or generating biased outputs.
  - Tool/API Hijacking: Forcing agents to use external tools inappropriately.

- **Defense Measures:**
  - Sanitization: Cleaning input to remove potentially malicious tokens.
  - Monitoring: Logging and analyzing interactions for anomalies.
  - Context Separation: Attempting to separate system instructions from user inputs, though this is challenging.

---

## How to manage context between AI agents?

Managing context between AI agents involves passing state via shared memory, summarizing previous conversations, or using structured data (JSON/stringified payloads) to hand off relevant information while discarding unnecessary noise.

**Top Strategies for Multi-Agent Context Management**

- Context Serialization & Passing: As an agent finishes its task, serialize the relevant output (e.g., to JSON) and pass this payload to the next agent’s input or call.
- Shared Memory/State Repository: Use a centralized database or document (e.g., a "planning doc" or vector store) that agents can read from and write to, allowing them to persist information across turns.
- Hierarchical Summarization: Compress older conversation segments or previous agent findings into a concise summary before passing them to the next agent, preserving essential information while saving tokens.
- System Prompt Injection: Dynamically update the next agent's system prompt with key context, such as the user's goal, the results of previous steps, or necessary data points.
- Context Trimming/Filtering: Actively remove obsolete or irrelevant information, such as clearing previous tool outputs, before transferring to the next agent to prevent "context rot" and reduce token usage.
- Selective Data Access: Rather than passing the entire history, allow agents to use tool calls (e.g., via MCP servers) to fetch specific data only when needed, minimizing the upfront context load.

**Best Practices**

- Divide and Conquer: Break complex, long-running tasks into smaller, focused tasks where each agent operates on a minimal, relevant subset of the total context.
- Avoid "Pattern Overfitting": When passing histories, introduce slight variations in prompting to prevent agents from becoming too accustomed to a specific, potentially incorrect, pattern.
- Maintain Continuity: Use consistent identifiers for the task, such as a session ID, to link the context across different agent interactions.

---

## Fault-tolerant AI agents

Fault-tolerant AI agents ensure operational continuity and reliability despite failures by utilizing mechanisms like retry policies, model fallbacks, state checkpointing, and sandboxing. These systems, often implemented using frameworks like LangGraph, prevent data loss and inconsistent states during multi-step tasks or API outages.

Here are some key strategies for Fault-Tolerant AI Agents,

- Retry Policies: Automatically retries failed API calls or model requests to manage transient errors.
- Model Fallbacks: Switches to alternative models (e.g., from OpenAI to Anthropic) if the primary provider fails.
- Checkpointing & Persistence: Saves the state of a workflow (e.g., using PostgresSaver) to allow resuming from the point of failure rather than restarting.
- Error Classification: Distinguishes between transient, LLM-recoverable, and fatal errors to apply appropriate recovery actions.
- Sandboxing: Executes agent actions in isolated environments, often using transactional file systems, to ensure safety and prevent malicious or accidental damage.
- Multi-Agent Resilience: Uses attention mechanisms to detect when an agent fails within a multi-agent system, allowing the system to compensate and continue functioning.

**Implementation Considerations**

- State Management: Agents should have schema-validated, persistent state to maintain consistency, especially when dealing with complex, multi-step workflows.
- Monitoring & Observability: Detailed logs and traces are necessary to understand failures, particularly in complex agent loops.
- Structural Reliability: Using structured concurrency and frameworks like Jido helps manage tasks and ensure they do not run uncontrollably, which can waste resources.

---

## What is Production-grade AI agent?

Productionizing an AI agent involves moving from a simple prompt-based script to a robust, systems-engineering approach. Success depends on shifting from thinking in prompts to thinking in workflows that emphasize reliability, observability, and safety.

**1. Architectural Foundations**
A production-grade agent requires a multi-layered architecture beyond a basic LLM call.

- State Management: Transition from in-memory storage to persistent databases like PostgreSQL or Redis to ensure sessions survive restarts and support "time-travel" debugging.
- Execution Models: Choose between stateless (simple requests), stateful (conversations), or event-driven patterns for long-running, asynchronous tasks.
- Specialization: Instead of one "mega-agent," use a multi-agent approach with specialized roles (e.g., Router, Researcher, Validator) to reduce confusion and improve accuracy.

**2. Tool Design & API Reliability**
Agents interact with the world through tools, which must be engineered for stability.

- Idempotency: Ensure calling a tool multiple times with the same arguments has no unintended side effects (e.g., it shouldn't book two meetings if a timeout occurs).
- Self-Healing: Implement logic that allows the agent to recognize tool failures and automatically retry or try an alternative method.
- Structured Outputs: Use libraries like Pydantic to enforce strict output schemas, ensuring the agent provides machine-readable data that won't break downstream services.

**3. Guardrails & Security**
Production environments require strict control over what an agent can see and do.

- Input/Output Filtering: Implement firewalls to detect prompt injection, PII (Personally Identifiable Information) leakage, and out-of-scope requests.
- Human-in-the-Loop (HITL): Require explicit human approval for high-stakes actions like financial transactions or deleting records.
- RBAC (Role-Based Access Control): Grant agents the minimum necessary permissions to access specific internal data and APIs.

**4. Observability & Evaluation**
You cannot maintain what you cannot see. Tracing is critical for debugging probabilistic LLM behavior.

- Structured Tracing: Use platforms like LangSmith or Langfuse to monitor every reasoning step, tool call, and token cost.
- Continuous Evaluation: Maintain an "evaluation set" of 100+ real-world scenarios to test the agent's performance weekly and detect accuracy drift.
- Cost Monitoring: Set up alerts for token consumption spikes and track Cost Per Task to ensure the agent's ROI remains viable.

**5. Deployment Pipeline**

- Containerization: Use Docker and Kubernetes for scalable, portable deployments.
- Standard Protocols: Leverage the Model Context Protocol (MCP) to standardize how agents discover and connect to your existing business systems securely.

---

## How to create a custom AI agent?

To create a custom AI agent, I would start by defining a narrow, high-value use case and creating a detailed system prompt for personality and constraints. Next, I would equip the agent with essential tools (e.g., search, API connectors) and relevant knowledge bases. Finally, I would use frameworks like Langchain, Pydantic AI for development, followed by iterative testing to optimize performance and reliability.

**Step-by-Step Approach for creating an AI Agent**

- **Define Scope & Purpose:** Clearly define the specific problem the agent will solve, who will use it, and what success looks like.
- **Establish the Brain & Prompting:** Select an LLM (e.g., GPT-4, Claude 3.5) and create a detailed system prompt defining its persona, constraints, and instructions.
- **Equip with Tools (Actions):** Connect the agent to external applications, such as Gmail, Slack, CRM systems, or web search tools, allowing it to perform actions.
- **Integrate Knowledge Bases:** Connect specific, curated data sources (PDFs, websites, databases) so the agent has specialized knowledge for its tasks.
- **Implement Memory & Context:** Enable memory to allow the agent to track progress, recall past interactions, and handle multi-step workflows.
- **Test & Deploy:** Use testing environments (e.g., Botpress, Voiceflow) to refine responses, followed by deployment for live use.

**Key Considerations**

- **Security:** Implement proper authentication and permission management, especially if the agent has access to sensitive data or can act on your behalf.
- **Iterative Design:** Start with a simple version and add complexity, such as specialized knowledge or multiple tools, only when necessary.
- **Evaluation:** Set up performance benchmarks to ensure the agent meets accuracy targets before full implementation.

---

## Challenges in developing multi-agent systems

Developing multi-agent systems (MAS) involves significant challenges, primarily centered around coordination, communication, and managing emergent, often unpredictable, behaviors.

Key hurdles include ensuring efficient, secure, and accurate communication between agents, handling high latency and computational costs, and debugging complex, multi-step workflows.

- **Coordination and Collaboration:** Agents often struggle with role ambiguity, leading to duplicate efforts, resource contention, or deadlocks. Effective task decomposition and maintaining shared goals across agents is difficult.
- **Communication and Information Sharing:** Designing protocols that prevent agents from over-communicating or failing to share critical data is a major issue.
- **Unpredictable Emergent Behavior:** When multiple autonomous agents interact, they may exhibit un-designed, erratic, or conflicting behaviors that are hard to debug and control.
- **Reliability and Error Propagation:** If one agent fails or provides false information, the error can cascade through the system, leading to widespread failures.
- **Scalability and Performance:** As more agents are added, system latency increases and, if powered by Large Language Models (LLMs), costs can rise exponentially.
- **Security and Trust:** Malicious agents or external attacks can compromise the system by manipulating data, demanding robust, secure, and trustworthy communication channels.
- **State Management:** Maintaining consistent, long-term context across multiple agents in complex, long-running processes is technically challenging.

**Key Considerations for Mitigation:**

- **Action Schemas:** Using strict, predefined schemas for agent actions can help reduce ambiguity.
- **Durable Execution:** Implementing mechanisms that allow agents to resume from errors rather than restarting from scratch is essential for long-running workflows.
- **Rigorous Testing:** Due to the non-deterministic nature of MAS, specialized, intensive testing and monitoring are required to ensure stability.

---

## Challenges of Multi AI agents in production

Multi-AI agent systems in production face significant hurdles, including non-deterministic, unpredictable behaviors, complex orchestration of inter-agent communication, and high latency due to sequential processing.

Key challenges include managing shared state and memory, debugging "black box" agent interactions, ensuring data privacy/security, and managing high costs.

- **Non-Determinism and Reliability**: Agents may produce different outputs for the same input, making them hard to trust and validate. They can "go rogue" or exhibit unpredictable behavior.
- **Orchestration and Communication:** Managing interactions between multiple specialized agents is complex. Conflict resolution is necessary when agents have opposing goals (e.g., one agent trying to reduce inventory while another tries to maximize availability).
- **Latency and Performance:** Sequential processing, where one agent relies on the output of another, can lead to significant delays in user-facing applications.
- **Debugging and Observability:** When agents fail, it is difficult to determine which agent failed, why it failed, or how to debug the interconnected system.
- **Memory and Context Management:** Maintaining consistent context across long, multi-turn interactions is difficult, as models often hit token limits.
- **Security and Privacy:** Agents often have high-level access to sensitive data, creating risks for data leakage, unauthorized access, and prompt injection attacks.
- **High Costs:** Operating multiple agents, especially those relying on large language models (LLMs), can lead to high computational and API costs.
- **Integration with Legacy Systems:** Connecting modern, autonomous agents with older, non-API-friendly systems is a major technical hurdle.

Here are some key considerations for success,

- **Rigorous Testing:** Due to "regression invisibility," small changes in one agent can break the entire system.
- **Governance and Monitoring:** Daily, active management and human oversight are necessary.
- **Start Simple:** It is often better to use a single, highly capable agent or a hierarchical structure before moving to a fully distributed multi-agent system.

---

## Guardrails for agentic systems

Guardrails for agentic systems are essential, real-time safety mechanisms designed to manage the risks associated with autonomous, multi-step AI actions. Unlike static AI, agents connect to live systems, APIs, and data, requiring a,layered, "defense-in-depth" approach to prevent unauthorized actions, data exposure, and misuse.

Here are the various types of guardrails for agentic systems:

**1. Architectural & Input/Output Guardrails**
These guardrails operate at the perimeter, validating data flow to and from the agent.

- Input Sanitization (Pre-processing): Blocks prompt injections, jailbreak attempts, and filters irrelevant requests before they reach the model.
- PII & Data Redaction Filters: Identifies and masks Personally Identifiable Information (PII), PHI, or PCI data in input/output to prevent data leakage.
- Output Validation: Scans generated content for toxicity, bias, inappropriate content, or hallucinations.
- Structured Output Enforcement: Ensures the AI generates formatted data (e.g., JSON, SQL) that conform to expected schemas.

**2. Operational & Action Guardrails (Tool Use)**
These control the actions an agent can take, particularly with external tools.

- Action Authorization (Human-in-the-Loop - HITL): Requires manual human approval for sensitive or high-impact actions (e.g., sending emails, making payments, modifying code).
- Tool/API Allow-listing: Strictly restricts the tools, APIs, or databases an agent can access, enforcing the principle of least privilege.
- Rate Limits and Quotas: Limits the number of API calls or actions in a given timeframe to prevent runaway loops, excessive costs, or system crashes.
- Dry-run Modes: Allows for simulating an action to validate its outcome before actual execution.

**3. Behavioral & Intent Guardrails**
These monitor the "reasoning" process of the agent.

- Intent/Goal Validation: Ensures the agent’s actions align with the defined business objective, preventing it from straying into prohibited territory.
- Confidence Thresholds: Requires a high confidence score from the agent before executing an action, triggering escalation if confidence is low.
- Runaway Loop Detection: Monitors for repetitive, circular reasoning and terminates the task if the agent gets stuck.

**4. Security & Compliance Guardrails**
These focus on regulatory requirements and system integrity.

- Identity & Access Management (RBAC/ABAC): Assigns unique identities to agents rather than sharing credentials, using Role-Based Access Control to govern permissions.
- Contextual Guardrails: Ensures the agent understands the conversational or environmental context to avoid inappropriate or irrelevant responses.
- Audit Trails & Logging: Maintains detailed, immutable logs of all inputs, outputs, decisions, and tool invocations for post-mortem analysis and compliance (e.g., GDPR, HIPAA).

**5. Adaptive & Runtime Guardrails**
These are dynamic mechanisms that evolve with the system.

- Anomaly Detection: Uses machine learning to detect unusual, non-deterministic behaviors or abnormal data queries that fall outside expected baselines.
- Graceful Fallback Mechanisms: Allows the agent to step down to a less-capable, more restricted mode if the primary system encounters errors or safety breaches.
- Continuous Evaluation/Red Teaming: Regularly stress-testing the agent with adversarial inputs to identify and fix weaknesses.

**Implementation Frameworks**
Several tools can be used to implement these guardrails:

- Native Tools: AWS Bedrock Guardrails, Azure AI Content Safety, OpenAI Moderation API.
- Open Source/Frameworks: NeMo Guardrails (NVIDIA), Guardrails AI, LlamaGuard (Meta), LangGraph (LangChain).
- Enterprise Solutions: BigID, HiddenLayer, Cequence.

---

### What are some common mistakes when creating AI agents?

Common mistakes when creating AI agents include tool overload, vague instructions, poor context management (resulting in high token costs), and ignoring data security. Effective agents require clear roles, specialized tools, and robust evaluation to avoid unpredictable, costly, or insecure behavior.

Here are some key Pitfalls to Avoid:

- **Tool Overload and Poor Implementation:** Giving an agent too many tools overwhelms it, leading to poor performance. Tools must have clear, descriptive names and precise documentation to function correctly.
- **Vague Role Definition:** Failing to clearly define the agent's specific role, objectives, and boundaries leads to unpredictable, chaotic behavior.
- **Poor Context Management:** Passing excessive or irrelevant conversation history causes token counts to explode, significantly increasing costs.
- **Ignoring Data Governance:** Allowing agents to access sensitive, unverified, or poorly tagged data creates high security and brand risks.
- **Over-reliance on Output:** Blindly trusting that the LLM will always produce valid, structured data (e.g., JSON) without validation leads to broken workflows.
- **Ignoring Real User Workflows:** Building for hype rather than solving specific, real-world user problems often results in useless agents.
- **Inefficient Multi-Agent Architecture:** Over-complicating systems with too many agents ("multi-agent spaghetti") leads to, high latency, and difficult debugging.

**Best Practices:**

- Define strict boundaries for what the agent can and cannot do.
- Implement data privacy and permission logic.
- Test rigorously with realistic, varied scenarios.
- Keep agents specialized rather than trying to make a "jack-of-all-trades".

---

## How to save costs in a multi-agent system?

Saving costs in a multi-agent system involves using smaller models for simple tasks and large models for complex reasoning, caching frequent LLM queries, and implementing strict token/budget limits per agent. Additional strategies include using specialized, smaller models for routine tasks, optimizing vector database usage, and monitoring API usage to prevent runaway costs.

**Top Cost-Saving Strategies:**

- Model Routing (Small vs. Big): Use smaller, specialized models for execution and reserve powerful, expensive models (e.g., GPT-4) only for complex reasoning.
- Semantic Caching: Implement a cache layer to store previously queried data, which prevents repetitive, expensive calls to LLMs.
- Budgeting & Limits: Set hard token budget caps per agent and per run to prevent runaway costs, especially with recursive agent loops.
- Efficient Tool Selection: Train agents to use cheaper data sources first, escalating to premium APIs only when necessary.
- Infrastructure Optimization: Use open-source models where possible, right-size compute resources, and delete idle instances.
- Vector Database Optimization: Use vector databases only when absolutely necessary, as they can add significant costs.
- Batching Requests: Instead of individual calls, batch API requests to reduce cost per record.

**Techniques to Reduce API/Token Usage:**

- Cache Plan Templates: Rather than caching full outputs, cache the structured plans or chains of thought.
- Result Verification: Use a "Judge" step to validate outputs to avoid re-running entire workflows.
- Memory Quantization: Use quantization techniques (e.g., INT8/INT4) for K/V storage to reduce memory and bandwidth usage.

Key Takeaway: A well-designed multi-agent system, which assigns specialized, smaller models for simpler tasks, can significantly reduce costs (sometimes by over 90%) compared to a single, large model approach.

---

## How to handle user interruptions in a multi-agent system (MAS)?

Handling user interruptions in a multi-agent system (MAS) requires a robust orchestration layer that manages state, prioritizes user intent, and allows for rapid context switching. Effective strategies include using "human-in-the-loop" (HITL) checkpoints, implementing dynamic, stateful conversation management, and ensuring agents can pause, resume, or abort tasks mid-execution.

Here are some key interruption handling strategies,

- **Interrupt & Resume (Durable Execution):** Using frameworks like LangGraph, the agentic workflow is paused at the exact point of interruption, allowing the system to save its state (checkpointer) and resume later from the last successful step.
- **"Accept & Pivot" Strategy**: Research suggests that accepting interruptions immediately and letting the user speak ("Accept" strategy) leads to higher user satisfaction, making the agent seem more agreeable and stable.
- **Hierarchical Supervisor Pattern:** A central "manager" agent interrupts current sub-agents, gathers the new user request, and decides whether to abort the current task or resume it later.
- **Stateful Context Management:** The system maintains a "stack" of tasks. When interrupted, the current agent pushes its context to the stack, handles the new request, and then pops the original task back to resume.
- **Compensation Logic:** If a user interrupts and changes direction, the system initiates compensation logic to undo or reverse actions taken by a previous, now-invalidated agent action.

**Implementation Techniques**

- Voice/Chat VAD (Voice Activity Detection): In voice-based systems, using a short silence time (e.g., 600-1200ms) allows for immediate detection of an interruption while still ensuring the user has enough time to speak.
- Keyword Triggering: Pre-setting keywords like "stop" or "pause" forces the orchestration layer to halt current tasks immediately.
- Idempotent Actions: Ensuring tool actions are idempotent (safe to run multiple times) ensures that if an interruption occurs during a tool call, retrying the task won't cause errors or duplicate work.

**Handling Scenarios**

- If the user asks a follow-up question: The agent pauses, addresses the new query using a temporary sub-agent, and then resumes the original workflow.
- If the user wants to cancel: The system calls to clear the current task stack and reset to a base state.
- If the user is rude/aggressive: The agent acknowledges the interruption but maintains its "turn" to wrap up essential information before yielding.

---

## How to handle infinite loops?

Handling infinite loops in AI agents involves setting hard limits on iterations (e.g., 5-10 steps), implementing timeout mechanisms, and monitoring state changes to detect, stop, or escalate trapped processes.

Key strategies include implementing circuit breakers, logging, and using human-in-the-loop intervention.

- Set Hard Limits: Implement maximum iteration counts for agent tasks to prevent endless loops.
- Define Stopping Conditions: Explicitly define criteria for task completion or failure.
- Implement Timeouts: Add time-based limitations on how long an agent can run.
- Monitor State Changes: Track changes between iterations; if the agent revisits the same state, trigger a break.
- Implement Circuit Breakers: Use mechanisms that halt execution if specific error thresholds are crossed.
- Human-in-the-Loop: Escalate to a human operator if the agent exceeds expected bounds or gets stuck.
- Log and Audit: Maintain detailed logs of agent actions, inputs, and outputs to diagnose loop causes.

**Common Causes**

- Agents often get stuck due to misinterpreting tasks.

---

## How to decide whether to change a Large Language Model (LLM) for a specific use case?

Deciding whether to change a Large Language Model (LLM) for a specific use case requires moving beyond "vibes" (subjective, one-off testing) to a systematic, data-driven evaluation framework. The decision is based on comparing model performance across four key pillars: Accuracy, Quality, Cost, and Latency, ideally using a "golden dataset" of representative, human-labeled examples.

Here is a step-by-step approach to decide if a model change is beneficial:

**1. Build a "Golden Dataset" & Define Metrics**

- Create a Representative Dataset: Curate 50–100+ examples that mimic real-world usage, including edge cases, tricky queries, and expected "good" answers.
- Define Metrics:
  - Accuracy: Factual correctness (e.g., in RAG applications, is the answer grounded in the provided context?).
  - Quality: Adherence to instructions, format (e.g., JSON validity), tone, and coherence.
  - Latency: Time-to-first-token (TTFT) and total response time, crucial for interactive apps.
  - Cost-Efficiency: Cost per 1,000 tokens (input + output).

**2. Implement Systematic Evaluation Methods**

Do not rely on one-off prompts. Use a combination of methods:

- LLM-as-a-Judge (Automated): Use a stronger model (e.g., GPT-4o, Claude 3.5 Sonnet) to evaluate the outputs of your test model (e.g., Mistral, Llama 3) based on a prompt-defined rubric.
- Deterministic Checks (Code-based): Use code to verify if the output is valid JSON, contains required fields, or matches a specific regex pattern.
- Human Evaluation (Spot Checks): Have domain experts review a subset of the results to ensure that the "LLM-as-a-Judge" aligns with human preferences.

**3. Run Head-to-Head (H2H) Comparisons**

- Run your golden dataset through the Current Model and the New Candidate Model using identical prompts, temperature (ideally 0 or very low for consistency), and context.
- Compare the results on a spreadsheet or in an eval tool (e.g., Promptfoo, LangSmith, DeepEval).

**4. Analyze Results**

- Better Answers: The new model consistently outperforms the old one on critical metrics (e.g., higher factual correctness, better adherence to tone) while staying within budget and speed requirements.
- Worse Answers: The new model hallucinated more frequently, deviated from required formatting, or was prohibitively slow/expensive, even if it "sounded" better.

**When to Change LLMs**

- Quality Regression: The current model is frequently missing crucial information or failing to follow instructions.
- High Latency/Cost: The current model is too slow or expensive for the required throughput, and a smaller, more specialized, or newer model can provide similar quality at a lower cost.
- Data Security/Privacy: You need to move from a proprietary API (e.g., OpenAI) to an open-source model (e.g., Llama 3) hosted on-premise.

**Key Pitfalls to Avoid**

- Overfitting to Benchmarks: High scores on public benchmarks (e.g., MMLU) often do not translate to better performance on specialized, domain-specific tasks.
- Neglecting Consistency: A model that is "smarter" but unpredictable can be worse than a consistent, less capable model.
- Ignoring Task-Specific Data: General-purpose models might perform worse than smaller, fine-tuned, or domain-specialized models.

---

## Pydantic

Pydantic is the leading data validation and settings management library for Python, designed to enforce type constraints at runtime. It allows developers to define data structures using Python type annotations, ensuring that input data conforms to specific types and constraints, making it an essential tool for building reliable, production-grade applications.

**What and Why We Need Pydantic**

- Runtime Validation & Type Safety: Unlike standard Python, which is dynamically typed, Pydantic ensures data accuracy by validating types at runtime, catching errors before they reach core application logic.
- Structured Data Parsing: It converts unstructured input (like raw API JSON, form data, or LLM responses) into validated Python objects (BaseModel) automatically.
- Settings Management: It provides a centralized and structured way to define, validate, and load settings, making it easy to validate and manage application configurations from environment variables and files.
- Performance: The validation logic is written in Rust, making Pydantic extremely fast.
- IDE Support: Because it uses Python's type hints, it provides excellent autocomplete and type checking in IDEs, enhancing developer productivity.

**Why Pydantic is Essential in Production AI Systems?**

Production AI systems—particularly those using Large Language Models (LLMs)—face the challenge of handling messy, unstructured, and unpredictable data. Pydantic acts as the "safety net" between the flexible, chaotic world of LLMs and the structured requirements of backend systems.

**1. Structured Output Validation:** LLMs often produce vague or malformed JSON. Pydantic enforces a strict schema, forcing the LLM to return data in a specific, expected format, such as a Pydantic .
**2. Reduced Hallucinations and Errors:** By enforcing output constraints, Pydantic reduces the likelihood of downstream systems failing due to unexpected data types or missing fields.
**3. Tool Use and Function Calling:** When agents use external tools (APIs, databases), Pydantic validates the arguments the LLM passes to these tools, ensuring they are valid before execution.
**4. Data Serialization & Ingestion:** In RAG (Retrieval-Augmented Generation) systems, Pydantic validates incoming user queries, document metadata, and retrieved snippets to ensure they conform to the input requirements of the embedding model.
**5. Reliability at Scale:** Many modern AI frameworks (FastAPI, LangChain, LlamaIndex, Instructor) rely on Pydantic, making it indispensable for ensuring data integrity across complex, multi-step agentic workflows.

In summary, Pydantic transforms LLMs from "text generators" into "reliable, typed, and structured software components".

---

## How to evaluate Multi-agent systems (MAS) in production?

Multi-agent systems (MAS) in production require monitoring beyond traditional software metrics (uptime, latency) to include behavioral, economic, and operational metrics. Because MAS often involve multiple LLM calls, tool usage, and interdependent tasks, key performance indicators (KPIs) must focus on reliability, cost-efficiency, and end-to-end task success.

Here are the key metrics and dimensions to consider, categorized by function:

**1. Task Success and Quality Metrics**

These metrics measure whether the agents achieved the desired, high-quality outcome, rather than just returning text.

- End-to-End Task Success Rate: The percentage of user requests successfully resolved without human intervention or fallback.
- Partial Completion Points: Identification of where failures occur in multi-step workflows to diagnose where a specific agent or subtask broke down.
- Goal Accuracy / Correctness: Whether the final output matches the required business logic or ground truth.
- Hallucination Rate: Frequency of unsupported or false claims within the output, particularly when using RAG (Retrieval-Augmented Generation).
- Role/Constraint Adherence: Measures if agents stay within defined personas, security boundaries, and policy constraints.

**2. Tool-Use and Reasoning Efficiency**
In agentic workflows, tools are often a primary source of failure.

- Tool Selection Accuracy: Did the orchestrator or agent choose the right tool for the subtask?
- Tool Call Success Rate/Error Rate: Percentage of tool calls that fail (due to API timeouts, bad input parameters, etc.).
- Execution Correctness: Measures if the tool's output was accurately parsed and used by the agent.
- Planning Efficiency: Evaluates if the agent reaches a solution directly or if it gets stuck in "analysis paralysis," taking too many unnecessary steps or tool calls.
- Redundant Call Rate: Identifies if agents are calling the same tool or performing the same research multiple times.

**3. Economic and Performance Efficiency (Cost & Latency)**
Multi-agent systems are resource-intensive; monitoring the "cost-to-value" ratio is critical.

- Cost per Transaction/Success: Total cost (API, infrastructure, tokens) divided by successful, not just attempted, tasks.
- End-to-End Trace Latency: Total time from user prompt to final resolution, including all agent-to-agent handoffs and tool execution times.
- Token Usage per Task: Monitoring the total input/output tokens to avoid runaway costs from infinite loops.
- Handoff Latency: Time spent between agents during delegation.

**4. Coordination and Reliability Metrics**
These monitor how agents work together.

- Escalation/Human Intervention Rate: Frequency at which the system fails and requires a human to take over.
- Error Cascade Rate: When one agent fails, how often does it cause downstream failures in other agents?.
- Deadlock/Loop Frequency: Number of times agents get stuck in circular dependencies (e.g., Agent A waits for B, who waits for A).
- State Consistency Violations: Checks if shared memory or context becomes desynchronized between agents.

**5. User-Centric Metrics**

- User Satisfaction (CSAT/NPS): Direct feedback on the quality of the interaction.
- Acceptance Rate/Correction Rate: How often the user accepts the agent's output without editing it.
- Conversation Length/Depth: Average number of turns, which can indicate if an agent is efficiently solving problems or engaging in excessive back-and-forth.

**Best Practices for Monitoring**

- Trace Everything: Log the entire "trajectory"—every prompt, response, tool call, and thought—to enable replay and debugging.
- Use "LLM-as-a-Judge": Use a more capable, specialized LLM to evaluate the outputs and intermediate reasoning steps of your production agents.
- Set Alerting on Symptoms: Alert when task success drops below a threshold (e.g., &lt;90%) rather than just when an individual API call fails.

---

## Memory Management for Long Conversations

Designing a memory system for an AI assistant that handles long, multi-session, and private conversations requires a hybrid approach, separating data by immediacy and importance. A high-performance, privacy-conscious architecture combines a fast short-term memory (STM) (e.g., Redis) for active conversation, a semantic long-term memory (LTM) (e.g., Pinecone/Weaviate) for deep context, and a structured database (e.g., Postgres) for persistent facts.

Here is a design based on best practices for performance and security.

**1. Storage Strategy**
To keep latency low, the system must avoid feeding the entire chat history into the LLM at once.

- Short-Term Memory (Session Scope - High Speed): Use an in-memory database like Redis to store the last 5–10 conversational turns. This keeps the immediate context (anaphora, current intent) ultra-fast for low-latency responses.
- Long-Term Semantic Memory (Global Scope - Vector Store): Periodically, the system embeds conversational chunks (using ) and stores them in a vector database (e.g., Pinecone).
- Structured Fact Storage (Persistent Profile - SQL): Extract high-value, durable entities (e.g., "User likes Python," "User lives in NYC") and store them in a secure relational database (Postgres).
- Privacy & Isolation:
  - Namespacing: All memory retrievals are strictly scoped by and to prevent cross-user data leakage.
  - Encryption at Rest: All stored memories are encrypted, with PII (Personally Identifiable Information) optionally anonymized before vectorization.

**2. Retrieval Strategy: Semantic & Proactive**
To maintain relevance without excessive token usage, retrieval must be precise.

- Hybrid Search (Dense + Sparse): Combine vector search (semantic meaning) with BM25 keyword search (exact term matching). This ensures the agent finds both conceptual, broad memories and specific names or IDs.
- Proactive Retrieval: When a user query arrives, a lightweight model (or the main LLM, if fast enough) decides if past information is needed. It queries the LTM/Vector store before responding, injecting only the top-k most relevant chunks into the prompt.
- Contextual Re-ranking: Use a re-ranking model to score the relevance of retrieved chunks, ensuring that only the most crucial information is included in the prompt to minimize token costs.

**3. Pruning & Memory Management Strategies**
To keep the system from becoming "trapped" by its own history or exceeding token limits, memory must be curated.

- Sliding Window (Short-Term): The earliest messages in the immediate, active session are dropped as new ones arrive, leaving only the most recent interactions.
- Recursive Summarization (Mid-Term): As a session ends or exceeds a size threshold (e.g., 50 turns), use a summary LLM to consolidate the raw chat history into a succinct summary.
- Fact Extraction (Long-Term): Instead of storing raw logs, use an asynchronous background task to analyze conversations and extract key entities, preferences, and facts into the structured SQL database.
- Recency-Weighted Aging: In the vector store, add a timestamp metadata field. When retrieving, use a scoring function that combines semantic similarity with a time-decay factor, prioritizing recent information over outdated context.

By applying these strategies—separating short and long-term memory, using hybrid search for precision, and extracting facts rather than storing raw text—the assistant remains fast, accurate, and secure.

---

## Inference Observability, Metrics, and Fallbacks

Deploying language models (LLMs) at scale requires moving beyond traditional APM (Application Performance Monitoring) to comprehensive AI observability, covering performance, quality, and semantic accuracy. The core observability signals must be collected across infrastructure and application levels, supplemented by robust fallback strategies like LLM-to-LLM routing, caching, and graceful degradation to handle provider outages, high latency, or degraded model performance without impacting the end user.

**I. Essential Observability Signals for LLM Inference**
To maintain high availability and performance at scale, monitor the following metrics:

- **Performance Metrics (Infrastructure & Speed):**
  - Time-to-First-Token (TTFT): Critical for user experience in streaming applications; p50/p95 latency.
  - Tokens Per Second (TPS): Measures throughput during the decoding phase.
  - GPU Utilization & Memory Headroom: Tracks VRAM usage to avoid OOM (Out of Memory) errors.
  - Request Rate (RPS) & Queue Length: Identifies congestion and scaling needs.
  - Cache Hit Rate: Measures effectiveness of KV-cache or semantic caching.

- **Operational & Cost Metrics:**
  - Token Consumption: Total prompt/completion tokens per user, session, and model (key for cost management).
  - Error Rates by Type: Distinguish between HTTP 429 (rate limits), 500/503 (server errors), and 400 (bad input).
  - Fallback Trigger Rate: Frequency of switching to backup models.

- **Quality & Semantic Metrics (AI-Native):**
  - Hallucination/Correctness Score: Automated evaluation using "LLM-as-a-judge" to check factuality against context (RAG).
  - Relevance Score: Measures if the output matches the intent.
  - Toxicity/Guardrail Violations: Frequency of flagged content.
  - User Feedback: Explicit signals (e.g., thumbs up/down).

**II. Designing Reliable Fallback Strategies**
Reliable systems assume failure. When primary models are slow or down, implement layered, automated, and non-intrusive fallback strategies.

**1. Multi-Provider Routing (High Availability):**

- Maintain a prioritized, ordered list of providers (e.g., GPT-4 → Claude 3.5 Sonnet → Open-source Mistral on-prem).
- Implement an AI Gateway (e.g., Portkey, Helicone) to automatically route traffic to a secondary provider if the first is down or heavily rate-limited.

**2. Model Tier Cascading (Quality/Cost Trade-off):**

- If the primary high-cost model (e.g., GPT-4o) fails or hits a capacity limit, route queries to a faster, cheaper, but slightly less capable model (e.g., GPT-4o-mini) to maintain service continuity rather than failing completely.

**3. Automatic Retry with Exponential Backoff:**

- For transient issues (e.g., rate limits, network blips), automatically retry the request with increasing delays. Avoid retrying 400-level errors.

**4. Semantic Caching & Graceful Degradation:**

- Semantic Cache: Cache popular prompts and responses. If the model is down, serve cached answers.
- Degraded Responses: If all LLM providers fail, serve a pre-written template or "Service temporarily unavailable" message, rather than a broken page.

**5. Circuit Breakers:**

- Monitor error rates and latency. If they exceed a threshold, "trip" the circuit to temporarily stop sending traffic to that provider to prevent cascading failures.

**6. Human-in-the-Loop (HITL) Routing:**

- Route complex or low-confidence queries (e.g., flagged by an evaluation guardrail) to a human agent, especially in high-stakes scenarios.

---

## MCP (Model Context Protocol) vs function calling

MCP (Model Context Protocol) and function calling both enable LLMs to interact with external tools, but differ in approach: Function calling is LLM-driven, vendor-specific, and best for quick, bespoke tasks. MCP is an open-standardized protocol (by Anthropic) that provides a consistent, reusable, and secure framework for connecting AI to data sources, reducing the need for custom integrations.

**Key Comparisons:**

- Approach: Function calling is direct; the LLM decides which function to use from a provided list. MCP acts as an intermediate layer, where an MCP server provides tools, and a client helps the LLM discover and use them.
- Flexibility: Function calling is often tightly coupled with specific LLM providers (e.g., OpenAI). MCP is designed to be model-agnostic, allowing tools to be shared across different AI applications.
- Scalability: MCP is better for complex, enterprise-level environments needing standardization.
- Implementation: Function calling requires manual setup of each tool and API. MCP simplifies this by enabling developers to build, test, and share tools in a standard format.

**When to Use Which:**

- Function Calling: Ideal for simple, fast implementations with one or two tools, particularly within a single provider's ecosystem.
- MCP: Recommended for complex systems, multi-tool environments, and when you need a secure, reusable, and standard way to connect LLMs to data.

---

## Human-in-the-Loop (HITL) Agentic AI

Human-in-the-Loop (HITL) Agentic AI integrates human judgment into autonomous AI workflows to ensure accuracy, safety, and accountability, particularly for high-risk decisions. Rather than full autonomy, these systems use AI for speed and data processing, pausing for human intervention at critical checkpoints to validate, guide, or approve actions.

**Core Principles of HITL Agentic AI**

- Adjustable Autonomy: HITL allows for defining specific points where the agent must halt and wait for human input, acting as a "brake" on potentially harmful or inaccurate actions.
- Strategic Intervention: Humans are not just reviewers but first-class citizens in the agentic lifecycle, providing context and rectifying ambiguities.
- High-Risk Safeguard: Essential for applications in finance, legal, or IT where AI actions (e.g., executing transactions) have real-world, financial, or ethical consequences.

**Implementation Approaches**

- LangGraph/Graph-Based Interrupts: Systems like LangGraph use interrupt_before or interrupt_after parameters to pause execution, allowing human review of the current state and data before proceeding.
- Asynchronous Human-in-the-Loop: Agents can be designed to pause, send a notification via tools like GotoHuman, and resume once a user interacts with a custom UI or API to approve or amend the decision.
- Middleware Oversight: Specialized middleware can monitor tool calls by the agent and require, for instance, an explicit approval for any email sent, file deleted, or API request made.

**Benefits of a Human-in-the-Loop System**

- Safety and Accuracy: Reduces the risks associated with AI hallucination or unexpected behavior in edge cases.
- Improved Model Training: Human feedback at critical junctures serves as high-quality data to refine and improve future agent performance.
- Regulatory Compliance: Addresses requirements for oversight, such as those found in the EU AI Act and NIST’s AI Risk Management Framework.

---

_Resources:_

1. [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629)

2. [LangChain: Chains & Routing Concepts](https://python.langchain.com/docs/concepts/agents/)

3. [Toolformer: Language Models Can Teach Themselves to Use Tools](https://arxiv.org/abs/2302.04761)

4. [OpenAI Function Calling Guide](https://platform.openai.com/docs/guides/function-calling)

5. [Tree of Thoughts: Deliberate Problem Solving with LLMs](https://arxiv.org/abs/2305.10601)

6. [Chain-of-Thought Prompting](https://arxiv.org/abs/2201.11903)

7. [CAMEL: Communicative Agents for “Mind” Exploration](https://arxiv.org/abs/2303.17760)

8. [AutoGen: Multi-Agent Conversation Framework (Microsoft)](https://github.com/microsoft/autogen)

9. [MemGPT: Towards LLMs with Long-Term Memory](https://arxiv.org/abs/2310.08560)

10. [LangChain Memory Systems Overview](https://python.langchain.com/docs/concepts/memory/)

11. [Lost in the Middle: How Language Models Use Long Contexts](https://arxiv.org/abs/2307.03172)

12. [Long Context Modeling Survey](https://arxiv.org/abs/2402.08268)

13. [Constitutional AI: Harmlessness from AI Feedback](https://arxiv.org/abs/2212.08073)

14. [Guardrails AI Framework](https://www.guardrailsai.com/)

15. [OpenAI Safety Best Practices](https://platform.openai.com/docs/guides/safety-best-practices)

16. [Building LLM Applications in Production (OpenAI Cookbook)](https://cookbook.openai.com/)

17. [Designing LLM Systems for Reliability (Chip Huyen blog)](https://huyenchip.com/2023/04/11/llm-applications.html)

18. [Observability for LLM Applications (LangSmith)](https://docs.smith.langchain.com/)

19. [LLM Evaluation & Monitoring (Arize AI Blog)](https://arize.com/blog/)
