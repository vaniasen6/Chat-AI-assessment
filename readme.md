# AI Customer Support Agent

This document provides a comprehensive overview of a sophisticated customer support chatbot for Thoughtful AI. The implementation uses advanced natural language processing techniques to provide accurate responses to customer inquiries about Thoughtful AI's products and services.

## Project Overview

The Thoughtful AI Support Agent is a specialized chatbot designed to answer customer questions about Thoughtful AI's suite of healthcare automation solutions. The system leverages semantic similarity search and few-shot learning to match user queries with predefined answers, ensuring accurate and consistent responses to common customer inquiries.

## Technology Stack

The project utilizes several key technologies:
- **Cohere**: Powers the language model and embedding functionality
- **LangChain**: Provides the framework for creating the conversational AI
- **FAISS**: Enables efficient similarity search for vector embeddings
- **Gradio**: Creates an intuitive web interface for the chatbot
- **Python**: Serves as the primary programming language

## Key Features

### Semantic Matching System

The chatbot uses semantic similarity matching rather than simple keyword matching, allowing it to understand the intent behind user questions even when phrased differently from the training examples. This is accomplished through:

- Vector embeddings of pre-defined questions using Cohere's embedding model
- FAISS vector store for efficient similarity search
- Configurable matching threshold to control precision

### Few-Shot Learning Approach

The implementation employs few-shot learning techniques:
- Pre-defined Q&A pairs serve as examples for the model
- The system dynamically selects the most relevant examples based on the user's query
- A carefully crafted prompt template guides the language model to provide consistent answers[1]

### Fallback Mechanism

When a user query doesn't match any pre-defined examples closely enough:
- The system follows strict rules to provide a default response
- This prevents hallucination or incorrect information being shared
- The default message guides users to ask questions within the supported domain[1]

### User Interface

The chatbot is deployed with a clean, user-friendly interface:
- Built using Gradio for rapid deployment and easy interaction
- Includes example questions to guide users
- Provides clear responses with appropriate formatting[1]

## Implementation Details

### Configuration Parameters

The system includes several tunable parameters:
- `MODEL_TEMPERATURE`: Controls randomness in responses (set to 0.1 for consistency)
- `TOP_N_MATCH`: Determines how many similar examples to retrieve (default: 2)
- API key management through environment variables
- Default answer text for out-of-scope questions[1]

### Vector Similarity Search

The semantic matching engine is built on:
- `SemanticSimilarityExampleSelector` from LangChain
- FAISS vector store for efficient similarity search
- Cohere embeddings (using the "embed-english-v3.0" model)
- Top-N retrieval of the most similar questions[1]

### Chatbot Agent Architecture

The core function `chatbot_ai_agent` implements several sophisticated features:

1. **Semantic Retrieval**: Dynamically finds the most relevant examples from the predefined dataset
2. **Few-Shot Prompt Construction**: Builds context-aware prompts based on matching examples
3. **LLM Fallback**: Provides appropriate responses even for out-of-domain queries
4. **Robust Error Handling**: Gracefully manages exceptions and edge cases
5. **Maintainability**: Modular design allows for easy updates to the Q&A dataset
6. **Session History Support**: Architecture ready for multi-turn conversations[1]

## Usage Instructions

### Setup

1. Install required packages:
```bash
pip install -qU gradio langchain-cohere faiss-cpu python-dotenv langchain-community
```

2. Set up your Cohere API key:
```python
import os
os.environ["COHERE_API_KEY"] = "your_api_key_here"
```

3. Run the application:
```python
demo.launch()
```

### Example Usage

The chatbot comes pre-loaded with examples about Thoughtful AI's products:
- Questions about the eligibility verification agent (EVA)
- Information about the claims processing agent (CAM)
- Details about the payment posting agent (PHIL)
- General information about Thoughtful AI's agents and their benefits[1]
