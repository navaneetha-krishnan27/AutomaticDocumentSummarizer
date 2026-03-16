# 📄 AI Document Summarizer & Assistant

An intelligent, locally-run web application designed to tackle information overload. Built with Python and Flask, this platform leverages advanced Natural Language Processing (NLP) to automatically summarize lengthy documents, extract key insights, and allow users to intuitively "chat" with their files using deep learning-based semantic search.

Beyond AI, it features a complete suite of PDF manipulation tools, making it a centralized, privacy-focused workspace for document processing.

✨ Key Features
Intelligent Summarization: Generates cohesive paragraphs (LSA) or concise bullet points (LexRank) from PDFs, Word docs, PowerPoints, and plain text.

Chat with Document: Ask questions about your uploaded file in natural language. Powered by sentence-transformers (MiniLM) for high-accuracy semantic search, with a robust TF-IDF statistical fallback.

Multilingual Translation: Instantly translate your extracted summaries into multiple languages.

PDF Utility Suite: Built-in tools to seamlessly Split, Merge, and convert Images (JPG/PNG) to PDF.

Admin Dashboard: A comprehensive backend interface with Chart.js analytics for tracking user activity, document processing stats, and system health.

Privacy-First (Local ML): Machine learning models are downloaded and run locally, ensuring your sensitive document data never leaves your server.

🛠️ Tech Stack
Backend: Python 3, Flask, SQLAlchemy, MySQL

AI & NLP: sumy, sentence-transformers, spacy, scikit-learn

File Processing: PyPDF2, python-docx, python-pptx, Pillow (PIL)

Frontend: HTML5, CSS3 (Glassmorphism UI), Vanilla JavaScript, Chart.js
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Flask](https://img.shields.io/badge/Flask-Web%20Framework-lightgrey)
![MySQL](https://img.shields.io/badge/MySQL-8.0-orange)
![Machine Learning](https://img.shields.io/badge/AI-NLP%20%26%20Semantic%20Search-success)

An intelligent, locally-run web application designed to tackle information overload. Built with Python and Flask, this platform leverages advanced Natural Language Processing (NLP) to automatically summarize lengthy documents, extract key insights, and allow users to intuitively "chat" with their files using deep learning-based semantic search. 

Beyond AI capabilities, it features a complete, standalone suite of PDF manipulation tools (Split, Merge, Image-to-PDF), making it a centralized, privacy-focused workspace for all document processing needs.

---

## 📑 Table of Contents
1. [Key Features](#-key-features)
2. [Algorithms & AI Models](#-algorithms--ai-models)
3. [Technology Stack](#-technology-stack)
4. [System Requirements](#-system-requirements)
5. [Installation & Setup](#-installation--setup)
6. [Project Structure](#-project-structure)
7. [Usage Guide](#-usage-guide)
8. [Future Scope](#-future-scope)
9. [License](#-license)

---

## ✨ Key Features

* **🧠 Intelligent Summarization:** * Generates cohesive paragraphs or concise bullet points from PDFs, Word docs (`.docx`), PowerPoints (`.pptx`), and plain text.
  * Cleans extracted text by stripping page numbers, footers, and code blocks.
* **💬 Chat with Document (Semantic Search):** * Ask questions about your uploaded file in natural language. 
  * Employs deep-learning vector embeddings to find the most contextually relevant answers, with a statistical TF-IDF fallback to ensure high availability.
* **🛠️ Comprehensive PDF Utility Suite:** * **Split PDF:** Extract specific page ranges and download the new document instantly.
  * **Merge PDF:** Combine multiple PDF files into a single, continuous document.
  * **Image to PDF:** Convert images (JPG/PNG) into standardized A4/Letter PDFs, automatically handling RGBA to RGB conversion and aspect ratio resizing.
* **🌍 Multilingual Translation:** Instantly translate your extracted summaries into multiple languages using `deep_translator`.
* **📊 Admin Dashboard:** A secure backend interface with `Chart.js` analytics for tracking user activity, document processing statistics, and database health.
* **🔒 Privacy-First (Local ML):** All machine learning models are downloaded and run locally. Your sensitive document data never leaves your machine.

---

## 🤖 Algorithms & AI Models

This project implements a hybrid approach to text processing, utilizing both traditional statistical NLP and modern deep learning:

1. **Latent Semantic Analysis (LSA):** Used for generating paragraph-style summaries. It extracts hidden relationships between words and sentences to identify core topics without redundancy.
2. **LexRank:** A graph-based algorithm used for generating bullet-point summaries. It calculates the "centrality" of sentences to find the most representative standalone statements.
3. **Sentence Transformers (MiniLM):** The `all-MiniLM-L6-v2` model powers the "Chat" feature. It converts document sentences and user queries into high-dimensional vectors, calculating **Cosine Similarity** to find exact semantic matches.
4. **TF-IDF Vectorization:** Serves as a robust fallback mechanism for the Chat feature. If the deep learning model is unavailable, the system uses TF-IDF term-weighting to find keyword-based answers.

---

## 💻 Technology Stack

* **Backend & Web Framework:** Python 3.x, Flask, Werkzeug
* **Database & ORM:** MySQL Server, Flask-SQLAlchemy, PyMySQL
* **AI & NLP Libraries:** `sumy`, `sentence-transformers`, `spacy`, `scikit-learn`
* **File Processing:** `PyPDF2` (Split/Merge), `Pillow` (Image processing), `python-docx`, `python-pptx`, `fpdf`
* **Frontend UI:** HTML5, CSS3 (Glassmorphism design), Vanilla JavaScript (ES6+)
* **Frontend Libraries:** `Chart.js` (Analytics), `PDF.js` (In-browser rendering)

---

## ⚙️ System Requirements

* **OS:** Windows 10/11, macOS, or Linux (Ubuntu 20.04+)
* **Processor:** Intel Core i5 / AMD Ryzen 5 or higher (Recommended for NLP processing)
* **RAM:** 8 GB Minimum (To load the ML models into memory)
* **Storage:** 5+ GB free space (For Python environments, local ML models, and temporary upload storage)
* **IDE:** Visual Studio Code (VS Code) recommended

---

## 🚀 Installation & Setup

**1. Clone the repository**
```bash
git clone [https://github.com/yourusername/ai-document-summarizer.git](https://github.com/yourusername/ai-document-summarizer.git)
cd ai-document-summarizer
2. Set up a Virtual Environment

Bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
3. Install Dependencies

Bash
pip install -r requirements.txt
4. Download NLP Models
Download the required Named Entity Recognition (NER) model for spaCy:

Bash
python -m spacy download en_core_web_sm
(Note: The sentence-transformers model will automatically download to the local_ml_model/ directory the first time you execute a chat query).

5. Database Configuration

Open your MySQL environment and create the database:

SQL
CREATE DATABASE nlp_fresh_db;
Update the database connection URI in app.py to match your credentials:

Python
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://username:password@localhost/nlp_fresh_db'
6. Initialize the Database
Run the following inside your Python shell or via a setup script to create the tables:

Python
from app import db, app
with app.app_context():
    db.create_all()
7. Run the Application

Bash
python app.py
Access the application at http://127.0.0.1:5000/.

📂 Project Structure
Plaintext
ai-document-summarizer/
│
├── app.py                  # Main Flask application and routing logic
├── requirements.txt        # Python dependencies
├── db_schema_new.sql       # SQL database schema reference
│
├── static/                 # Frontend assets
│   ├── css/                # Glassmorphism stylesheets
│   ├── js/                 # Client-side validation and async chat logic
│   └── images/             # UI icons and logos
│
├── templates/              # Jinja2 HTML templates
│   ├── base.html           # Main layout wrapper
│   ├── dashboard.html      # User workspace
│   ├── result.html         # Summary & Chat interface
│   ├── split_pdf.html      # PDF manipulation tools
│   └── admin_dashboard.html# Analytics interface
│
├── uploads/                # Temporary storage for user files
└── local_ml_model/         # Cached sentence-transformers model files
📖 Usage Guide
Create an Account: Register a new user profile to access the dashboard.

Upload a Document: Navigate to the main Summarizer tool. Upload a supported file (.pdf, .docx, .pptx, .txt).

Select Options: Choose your desired output format (Paragraphs or Bullet Points) and the summary length.

Interact: Once the summary is generated, use the "Chat" input box below the summary to ask specific questions about the text.

PDF Utilities: Access the "Tools" menu in the navigation bar to Split, Merge, or Convert Images to PDFs independently of the AI engine.

🔮 Future Scope
SaaS Architecture Migration: Transitioning the backend to Django REST Framework and frontend to React.js for enterprise scalability. Database migration from MySQL to PostgreSQL.

OCR Integration: Integrating Tesseract OCR to allow the processing of scanned documents and handwritten notes.

Abstractive Summarization: Upgrading from extractive algorithms (LSA/LexRank) to Large Language Models (LLMs) like Llama 3 for context-aware, generative summarization.

📜 License
This project is licensed under the MIT License. Feel free to use, modify, and distribute it as per the license terms.
