# Chatbot with Reasoning 🤖

A Streamlit-based chatbot application powered by **Ollama** and **DeepSeek-R1** model, designed to showcase AI reasoning processes with a beautiful, interactive UI.

## Features

- 💡 **Visible Reasoning Process**: Watch the model think through problems step-by-step with `<think>` tags
- 📊 **Streaming Responses**: Real-time response generation with live UI updates
- 🎨 **Interactive UI**: Clean, centered Streamlit interface with chat history
- 🔍 **Collapsible Thinking**: Hide/show reasoning with an expander widget
- 🚀 **Fast & Lightweight**: Uses DeepSeek-R1 1.5B model for efficient reasoning

## Prerequisites

Before you begin, ensure you have the following installed:

1. **Python 3.12+** - Download from [python.org](https://www.python.org/)
2. **Ollama** - Download from [ollama.com](https://ollama.com/download)
3. **DeepSeek-R1 Model** - Pull the model with:
   ```bash
   ollama pull deepseek-r1:1.5b
   ```

## Installation

1. **Clone or navigate to the project directory:**
   ```bash
   cd chatbot-with-reasoning
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python -m venv .venv
   .venv\Scripts\activate  # On Windows
   # or
   source .venv/bin/activate  # On macOS/Linux
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
   Or using pyproject.toml:
   ```bash
   pip install -e .
   ```

## Usage

1. **Ensure Ollama is running:**
   ```bash
   ollama serve
   ```
   Ollama will start on `http://localhost:11434`

2. **Run the Streamlit app:**
   ```bash
   streamlit run main.py
   ```

3. **Open your browser** to `http://localhost:8501` (Streamlit will open automatically)

4. **Start chatting!** Type your questions and watch the model think through them.

## Project Structure

```
chatbot-with-reasoning/
├── main.py              # Main Streamlit application
├── README.md            # This file
├── pyproject.toml       # Project metadata and dependencies
├── .venv/               # Virtual environment
└── assets/
    └── copilot.jpg      # Copilot logo for header
```

## How It Works

### Chat Flow

1. **User Input** → Message sent to DeepSeek-R1 with system prompt
2. **Thinking Phase** → Model generates `<think>...</think>` content (displayed live in status box)
3. **Response Phase** → Model provides final answer (displayed in chat)
4. **Message Storage** → Both thinking and response saved to chat history

### System Prompt

The chatbot is instructed to follow a strict format:
```
<think>
Step-by-step reasoning here
</think>
Final answer here
```

This ensures consistent, traceable reasoning that can be extracted and displayed separately.

### Key Components

- **`format_reasoning_response()`** - Strips `<think>` tags for clean display
- **`display_assistant_message()`** - Shows reasoning in collapsible expander
- **`process_thinking_phase()`** - Handles streaming thinking content
- **`process_response_phase()`** - Handles streaming response content
- **`handle_user_input()`** - Manages chat input and response generation

## Dependencies

- **streamlit** >= 1.55.0 - Web app framework
- **ollama** >= 0.6.1 - Ollama Python client

See `pyproject.toml` for exact versions.

## API Endpoints

The app connects to Ollama's local API:
- **Default Host**: `http://localhost:11434`
- **Model**: `deepseek-r1:1.5b`
- **Stream**: Enabled for real-time responses

## Customization

### Change the Model

Edit this line in `main.py`:
```python
model="deepseek-r1:1.5b",  # Change to another Ollama model
```

Other reasoning-capable models:
- `deepseek-r1:8b` - Larger version (requires more VRAM)
- `deepseek-r1:7b-distill` - Distilled version

### Modify System Prompt

Edit the system message in the `if __name__ == "__main__":` block:
```python
{"role": "system", "content": "Your custom system prompt here"}
```

### Update the Header

Replace `assets/copilot.jpg` with your own image, or modify the header markdown in `main()`.

## Troubleshooting

| Issue | Solution |
|-------|----------|
| **"Connection refused" error** | Make sure Ollama is running: `ollama serve` |
| **Model not found** | Pull the model: `ollama pull deepseek-r1:1.5b` |
| **FileNotFoundError: assets/copilot.jpg** | Create `assets/` folder and add a `copilot.jpg` image |
| **Slow responses** | Use smaller model or check system resources |
| **Thinking not showing** | Ensure system prompt is properly formatted in chat history |

## Performance Tips

- **GPU Acceleration**: Enable in Ollama for faster inference (`ollama GPU`)
- **Model Size**: 1.5B model is lightweight; upgrade to 8B for better reasoning if you have resources
- **Stream Optimization**: Streaming is already enabled; adjust `st.session_state` retention if needed

## Future Enhancements

- 📝 Save conversations to file
- 🌙 Dark/Light mode toggle
- ⚙️ Model selection dropdown
- 💾 Conversation history export (JSON/CSV)
- 🔧 Custom system prompt editor in UI

## License

This project is open source and available under the MIT License.

## Resources

- [Ollama Documentation](https://github.com/ollama/ollama)
- [Streamlit Documentation](https://docs.streamlit.io/)
- [DeepSeek-R1 Model](https://ollama.com/library/deepseek-r1)

---

**Happy reasoning! 🚀**
