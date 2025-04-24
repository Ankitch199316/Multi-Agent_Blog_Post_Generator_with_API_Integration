# Multi-Agent Blog Post Generator

This repository provides a modular, multi-agent system to automate the end-to-end creation of high-quality blog posts. It leverages OpenRouter for LLM interaction, SerpAPI for web search, and NewsAPI for recent news, coordinating three specialized agents—Planning, Writing, and Editing—through shared memory.

---

## 🚀 Features

- **PlanningAgent**: Researches a topic via web search and news APIs, then generates a detailed, SEO-optimized blog plan (title, outline, keywords, audience, etc.).
- **ContentWriterAgent**: Consumes the plan and research to draft a full blog post in Markdown format.
- **EditorAgent**: Proofreads, refines, and formats the draft for readability, SEO, and consistency with the plan.
- **SharedMemory**: Central message bus for agent coordination, tracking research data, plans, drafts, and inter-agent communication.
- **Orchestrator**: `generate_blog_post(topic, output_path)` function to run the complete workflow in sequence and optionally save the final Markdown file.

---

## 🛠️ Prerequisites

- Python 3.8 or later
- API keys for:
  - **OpenRouter** (LLM access)
  - **SerpAPI** (web search)
  - **NewsAPI** (news articles)

---

## 📦 Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/blog-agent-system.git
   cd blog-agent-system
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

---

## ⚙️ Configuration

Set your API keys as environment variables:

```bash
export OPENROUTER_API_KEY="your_openrouter_key"
export SERPAPI_API_KEY="your_serpapi_key"
export NEWSAPI_API_KEY="your_newsapi_key"
```

Alternatively, you can hardcode them in the script (not recommended for production).

---

## 📑 Usage

### Generate a Blog Post

```python
from blog_agent import generate_blog_post

# Provide your topic and (optional) output directory
final_markdown = generate_blog_post(
    topic="Sales in the era of AI",
    output_path="./output/"
)
print(final_markdown)
```

This will:
1. Conduct research (web & news) via `PlanningAgent`.
2. Create a blog plan and send it to `ContentWriterAgent`.
3. Draft the blog post in Markdown.
4. Edit and refine the draft with `EditorAgent`.
5. Save the final `.md` file under `./output/` (filename derived from the title).

---

## 🧩 Architecture

```text
SharedMemory ---> PlanningAgent --research & plan--> SharedMemory
                ContentWriterAgent --draft--> SharedMemory
                EditorAgent --final edit--> SharedMemory
                Orchestrator (generate_blog_post)
```

1. **SharedMemory**: Holds `topic`, `research_data`, `blog_plan`, `blog_draft`, and `final_blog`.
2. **Agents**: Each agent inherits from `Agent`, implements `execute_task()`, and communicates via shared memory.
3. **LLM Integration**: `Agent.query_llm()` sends prompts to OpenRouter’s chat completion endpoint.
4. **APIs**: SerpAPI for organic search results; NewsAPI for recent articles.

---

## 📋 Code Structure

```text
blog_agent.py         # Main module with SharedMemory, Agent classes, and orchestrator
requirements.txt      # Python dependencies
output/               # (Optional) Directory to save generated posts
README.md             # This documentation
```

---

## 🤝 Contributing

1. Fork the repository.
2. Create a new branch: `git checkout -b feature/YourFeature`.
3. Commit your changes: `git commit -m "Add feature XYZ"`.
4. Push to the branch: `git push origin feature/YourFeature`.
5. Open a Pull Request.

---

## 📄 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## 🙋‍♂️ Acknowledgments

- OpenRouter for LLM API
- SerpAPI for search integration
- NewsAPI for news retrieval
- Inspired by multi-agent collaboration frameworks

