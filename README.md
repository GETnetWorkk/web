# web

1. 새 폴더 만들기
2. 가상환경 만들기
```
conda create -n webApp python=3.9
```
![image](https://github.com/user-attachments/assets/fc12bdc5-01bc-4be6-a355-e4bbb2260745)

4. Flask 프레임워크 설치
```
pip install flask
```
5. app.py 파일 만들기
```
from flask import Flask, render_template, request, redirect
import csv

app = Flask(__name__)

# Route for the home page
@app.route('/')
def index():
    return render_template('index.html')

# Route to handle form submission
@app.route('/add', methods=['POST'])
def add_contact():
    name = request.form['name']
    phone = request.form['phone']

    # Save to addbook.txt in CSV format
    with open('addbook.txt', 'a', newline='', encoding='utf-8') as file:
        writer = csv.writer(file)
        writer.writerow([name, phone])

    return redirect('/')

if __name__ == '__main__':
    app.run(debug=True)
```
