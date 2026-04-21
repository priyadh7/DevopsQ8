# DevopsQ8 Q8 – Containerise Flask Application
STEP 1: Use SAME app
from flask import Flask, request

app = Flask(__name__)
tasks = []

@app.route('/')
def home():
    return "<h3>To-Do</h3>" + str(tasks) + \
           "<form action='/add' method='post'>" \
           "<input name='task'><button>Add</button></form>"

@app.route('/add', methods=['POST'])
def add():
    tasks.append(request.form['task'])
    return "Added <a href='/'>Back</a>"

if __name__ == '__main__':
    app.run(debug=True)
requirements.txt
flask

STEP 3: Dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]

STEP 4: Build image
docker build -t flask-container .
docker run -d -p 5000:5000 --name myflask flask-container

STEP 5: Run container
docker run -d -p 5000:5000 --name myflask flask-container

🪜 STEP 6: Check output
http://localhost:5000
