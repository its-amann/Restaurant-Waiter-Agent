# Restaurant Waiter Agent 🤖

<div align="center">
  <img src="./_asserts/ServeBot 3000.jpg" alt="Server Bot Logo" width="400"/>
  <p><em>Restaurant Waiter Agent Logo</em></p>
</div>

<div align="center">
  <img src="./_asserts/graph preview after making question checking node  function.png" alt="Agent Workflow" width="800"/>
  <p><em>Restaurant Waiter Agent Workflow Diagram</em></p>
</div>

<div align="center">
  <img src="./_asserts/output of the agent working.png" alt="Agent in Action" width="800"/>
  <p><em>Agent Interaction Example</em></p>
</div>

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Technical Components](#technical-components)
- [Workflow](#workflow)
- [Installation](#installation)
- [Dependencies](#dependencies)
- [Usage](#usage)
- [State Management](#state-management)
- [Components Breakdown](#components-breakdown)
- [Contributing](#contributing)
- [License](#license)

## Overview

The Restaurant Waiter Agent is an advanced AI-powered system designed to simulate a restaurant waiter capable of interacting with customers, answering questions about the menu, and providing friendly responses. The system utilizes LangChain and LangGraph libraries to construct the agent's workflow and integrates with OpenAI's GPT-based language models for natural language understanding and generation.

## Features

### Core Capabilities
- 🗣️ Natural conversation handling
- 📋 Menu information retrieval
- 💬 Context-aware responses
- 🤝 Professional interaction management
- 🔄 Dynamic conversation flow
- 📊 State tracking and management

### Interaction Features
- Answers menu-related questions
- Provides dish recommendations
- Handles off-topic queries gracefully
- Maintains conversation context
- Offers friendly and professional responses
- Processes customer preferences

## Architecture

The system is built using a sophisticated architecture that combines several key components:

### Core Components
1. **Document Processing**
   - UnstructuredExcelLoader for menu data
   - RecursiveCharacterTextSplitter for text processing

2. **Vector Storage**
   - FAISS vector store for efficient similarity search
   - OpenAI embeddings for document vectorization

3. **Language Models**
   - OpenAI's GPT models for response generation
   - Custom prompt templates for context management

4. **Workflow Management**
   - LangGraph for workflow orchestration
   - State management system for conversation tracking

## Technical Components

### State Management
```python
class AgentState(TypedDict):
    start: bool             # Conversation initiation flag
    conversation: int       # Conversation turn counter
    question: str          # Customer's current question
    answer: str           # Agent's response
    topic: bool           # Question appropriateness flag
    documents: list       # Retrieved relevant documents
    recursion_limit: int  # Loop prevention counter
    memory: list         # Conversation history
```

### Key Functions

1. **Greeting Handler**
```python
def greetings(state):
    # Initializes conversation
    # Captures initial user input
    # Updates conversation state
```

2. **Question Assessment**
```python
def check_question(state):
    # Evaluates question appropriateness
    # Uses GPT model for assessment
    # Updates topic state
```

3. **Document Retrieval**
```python
def retrieve_docs(state):
    # Performs similarity search
    # Retrieves relevant menu items
    # Updates document state
```

## Workflow

The agent follows a structured workflow:

1. **Initialization**
   - System setup and model loading
   - State initialization
   - Resource preparation

2. **Conversation Flow**
   - Greeting and initial interaction
   - Question processing and validation
   - Context-aware response generation
   - Continuous conversation management

3. **Response Generation**
   - Document retrieval
   - Context incorporation
   - Response refinement
   - Professional tone maintenance

### Workflow Diagram Explanation

The workflow diagram (shown above) illustrates:
- Conversation entry points
- Decision nodes for topic assessment
- Document retrieval paths
- Response generation flow
- State management connections

## Installation

1. Clone the repository:
```bash
git clone [repository-url]
cd restaurant-waiter-agent
```

2. Install required packages:
```bash
pip install -q langchain-community langchain-openai unstructured faiss-cpu langgraph
```

3. Set up environment variables:
```bash
export OPENAI_API_KEY='your-api-key'
```

## Dependencies

Core dependencies include:
- langchain-community
- langchain-openai
- unstructured
- faiss-cpu
- langgraph

Additional requirements:
- Python 3.7+
- OpenAI API access
- Sufficient computational resources for vector operations

## Usage

### Basic Implementation

```python
# Initialize the workflow
workflow = StateGraph(AgentState)

# Add workflow nodes
workflow.add_node("greetings", greetings)
workflow.add_node("check_question", check_question)
workflow.add_node("retrieve_docs", retrieve_docs)
workflow.add_node("generate", generate)
workflow.add_node("improve_answer", improve_answer)

# Set entry point
workflow.set_entry_point("greetings")

# Compile the application
app = workflow.compile()
```

### Running the Agent

```python
# Initialize state
initial_state = {
    "start": True,
    "recursion_limit": 50
}

# Run the agent
result = app.invoke(initial_state)
```

## State Management

The agent maintains state through several key components:

### Conversation State
- Tracks conversation turns
- Maintains question history
- Stores generated responses
- Manages topic relevance

### Document State
- Handles retrieved documents
- Manages similarity search results
- Maintains context information

### Memory Management
- Stores conversation history
- Tracks user preferences
- Maintains context continuity

## Components Breakdown

### 1. Document Processing
The system uses UnstructuredExcelLoader to process menu data:
```python
loader = UnstructuredExcelLoader(file, mode="elements")
data = loader.load()
```

### 2. Vector Store
FAISS implementation for efficient similarity search:
```python
embeddings = OpenAIEmbeddings()
db = FAISS.from_documents(data, embeddings)
```

### 3. Response Generation
Multi-step response generation process:
```python
def generate(state):
    # Context preparation
    # Response generation
    # Response refinement
```

### 4. Answer Improvement
Response refinement system:
```python
def improve_answer(state):
    # Answer analysis
    # Professional tone enhancement
    # Context incorporation
```

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

<div align="center">
  <p>Built with ❤️ using LangChain and LangGraph</p>
</div> 