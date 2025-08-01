# Recallio Memory for LangChain

This repository provides an implementation of `RecallioMemory`, a drop‑in replacement for `BaseMemory` from [LangChain](https://python.langchain.com/). It stores conversation history in the [Recallio](https://app.recallio.ai) cloud service using the official `recallio` client (version 1.2.4).

## Features

- **Scoped writes** – memories can be associated with a specific `session_id` or `user_id`.
- **TTL support** – pass a time‑to‑live in seconds and it will be converted to an expiration timestamp stored alongside each memory.
- **Vector recall** – previous messages are retrieved from Recallio using semantic search. Memories can also be filtered by custom tags.

## Installation

```bash
pip install recallio==1.2.4 langchain
```

## Usage

```python
from langchain_recallio.memory import RecallioMemory

memory = RecallioMemory(
    api_key="YOUR_RECALLIO_API_KEY",
    project_id="my-project",
    user_id="alice",
    session_id="chat-session-1",
    ttl_seconds=3600,  # expire after one hour
)

# Store an interaction
memory.save_context({"input": "Hello"}, {"output": "Hi there!"})

# Load recent conversation history to inject into a prompt
history = memory.load_memory_variables({"input": "What's up?"})
print(history)
```

## Running the tests

```
pytest
```

The tests use mocks and do not require a valid Recallio API key.

## License

This project is distributed under the MIT license.
