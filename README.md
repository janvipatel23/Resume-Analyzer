# 📑 Resume Analyzer

An AI-powered resume analysis tool that extracts text from uploaded PDF resumes, scores them across multiple dimensions, and delivers detailed feedback — all inside a clean, interactive Streamlit interface.

---

## ✨ Features

- **PDF Upload & Preview** — Upload any PDF resume and instantly preview the extracted text side-by-side with the AI analysis.
- **AI-Powered Analysis** — Leverages **Llama 3.3 70B** (via Groq) to analyze resumes and return structured, expert-level feedback.
- **Detailed Scoring** — Each resume is scored out of **100 points** across four weighted categories.
- **Visual Score Breakdown** — Category scores rendered as an interactive **bar chart** powered by Streamlit + Pandas.
- **Overall Progress Bar** — Visual indicator of total score at a glance.
- **Improvement Suggestions** — Actionable, personalized recommendations to strengthen the resume.
- **Key Skills Extraction** — Automatically identifies and lists core skills found in the resume.

---

## 🖥️ App Layout

```
┌──────────────────────────────────────────────────────────────┐
│                      Resume Analyzer 📑                      │
│     Upload your resume and get a summary, key skills         │
│            score and improvement suggestion                  │
│                                                              │
│         [ Upload PDF Resume ────────────────── ]            │
├─────────────────────────┬────────────────────────────────────┤
│    Resume Preview       │         AI Analysis                │
│                         │                                    │
│  [Extracted PDF Text]   │  ✅ Summary                        │
│                         │  ✅ Key Skills                     │
│                         │  ✅ Improvement Suggestions        │
│                         │                                    │
│                         │  📊 Score Breakdown (Bar Chart)    │
│                         │  🔵 Overall Score (Progress Bar)   │
└─────────────────────────┴────────────────────────────────────┘
```

---

## 📊 Scoring Rubric

| Category | Points |
|---|---|
| Skills Match | 30 |
| Experience & Achievements | 30 |
| Clarity & Formatting | 20 |
| Overall Impression | 20 |
| **Total** | **100** |

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Language** | Python 3.11+ | Core application language |
| **UI Framework** | Streamlit | Interactive web UI — file upload, two-column layout, charts |
| **LLM** | Groq API — `llama-3.3-70b-versatile` | AI analysis: summary, skills, suggestions, scoring |
| **LLM Client** | OpenAI Python SDK | OpenAI-compatible client pointed at Groq's base URL |
| **PDF Parsing** | PyPDF2 (`PdfReader`) | Extract raw text from every page of the uploaded PDF |
| **Data Handling** | Pandas | Build score DataFrames for Streamlit's bar chart |
| **Text Cleanup** | Python `re` (regex) | Normalize inconsistent whitespace and newlines from PDF output |
| **Config** | python-dotenv | Securely load `GROQ_API_KEY` from a `.env` file |

---

## 📁 Project Structure

```
Resume-Analyzer/
├── main.py          # Complete application — PDF parsing, LLM call, Streamlit UI
├── .gitignore       # Git ignore rules
└── README.md        # Project documentation
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.11+
- A free [Groq API key](https://console.groq.com/)

### 1. Clone the Repository

```bash
git clone https://github.com/janvipatel23/Resume-Analyzer.git
cd Resume-Analyzer
```

### 2. Install Dependencies

```bash
pip install streamlit openai PyPDF2 pandas python-dotenv
```

### 3. Configure Environment Variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
```

### 4. Run the App

```bash
streamlit run main.py
```

The app will open in your browser at `http://localhost:8501`.

---

## 🔄 How It Works

```
User uploads PDF
       │
       ▼
PyPDF2 extracts text page-by-page
       │
       ▼
Regex normalizes whitespace and line breaks
       │
       ▼
Two-column layout renders:
  ├── Left: Resume text preview
  └── Right: "Analyze Resume" button
                   │
                   ▼ (on click)
       Prompt is constructed:
         1. Summary
         2. Key Skills
         3. Improvement Suggestions
         4. Score out of 100 (4 categories → JSON)
                   │
                   ▼
       Groq API → llama-3.3-70b-versatile (max 700 tokens)
                   │
                   ▼
       Response is split on "Score JSON:"
         ├── Analysis text   → st.write()
         └── JSON scores     → Pandas DataFrame
                                   ├── Bar chart (st.bar_chart)
                                   └── Progress bar (st.progress)
```

---

## ⚙️ Configuration Reference

| Parameter | Value | Description |
|---|---|---|
| `model` | `llama-3.3-70b-versatile` | Groq LLM model for resume analysis |
| `max_tokens` | `700` | Maximum tokens in the LLM response |
| `base_url` | `https://api.groq.com/openai/v1` | Groq's OpenAI-compatible API endpoint |
| `layout` | `wide` | Streamlit page layout mode |
| `file_type` | `pdf` | Accepted resume upload format |

---

## 📦 Full Dependency List

```
streamlit
openai
PyPDF2
pandas
python-dotenv
```

---

## 🤝 Contributing

Contributions, bug reports, and feature requests are welcome! Feel free to open a pull request or issue on [GitHub](https://github.com/janvipatel23/Resume-Analyzer).

---

## 📄 License

This project is open source. See the repository for license details.