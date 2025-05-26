# web

1. 새 폴더 만들기
2. 가상환경 만들기
```
conda create -n webApp python=3.9
```
![image](https://github.com/user-attachments/assets/fc12bdc5-01bc-4be6-a355-e4bbb2260745)

3. Flask 프레임워크 설치
```
pip install flask
```
4. Flask 구조
```
/your-flask-app
    /static
        /css
        /js
        /images
    /templates
        layout.html
        index.html
        login.html
    app.py
    requirements.txt
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
6. templates/index.html 파일 만들기
```
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Address Book</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <h1>Address Book in A class</h1>
    <form action="/add" method="post">
        <label for="htmlname">Name:</label>
        <input type="text" id="htmlname" name="pyname" required>

        <label for="htmlphone">Phone:</label>
        <input type="text" id="htmlphone" name="pyphone" required>

        <button type="submit">Add Contact</button>
    </form>
    <img src="{{ url_for('static', filename='images/a.jpg') }}" alt="Logo" style="display:block; margin:32px auto 0; width:160px; height:auto;">
</body>
</html>
```
7. static/style.css 파일 만들기
```
body {
    font-family: 'Segoe UI', Arial, sans-serif;
    background: linear-gradient(120deg, #e0eafc 0%, #cfdef3 100%);
    margin: 0;
    padding: 0;
    min-height: 100vh;
}

h1 {
    color: #2d3a4b;
    text-align: center;
    margin-top: 40px;
    letter-spacing: 2px;
    font-weight: 700;
}

form {
    background: #fff;
    padding: 40px 48px 32px 48px; /* 좌우 패딩을 36px → 48px로 늘림 */
    border-radius: 16px; /* 더 둥글게 */
    box-shadow: 0 8px 32px rgba(44, 62, 80, 0.14);
    max-width: 420px;
    margin: 48px auto;
    display: flex;
    flex-direction: column;
    gap: 18px; /* 간격 증가 */
}

label {
    display: block;
    margin-bottom: 4px; /* 라벨-인풋 간격 조정 */
    font-weight: 600;
    color: #34495e;
    letter-spacing: 1px;
}

input[type="text"] {
    width: 100%;
    padding: 14px;
    margin-bottom: 0; /* 인풋 아래 마진 제거 */
    border: 1px solid #bfc9d1;
    border-radius: 8px;
    font-size: 1rem;
    transition: border 0.2s;
    background: #f8fafc;
}

input[type="text"]:focus {
    border: 1.5px solid #5cb85c;
    outline: none;
    background: #fff;
}

button {
    margin-top: 10px; /* 버튼 위에 여백 추가 */
    background: linear-gradient(90deg, #5cb85c 0%, #48c6ef 100%);
    color: white;
    padding: 14px 0;
    border: none;
    border-radius: 8px;
    font-size: 1.1rem;
    font-weight: 600;
    cursor: pointer;
    box-shadow: 0 2px 8px rgba(44, 62, 80, 0.08);
    transition: background 0.2s, transform 0.1s;
}

button:hover {
    background: linear-gradient(90deg, #48c6ef 0%, #5cb85c 100%);
    transform: translateY(-2px) scale(1.03);
}
```
## 실행 하기
브라우저에서 http://127.0.0.1:5000로 접속하여 이름과 전화번호를 입력하고 저장할 수 있습니다.
![image](https://github.com/user-attachments/assets/76c47e9f-4040-47bc-ad4b-1c23b301f997)
