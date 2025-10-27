# Expense_Tracker
📋 Project Overview

Expense Tracker is a Python-based application that helps users manage and analyze their daily income and expenses.
It allows users to add, view, edit, and delete expense records while providing insightful summaries and data visualization for better financial awareness.

This project is ideal for learning Python with database integration, Flask/Django web frameworks, and data visualization using Matplotlib or Plotly.

🧠 Key Features

✅ Add income and expense records
✅ Categorize expenses (Food, Travel, Bills, etc.)
✅ View total balance, monthly and yearly summaries
✅ Search and filter by category or date
✅ Data visualization using charts (Pie/Bar)
✅ Persistent data storage using SQLite or MySQL
✅ Export reports to CSV or Excel
✅ Simple and responsive UI (if web-based)

🏗️ Tech Stack
Layer	Technology
Language	Python 3.x
Framework	Flask / Django (choose based on your version)
Database	SQLite / MySQL
Visualization	Matplotlib / Plotly
Frontend (if web)	HTML, CSS, Bootstrap
IDE	VS Code / PyCharm / Jupyter / Eclipse with PyDev
🗂️ Project Structure (Flask Example)
expense_tracker/
│
├── app.py
├── requirements.txt
├── README.md
│
├── static/
│   ├── css/
│   ├── js/
│   └── images/
│
├── templates/
│   ├── index.html
│   ├── add_expense.html
│   ├── view_expenses.html
│   └── summary.html
│
└── database/
    └── expenses.db

⚙️ Installation & Setup
1️⃣ Clone the Repository
git clone https://github.com/yourusername/expense-tracker.git
cd expense-tracker

2️⃣ Create a Virtual Environment
python -m venv venv

3️⃣ Activate the Virtual Environment

Windows:

venv\Scripts\activate


macOS/Linux:

source venv/bin/activate

4️⃣ Install Dependencies
pip install -r requirements.txt


(Example requirements.txt)

Flask
Flask-SQLAlchemy
matplotlib
pandas

5️⃣ Initialize the Database
python
>>> from app import db
>>> db.create_all()
>>> exit()

6️⃣ Run the Application
python app.py


Visit → http://localhost:5000

🧩 Example Code (app.py - Flask version)
from flask import Flask, render_template, request, redirect
from flask_sqlalchemy import SQLAlchemy
from datetime import datetime

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///expenses.db'
db = SQLAlchemy(app)

class Expense(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(100))
    amount = db.Column(db.Float)
    category = db.Column(db.String(50))
    date = db.Column(db.DateTime, default=datetime.utcnow)

@app.route('/')
def index():
    expenses = Expense.query.order_by(Expense.date.desc()).all()
    return render_template('index.html', expenses=expenses)

@app.route('/add', methods=['POST'])
def add():
    title = request.form['title']
    amount = float(request.form['amount'])
    category = request.form['category']
    new_expense = Expense(title=title, amount=amount, category=category)
    db.session.add(new_expense)
    db.session.commit()
    return redirect('/')

@app.route('/delete/<int:id>')
def delete(id):
    expense = Expense.query.get_or_404(id)
    db.session.delete(expense)
    db.session.commit()
    return redirect('/')

if __name__ == '__main__':
    app.run(debug=True)

📊 Future Enhancements

User authentication and login system

Monthly budget planner

Graphical insights using Plotly

Export data to Excel or PDF

Email notifications or reminders

🧠 Learning Outcomes

Understanding CRUD operations in Python

Using Flask + SQLAlchemy ORM

Handling templates and forms

Data visualization and analytics

Deploying Flask apps on servers (like Heroku or Render)
