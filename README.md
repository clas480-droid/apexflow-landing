# YouTube Video Summarizer

A Python script that takes any YouTube video link, extracts its transcript with timestamps using `youtube-transcript-api`, and uses an AI prompt to summarize key points, core concepts, and key moments.

---

## 🚀 Features

- **Flexible URL Support**: Works with standard YouTube URLs (`watch?v=...`), short URLs (`youtu.be/...`), embed links, shorts (`/shorts/...`), live links, or raw video IDs.
- **Intelligent Timestamping**: Formats transcript subtitles into readable ~30-second blocks with `[MM:SS]` or `[HH:MM:SS]` markers so the AI can accurately reference specific moments.
- **Multi-Language Support**: Automatically detects and fetches transcripts in preferred languages (English, Arabic, Spanish, etc.), falling back to auto-generated subtitles when manual ones aren't available.
- **Multiple AI Providers (Zero Extra SDKs Required)**:
  - **Google Gemini** (Default: `gemini-2.5-flash`, `gemini-2.0-flash`, `gemini-1.5-flash`)
  - **OpenAI** (`gpt-4o-mini`, `gpt-4o`, etc.)
  - **Anthropic Claude** (`claude-3-5-sonnet`, etc.)
  - **Ollama** (Local LLM, e.g. `llama3.2`)
- **Offline / Prompt-Only Mode**: Run `--prompt-only` to generate the complete formatted prompt and copy it directly into web chatbots (ChatGPT, Claude, Gemini) without needing an API key!
- **Export to Markdown**: Save summaries directly to disk with `-o summary.md`.

---

## 📦 Installation

1. Install the required dependency:
```bash
pip install -r requirements.txt
```
*(Or `pip install youtube-transcript-api`)*

2. Set your preferred AI API key:

### Google Gemini (Recommended)
```bash
export GEMINI_API_KEY="your-gemini-api-key"
```
*(Get a free Gemini API key from [Google AI Studio](https://aistudio.google.com/))*

### OpenAI
```bash
export OPENAI_API_KEY="your-openai-api-key"
```

### Anthropic
```bash
export ANTHROPIC_API_KEY="your-anthropic-api-key"
```

---

## 📖 Usage Examples

### 1. Basic Summarization (Google Gemini)
```bash
python youtube_summarizer.py "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
```

### 2. Interactive Mode (Prompt for URL)
```bash
python youtube_summarizer.py
```

### 3. Using OpenAI & Saving Output to Markdown
```bash
python youtube_summarizer.py "https://youtu.be/dQw4w9WgXcQ" --provider openai -o summary.md
```

### 4. No API Key? Copy Prompt to Web AI
```bash
python youtube_summarizer.py "https://youtu.be/dQw4w9WgXcQ" --prompt-only
```

### 5. Using Local Ollama
```bash
python youtube_summarizer.py "https://youtu.be/dQw4w9WgXcQ" --provider ollama --model llama3.2
```

### 6. View Raw Timestamped Transcript
```bash
python youtube_summarizer.py "https://youtu.be/dQw4w9WgXcQ" --transcript-only
```

---

## ⚙️ Command-Line Options

| Flag | Description | Default |
|---|---|---|
| `url` | YouTube video URL or ID | Prompted interactively if omitted |
| `--provider`, `-p` | AI Provider (`gemini`, `openai`, `anthropic`, `ollama`) | Auto-detected from environment |
| `--model`, `-m` | Custom model name | Provider default (e.g., `gemini-2.5-flash`) |
| `--api-key`, `-k` | Pass API key directly | Reads from environment variable |
| `--output`, `-o` | Save output to Markdown file | Prints to console |
| `--languages`, `-l` | Comma-separated preferred language codes | `en,ar,es,fr,de` |
| `--chunk-interval` | Chunk interval in seconds for grouping subtitles | `30` |
| `--prompt-only` | Print formatted prompt only (no API call) | Disabled |
| `--transcript-only`| Print formatted transcript only | Disabled |
| `--ollama-host` | Ollama host address | `http://localhost:11434` |

---

## 🧪 Testing

Run the included unit test suite:
```bash
python test_youtube_summarizer.py
```
