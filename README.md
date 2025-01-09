
# Ollama Prompt Tool

This repository provides a simple command-line interface (CLI) tool for interacting with language models using the `ollama` Python library. Users can input prompts, receive model-generated responses, and maintain a history of interactions for context in subsequent queries.

## Features
- User-friendly CLI interface
- Continuous interaction with a language model
- Context preservation for better response relevance
- Handles errors gracefully

---

## Prerequisites

### 1. Install Python
Ensure you have Python 3.8 or higher installed. You can download it from the [official Python website](https://www.python.org/downloads/).

### 2. Install Required Libraries
Use `pip` to install the required dependencies:

```bash
pip install ollama
```

### 3. Compatible Models
This tool works with models available through `ollama`, such as `vicuna:7b`. Ensure you have the desired model downloaded and ready for use.

---

## Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/ollama-prompt-tool.git
cd ollama-prompt-tool
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

---

## Usage

Run the script from your terminal:

```bash
python main.py
```

### Interacting with the Model
1. Enter a prompt when prompted.
2. Press Enter to submit the prompt.
3. The model's response will be displayed.
4. To exit, press Enter without typing a prompt.

---

## Code Explanation

```python
import ollama

# Initialize a list to store responses
response_history = []

while True:
    # Get user input for the prompt (display in green)
    prompt = input("\033[92m\nEnter your prompt (or press Enter to exit): \033[0m")
    if prompt == '':
        break
    
    # Combine previous responses as context
    context = "\n".join(response_history)
    full_prompt = context + "\n" + prompt if context else prompt
    
    try:
        # Generate a response using the model
        response = ollama.generate(model='vicuna:7b', prompt=full_prompt)
        
        # Store the response in the history
        response_history.append(response.response)
        
        # Print the latest response in cyan
        print("\033[96m\n" + response.response + "\033[0m")
    except Exception as e:
        # Print the error in red
        print("\033[91m\nAn error occurred:\033[0m", "\033[91m" + str(e) + "\033[0m")
```

- **`response_history`**: Stores previous responses to maintain context.
- **`ollama.generate`**: Generates a response using the specified model.
- **Error Handling**: Captures and displays errors in red text.

---

## Contributing

Contributions are welcome! Feel free to submit issues or pull requests to improve the tool.

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.
