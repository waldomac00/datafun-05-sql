# Michael J Moore: SQLite Books & Authors Project

This project demonstrates how to create and manage a simple **relational database** using **SQLite3** and Python. It models a **one-to-many (1:M) relationship** between authors and books:
- One author can have many books.
- Each book is associated with exactly one author.

The project uses **CSV files** as the source of data and a Python script (`book_manager.py`) to:
1. Verify project folders exist.
2. Create a SQLite database file.
3. Execute SQL statements to define tables.
4. Load data from CSV files into staging tables.
5. Insert the data into relational tables while preserving primary key and foreign key constraints.
6. Add an `is_favorite` column to the books table for extended functionality.

---

## 📂 Project Structure

```
datafun-05-sql/
│
├── data/                   # Data files (CSV sources)
│   ├── authors.csv
│   └── books.csv
│
├── sql/                    # SQL scripts
│   └── create_tables.sql
│
├── book_manager.py         # Python script to build & load the database
├── book_db.sqlite3         # SQLite database file (created after running the script)
├── README.md               # Project documentation
├── requirements.txt        # Project dependencies
└── .gitignore              # Ignore virtual environment, db files, etc.
```

---

## ⚙️ Setup and Workflow

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/datafun-05-sql.git
cd datafun-05-sql
```

### 2. Create and Activate a Virtual Environment
#### Windows
```bash
py -3.12 -m venv .venv
.\.venv\Scripts ctivate
```

#### macOS / Linux
```bash
python3.12 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies
```bash
python -m pip install --upgrade pip setuptools wheel
python -m pip install pandas
```

### 4. Run the Script
```bash
python book_manager.py
```

After running, the script will:
- Create `book_db.sqlite3` in the project root.
- Build `authors` and `books` tables.
- Load data from `data/authors.csv` and `data/books.csv`.
- Insert rows into the database while preserving constraints.

---

## 🗄️ Database Schema

### Authors Table
- **author_id** (TEXT, PK)  
- **first** (TEXT)  
- **last** (TEXT)  

### Books Table
- **book_id** (TEXT, PK)  
- **title** (TEXT)  
- **year_published** (INTEGER)  
- **author_id** (TEXT, FK → authors.author_id)  
- **is_favorite** (INTEGER, default = 0)  

---

## ✅ Example Data

**authors.csv**
```csv
author_id,first,last
10f88232-1ae7-4d88-a6a2-dfcebb22a596,Harper,Lee
c3a47e85-2a6b-4196-a7a8-8b55d8fc1f70,George,Orwell
e0b75863-866d-4db4-85c7-df9bb8ee6dab,F. Scott,Fitzgerald
```

**books.csv**
```csv
book_id,title,year_published,author_id
d6f83870-ff21-4a5d-90ab-26a49ab6ed12,To Kill a Mockingbird,1960,10f88232-1ae7-4d88-a6a2-dfcebb22a596
0f5f44f7-44d8-4f49-b8c4-c64d847587d3,1984,1949,c3a47e85-2a6b-4196-a7a8-8b55d8fc1f70
f9d9e7de-c44d-4d1d-b3ab-59343bf32bc2,The Great Gatsby,1925,e0b75863-866d-4db4-85c7-df9bb8ee6dab
```

---

## 🔎 Example Query

After running the project, you can explore the database using SQL queries. For example:

```sql
SELECT b.title, b.year_published, a.first || ' ' || a.last AS author
FROM books b
JOIN authors a ON a.author_id = b.author_id
ORDER BY b.year_published ASC;
```

---

## 📝 Notes
- The **is_favorite** field was added to demonstrate modifying an existing table.  
- GUIDs are stored as **TEXT** in SQLite.  
- SQLite is a great entry point for SQL because it is lightweight, serverless, requires no configuration, and stores everything in a single file.  
- This project follows the **plan → create → load → query** workflow, useful for both class projects and real-world prototyping.

---

## 🚀 Next Steps
- Extend the project with your own pair of related tables (e.g., movies and directors, students and courses).  
- Write and test additional SQL queries for filtering, grouping, and joining.  
- Explore indexes, constraints, and triggers for more advanced database functionality.  
