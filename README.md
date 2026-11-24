# HireMe AI – AI-Powered Resume Assistant 🤖

An intelligent AI-powered resume assistant that understands your professional profile, extracts structured information from PDF resumes, and answers career-related questions using Large Language Models (LLMs).

HireMe AI combines **React.js, FastAPI, Python, and Groq LLMs** to transform traditional resumes into interactive, conversational career profiles.

---

## 📌 Project Overview

Traditional resumes contain valuable information about a candidate's education, technical skills, projects, certifications, and professional experience. However, extracting specific information from lengthy resumes manually can be time-consuming.

**HireMe AI** addresses this problem by allowing users to upload or prepare a resume in PDF format, extract its content, convert it into structured JSON, and interact with it through an AI-powered chatbot.

Users can ask questions such as:

- What are my strongest technical skills?
- Explain my projects and their technologies.
- What programming languages do I know?
- Summarize my educational background.
- What experience do I have in Machine Learning?
- What improvements can I make to my professional profile?

The chatbot uses the candidate's parsed resume as context and generates relevant responses.

---

## ✨ Key Features

### 1. PDF Resume Extraction
- Extracts text from PDF resumes using PyPDF.
- Processes resume content for further analysis.
- Supports text-based PDF documents.

### 2. AI-Powered Resume Parsing
- Converts unstructured resume content into structured JSON.
- Organizes candidate information into meaningful sections.
- Extracts relevant professional information.

### 3. Interactive AI Chatbot
- Allows users to ask questions about their resumes.
- Generates contextual answers using Groq-powered LLMs.
- Provides conversational access to candidate information.

### 4. Context-Aware Responses
- Uses parsed resume information as the chatbot's context.
- Avoids inventing qualifications, experience, or skills.
- Responds based on available resume information.

### 5. Modern User Interface
- Built using React.js and Vite.
- Interactive chatbot interface.
- Resume preparation status indicator.
- Chat messaging interface.
- Responsive CSS-based design.

---

## 🛠️ Tech Stack

| Category | Technologies |
|---|---|
| Frontend | React.js |
| Build Tool | Vite |
| Styling | CSS3 |
| Programming Language (Frontend) | JavaScript (ES6+) |
| Backend | Python |
| Backend Framework | FastAPI |
| Programming Language (Backend) | Python |
| AI / LLM Integration | Groq API |
| PDF Processing | PyPDF |
| Data Format | JSON |
| Data Validation | Pydantic |
| Environment Management | Python dotenv |
| Icons | Lucide React |
| API Communication | REST API, HTTP, Fetch API |
| Version Control | Git & GitHub |

### Programming Languages

- **Python:** Backend development, PDF extraction, resume parsing, and AI integration.
- **JavaScript:** Frontend development, React components, state management, and API communication.
- **HTML5:** Frontend application structure.
- **CSS3:** Styling and responsive user interface design.
- **JSON:** Structured resume data exchange between application components.

---

## 🏗️ System Architecture

HireMe AI follows a client-server architecture.

```text
                 USER
                   |
                   v
            REACT FRONTEND
              (Vite + JS)
                   |
                   v
              REST API
                   |
                   v
             FASTAPI SERVER
                   |
          +--------+---------+
          |                  |
          v                  v
      PDF EXTRACTOR      CHAT ENDPOINT
          |                  |
          v                  v
      RESUME TEXT       PARSED RESUME
          |                  |
          v                  v
      RESUME PARSER      GROQ LLM
          |                  |
          v                  |
    STRUCTURED JSON          |
          |                  |
          +------------------+
                   |
                   v
             AI RESPONSE
                   |
                   v
             REACT FRONTEND
                   |
                   v
                  USER
```

### Workflow

1. The user interacts with the React frontend.
2. The frontend sends an HTTP request to the FastAPI backend.
3. The PDF extractor extracts text from the candidate's resume.
4. The resume parser processes the extracted content using an LLM.
5. Structured candidate information is generated in JSON format.
6. The chatbot retrieves the parsed resume information.
7. The Groq LLM generates contextual responses to user questions.
8. The response is displayed in the React chat interface.

---

## 📂 Project Structure

```text
HireMe-AI/
│
├── backend/
│   ├── main.py
│   ├── resume_parser.py
│   ├── AIML_Resume_Oct.pdf
│   ├── parsed_resume.json
│   └── .env
│
├── frontend/
│   ├── src/
│   │   ├── App.jsx
│   │   ├── App.css
│   │   └── main.jsx
│   │
│   ├── public/
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
│
├── .venv/
│
├── .gitignore
└── README.md
```

**Note:** The project structure may evolve as additional features are introduced. The `.venv` directory and sensitive environment files should not be committed to GitHub.

---

## ⚙️ Installation and Setup

Follow these steps to run HireMe AI locally.

### Prerequisites

Make sure you have installed:

- Python
- Node.js and npm
- Git
- VS Code (recommended)
- A Groq API key

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/HireMe-AI.git
```

Navigate into the project:

```bash
cd HireMe-AI
```

### 2. Backend Setup

Navigate to the backend directory:

```bash
cd backend
```

Activate your Python virtual environment.

For Windows PowerShell, if your `.venv` is in the project root:

```powershell
..\.venv\Scripts\Activate.ps1
```

Install the required dependencies:

```bash
pip install fastapi uvicorn groq pypdf python-dotenv pydantic
```

Create a `.env` file inside the backend directory:

```env
GROQ_API_KEY=your_groq_api_key
```

**Important:** Never upload your actual API key to GitHub.

### 3. Add Your Resume

Place your PDF resume inside the backend directory.

Update the resume filename in `main.py` if necessary:

```python
RESUME_PATH = "AIML_Resume_Oct.pdf"
```

### 4. Start the Backend Server

From the backend directory, run:

```bash
uv run uvicorn main:app --reload
```

The backend will run at:

```text
http://127.0.0.1:8000
```

FastAPI interactive API documentation:

```text
http://127.0.0.1:8000/docs
```

### 5. Frontend Setup

Open another terminal and navigate to the frontend directory:

```bash
cd frontend
```

Install frontend dependencies:

```bash
npm install
```

Install Lucide React:

```bash
npm install lucide-react
```

Start the development server:

```bash
npm run dev
```

The frontend will typically run at:

```text
http://localhost:5175
```

If Vite displays a different port, use the URL shown in your terminal.

### 6. Configure CORS

Ensure the FastAPI backend allows requests from your frontend origin.

Example:

```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=[
        "http://localhost:5175",
        "http://127.0.0.1:5175"
    ],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"]
)
```

---

## 🔌 API Endpoints

HireMe AI uses REST APIs to connect the React frontend with the FastAPI backend.

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Checks backend availability |
| GET | `/parse-resume` | Extracts and parses the resume |
| POST | `/chat` | Processes user questions using resume context |

### 1. Backend Health Check

```http
GET /
```

Checks whether the backend server is running.

### 2. Resume Parsing

```http
GET /parse-resume
```

Extracts resume information and returns structured data.

### 3. AI Chat

```http
POST /chat
```

Request body:

```json
{
    "question": "What are my technical skills?"
}
```

Example response:

```json
{
    "question": "What are my technical skills?",
    "answer": "Your technical skills include Python, JavaScript and Machine Learning..."
}
```

*The response above is illustrative; actual answers depend on the candidate's resume.*

---

## 🧠 AI Integration

HireMe AI uses the Groq API to integrate Large Language Models into the resume parsing and conversational workflow.

The LLM is used to:

- Understand extracted resume text.
- Organize information into structured JSON.
- Interpret natural-language questions.
- Generate contextual responses using candidate information.

The chatbot is designed with instructions to use the supplied resume as its source of information and avoid making unsupported claims.

---

## 🔒 Security Considerations

- Store API keys in environment variables.
- Never commit `.env` files.
- Do not upload personal resumes or sensitive candidate information publicly without permission.
- Add authentication and authorization before deploying the application for multiple users.
- Validate uploaded PDF files before processing.

---

## 🚀 Future Enhancements

The following features are potential improvements for future versions:

- [ ] Multiple resume uploads and user profiles.
- [ ] Resume scoring and ATS compatibility analysis.
- [ ] Job description and resume matching.
- [ ] AI-powered skill gap analysis.
- [ ] Resume improvement recommendations.
- [ ] Interview question generation based on candidate profiles.
- [ ] Persistent chat history.
- [ ] User authentication and authorization.
- [ ] Database integration for storing candidate profiles.
- [ ] Resume export and report generation.
- [ ] Cloud deployment.

---

## 🎯 Project Objective

The primary objective of HireMe AI is to make professional resume information more accessible through conversational AI.

By combining document processing, structured data extraction, REST APIs, and Large Language Models, the project demonstrates how AI can simplify resume analysis and improve the way candidates interact with their professional information.

---

## 👨‍💻 Author

**Ayan Ahmad**

B.Tech – Computer Science Engineering  
Specialization: Data Science

GitHub: [Add your GitHub profile URL](https://github.com/)

LinkedIn: [Add your LinkedIn profile URL](https://linkedin.com/)

---

## ⭐ Support

If you find this project interesting, consider giving the repository a star ⭐ on GitHub!

Contributions, suggestions, and feedback are welcome.

**Built with Python, React.js, FastAPI, and Generative AI.**
