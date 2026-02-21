# Assignment: Smart Customer Support Router
**Implementation of a Mixture of Experts (MoE) Architecture with Tool Use**



## 🎯 Project Overview
This notebook demonstrates a production-grade **Mixture of Experts (MoE)** routing system built with the Groq API and `llama-3.3-70b-versatile`. Instead of relying on a single, generalized prompt with a massive context window, this architecture intelligently classifies user intent and routes the query to highly specialized, domain-specific "experts."

## 🧠 Architecture Components

1. **The Router (Classifier):** - A low-temperature (`T=0`) LLM call designed strictly for deterministic classification. 
   - It evaluates the user's input and returns a single category token: `technical`, `billing`, `general`, or `data`.

2. **The Orchestrator (Control Flow):** - The Python logic that receives the Router's classification and dynamically shifts the model's persona by injecting the appropriate System Prompt.

3. **The Prompt Experts (Generation):** - Specialized LLM configurations with a higher temperature (`T=0.7`) to allow for creative, empathetic, or rigorously technical responses based on the routed domain.

4. **Tool Use / Function Calling (Bonus Challenge):**
   - If the Router detects a request for real-time metrics (e.g., Bitcoin prices), it outputs the `data` token.
   - The Orchestrator intercepts this route and completely bypasses the LLM generation phase, executing a standard Python function instead. This prevents hallucinations and saves compute/tokens.

## 💡 Why This Matters
By decoupling intent classification from response generation, this MoE pattern drastically reduces token usage, minimizes prompt bloat, and ensures that the AI responds with the highest possible accuracy and appropriate tone for the specific task at hand.
