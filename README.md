# 🔄 NL-to-SQL-to-NL Pipeline

An intelligent, bidirectional database query assistant that translates natural language queries into executable SQL, executes them securely against a relational database, and synthesizes the raw tabular output back into clear, conversational natural language answers.

---

## 📌 Features

- **Natural Language to SQL (NL ➔ SQL):** Converts plain English questions into syntactically correct SQL queries using schema-aware prompt engineering.
- **Automated Query Execution:** Connects directly to relational databases to run generated queries safely.
- **SQL to Natural Language (SQL ➔ NL):** Interprets raw database result sets and generates human-readable explanations and executive summaries.
- **Schema-Aware Context:** Dynamically inspects tables, schemas, and column relationships to eliminate hallucinations.
- **Multi-Turn Memory & Validation:** Validates query structure and retains context across multiple queries.

---

## 🔄 Architecture Workflow

```text
       [ User Query ]
             │
             ▼
   ┌───────────────────┐
   │ Schema Inspection │ (Retrieves relevant table & column metadata)
   └─────────┬─────────┘
             │
             ▼
   ┌───────────────────┐
   │  LLM (NL ➔ SQL)   │ (Generates dialect-specific SQL query)
   └─────────┬─────────┘
             │
             ▼
   ┌───────────────────┐
   │ Database Engine   │ (Executes SQL query against DB)
   └─────────┬─────────┘
             │
             ▼
   ┌───────────────────┐
   │  LLM (SQL ➔ NL)   │ (Synthesizes raw tabular output into plain English)
   └─────────┬─────────┘
             │
             ▼
      [ Final Answer ]
```

---

## 🛠️ Tech Stack

- **Language:** Python 3.9+
- **LLM / Frameworks:** LangChain, Groq / LLaMA / OpenAI API
- **Databases Supported:** SQLite, MySQL, PostgreSQL
- **Frontend / Interface:** Streamlit (or CLI)
- **Environment Management:** python-dotenv

---

## 📁 Repository Structure

```plaintext
NL_-SQL_-NL/
├── data/                  # Sample database files / seed data
├── src/
│   ├── db_connector.py    # Database connection & schema extraction
│   ├── sql_generator.py   # NL-to-SQL generation logic
│   └── nl_responder.py    # Result interpretation & response generation
├── app.py                 # Streamlit web app / entrypoint
├── requirements.txt       # Python dependencies
├── .env.example           # Environment variable template
└── README.md
```

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone [https://github.com/CHARANSAI2003/NL_-SQL_-NL.git](https://github.com/CHARANSAI2003/NL_-SQL_-NL.git)
cd NL_-SQL_-NL
```

### 2. Set Up a Virtual Environment
```bash
# macOS/Linux
python3 -m venv venv
source venv/bin/activate

# Windows
python -m venv venv
venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables
Create a `.env` file in the root directory:
```env
# LLM API configuration
OPENAI_API_KEY=your_openai_api_key_here
# or GROQ_API_KEY=your_groq_api_key_here

# Database URI (e.g., sqlite:///data/sample.db or postgresql://user:pass@localhost:5432/dbname)
DATABASE_URI=sqlite:///data/sample.db
```

### 5. Run the Application
```bash
streamlit run app.py
```

---

## 💡 Example Walkthrough

| Step | Example |
| :--- | :--- |
| **User Input** | *"What were the top 3 selling products last month?"* |
| **Generated SQL** | `SELECT product_name, SUM(amount) AS total_sales FROM orders WHERE order_date >= date('now', '-1 month') GROUP BY product_name ORDER BY total_sales DESC LIMIT 3;` |
| **Database Result** | `[("Wireless Mouse", 5200), ("Mechanical Keyboard", 4300), ("USB-C Hub", 3100)]` |
| **NL Response** | *"The top 3 selling products last month were the Wireless Mouse ($5,200), Mechanical Keyboard ($4,300), and USB-C Hub ($3,100)."* |


---

## 👤 Author

- **Charan Sai Batthala** - [GitHub](https://github.com/CHARANSAI2003)
