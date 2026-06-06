# Building with the Claude API 🤖

A hands-on course covering the core concepts and practical skills needed to build production-ready applications with Anthropic's Claude API.

---

## 📋 Course Overview

This course walks through the Claude API from first principles — starting with basic message calls and building up to agentic tool-use pipelines. By the end, you'll be able to design, build, and deploy Claude-powered applications confidently.

---

## 🗂️ Repository Structure

```
.
├── notebooks/          # Jupyter notebooks for each module
├── src/                # Reusable helper modules (chat, tools, utils)
├── .env.example        # Template for required environment variables
├── .gitignore
└── README.md
```

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/<your-username>/prompt_engineering.git
cd prompt_engineering
```

### 2. Create and activate a virtual environment
```bash
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Set up environment variables
```bash
cp .env.example .env
```
Open `.env` and add your Anthropic API key:
```
ANTHROPIC_API_KEY=your-api-key-here
```
> ⚠️ **Never commit your `.env` file.** It is listed in `.gitignore`. Get your API key at [console.anthropic.com](https://console.anthropic.com).

---

## 📚 Modules

| # | Topic | Key Concepts |
|---|-------|--------------|
| 1 | **Intro to the Messages API** | `client.messages.create`, roles, content blocks |
| 2 | **Prompt Engineering** | System prompts, temperature, stop sequences |
| 3 | **Structured Outputs** | JSON mode, schema design, output parsing |
| 4 | **Tool Use** | Defining tools, the agentic loop, `tool_use` / `tool_result` blocks |
| 5 | **Multi-turn Conversations** | Message history, helper utilities, stateful chat |
| 6 | **Streaming** | `stream=True`, real-time token handling |
| 7 | **Production Patterns** | Error handling, retries, token counting, cost management |

---

## 🛠️ Key Concepts

### Sending a message
```python
import anthropic

client = anthropic.Anthropic()

response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "Hello, Claude!"}
    ]
)
print(response.content[0].text)
```

### Tool use (agentic loop)
```python
response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1024,
    tools=[my_tool_schema],
    messages=messages
)

if response.stop_reason == "tool_use":
    # Execute the tool and append the result to messages
    ...
```

---

## ⚙️ Environment Variables

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_API_KEY` | Your Anthropic API key (required) |

---

## 📦 Dependencies

- `anthropic` — Official Anthropic Python SDK
- `python-dotenv` — Loads `.env` variables
- `jupyter` — Notebook environment

---

## 🔒 Security Notes

- Store secrets in `.env` only — never hardcode API keys
- `.env` is git-ignored; use `.env.example` to share the required variable names
- Rotate any key that has been accidentally committed to version control immediately at [console.anthropic.com](https://console.anthropic.com)

---

## 📖 Resources

- [Anthropic Documentation](https://docs.anthropic.com)
- [Claude API Reference](https://docs.anthropic.com/en/api)
- [Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)
- [Anthropic Cookbook](https://github.com/anthropics/anthropic-cookbook)

---

## 📝 License

This project is for educational purposes as part of the *Building with the Claude API* course.
