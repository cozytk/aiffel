### 플라스크

*마이크로 웹 프레임워크*

- 마이크로 : 플라스크의 특징인 웹서비스를 구성하는 최소한의 기능을 담음. 단순하지만 확장 가능
- 프레임워크 : 기본적으로 필요한 기능들이 미리 구축되어 있어 추가하고자 하는 기능들만 선별적으로 개발

### 프로젝트 구조

```
~/aiffel/flask_app
└─ pyproject/
      ├─ __init__.py
      ├─ app.py
      ├─ app_data.py
      ├─ app_image.py
      ├─ static/
      └─ templates/
          ├─ index.html
          ├─ data.html
          └─ image.html
```

/templates/index.html

```html
<html>

<head>
    <title>전처리 페이지 UI</title>
</head>

<body>

    <form action="/get_selected_table" method="POST" enctype="multipart/form-data">
        <input type="text" name="table_name" placeholder="테이블 명" required="required" />
        <button type="submit">선택</button>
        {% if label %}
            <span>
                {{ label }}
            </span>
        {% endif %}

    </form>

    <form action="/get_column_name_change" method="POST" enctype="multipart/form-data">
        <h1>컬럼 이름 변경</h1>
            <input type="text" name="before_column_name" placeholder="변경 전 컬럼명" required="required" />
            <input type="text" name="after_column_name" placeholder="변경 후 컬럼명"required="required" />
        <br>
        <br>
        <button type="submit">변경</button>
    </form>

    <form action="/get_image_pre_status" method="POST" enctype="multipart/form-data">
        <h1>이미지 전처리 종류 선택</h1>
        <input type="checkbox" name="pre_toggle_0">
        <span>180도 회전 </span>
        <br>
        <input type="checkbox" name="pre_toggle_1">
        <span>흑백 변경 </span>
        <br>
        <input type="checkbox" name="pre_toggle_2">
        <span>이미지 사이즈 변경 </span>
        <br>
        <button type="submit">변경</button>
    </form>

    <form action="/upload_image" method="POST" enctype="multipart/form-data">
        <h1>이미지 업로드 하기</h1>
        <input type="file" name="uploaded_image">
        <button>이미지 업로드</button>
        {% if label %}
            <span>
                {{ label }}
            </span>
        {% endif %}
    </form>
</body>

</html>
```

/app.py

```python
from flask import Flask, render_template, request
from flask_ngrok import run_with_ngrok

import os

app = Flask(__name__)
run_with_ngrok(app)

'''
File upload
'''
@app.route("/index")
def index():
    return render_template('index.html')

@app.route('/get_column_name_change', methods=['POST'])
def column_name_change():
    # aft_column_name = request.form.values('after_column_name')
    bef_column_name = request.form.get('before_column_name')
    aft_column_name = request.form.get('after_column_name')

    print(bef_column_name)
    print(aft_column_name)

    return render_template('index.html')

@app.route('/get_image_pre_status', methods=['POST'])
def image_preprocessing():
    if request.method == 'POST':
        print("0 = ", request.form.get('pre_toggle_0'))
        print("1 = ", request.form.get('pre_toggle_1'))
        print("2 = ", request.form.get('pre_toggle_2'))
    return render_template('index.html')

@app.route('/get_selected_table', methods=["POST"])
def selected_table():
       text = request.form.get('table_name')
       print(text)
       return render_template('index.html')

@app.route('/get_selected_table2', methods=["POST"])
def select_table2():
   text = request.form.get('textbox')

   return render_template('index.html', label=text)

@app.route('/upload_image', methods=['POST'])
def upload_image_file():
    if request.method == 'POST':
        file = request.files['uploaded_image']
        if not file: return render_template('index.html', label="No Files")
        label = file

        return render_template('index.html', label=label)

if __name__ == '__main__':
    app.run()
```

/templates/image.html

```python
<html>

<head>
    <title>이미지 전처리 페이지</title>
</head>

    <body>

        <form action="/image_preprocess" method="POST" enctype="multipart/form-data">
            <h1>이미지 업로드 하기</h1>
            <input type="file" name="uploaded_image">

            <h1>이미지 전처리 종류 선택</h1>
            <input type="checkbox" name="pre_toggle_0">
            <span>180도 회전 </span>
            <br>
            <input type="checkbox" name="pre_toggle_1">
            <span>흑백 변경 </span>
            <br>
            <input type="checkbox" name="pre_toggle_2" id="change_image_size_cb" onclick="setTextBoxShow()">
            <span>이미지 사이즈 변경 </span>

            <h1 id="size_header"style="display:none">이미지 사이즈 지정</h1>
                <input type="text" id="width_size" name="changed_width" placeholder="넓이(width)를 입력해주세요" onkeypress="onlyNumber()" style="display:none"/>
                <input type="text" id="height_size" name="changed_height" placeholder="높이(height)를 입력해주세요" onkeypress="onlyNumber()" style="display:none"/>
            <br>

            <script>
            function onlyNumber(){

                    if((event.keyCode<48)||(event.keyCode>57))

                       event.returnValue=false;

            }
            function setTextBoxShow() {
              var checkBox = document.getElementById("change_image_size_cb");
              if (checkBox.checked == true){
                width_size.style.display = "block";
                height_size.style.display = "block";
                size_header.style.display = "block";

              } else {
                width_size.style.display = "none";
                height_size.style.display = "none";
                size_header.style.display = "none";
              }
            }
            </script>

            {% if label %}
                <span>
                    결과 저장 경로 :
                </span>
            <br>
                <span>
                    {{ label }}
                </span>
            <br>
            <br>
            {% endif %}
            <button type="submit">변경</button>
        </form>
    </body>
</html>
```

app_image.py

```python
from flask import Flask, render_template, request
from flask_ngrok import run_with_ngrok
import os
from PIL import Image

app = Flask(__name__)
run_with_ngrok(app)

'''
이미지 처리 함수
'''
def image_resize(image, width, height):
        return image.resize((int(width), int(height)))

def image_rotate(image):
    return image.transpose(Image.ROTATE_180)

def image_change_bw(image):
    return image.convert('L')

'''
플라스크
'''
@app.route("/index")
def index():
    return render_template('image.html')

@app.route('/image_preprocess', methods=['POST'])
def preprocessing():
    if request.method == 'POST':
        file = request.files['uploaded_image']
        if not file: return render_template('index.html', label="No Files")

        img = Image.open(file)

        is_rotate_180 = request.form.get('pre_toggle_0')
        is_change_bw = request.form.get('pre_toggle_1')
        is_change_size = request.form.get('pre_toggle_2')

        if is_rotate_180 == 'on':
            img = image_rotate(img)

        if is_change_bw == 'on':
            img = image_change_bw(img)

        if is_change_size == 'on':
            img = image_resize(img, request.form.get('changed_width'), request.form.get('changed_height'))

        img.save('result_image.png')

        src_dir = os.path.dirname(os.path.abspath(__file__))
        image_path = os.path.join(src_dir, 'result_image.png')

        # 결과 리턴
        return render_template('image.html', label=image_path)

if __name__ == '__main__':
    app.run()
```

/templates/data.html

```html
<html>

<head>
    <title>SQL 처리 페이지</title>
</head>

<body>
    <h1>SQL 처리 페이지</h1>
        <form action="/dbsql" method="POST">
        <h2>데이터베이스 이름</h2>
        <span> <input type="text" name="db_name" placeholder="ex)name.db"> </span>

        <h2>SQL (명령어 한 줄만 가능)</h2>
        <textarea name="sql" cols="40" rows="10" placeholder="ex) SELECT * FROM table_name"></textarea>
        <br>
        {% if label %}
            <span class="result_lable">
                {% block content %}
                {{ label }}
                {% endblock %}
            </span>
        <br>
        {% endif %}

        <button type="submit">SQL 전송</button>

    </form>
</body>

</html>
```

/app_data.py

```python
from flask import Flask, render_template, request
from flask_ngrok import run_with_ngrok
import os
import sqlite3
import pandas as pd

app = Flask(__name__)
run_with_ngrok(app)

'''
DB 함수
'''
def get_db(db_name):
    return sqlite3.connect(db_name)

def sql_command(conn, command):

    try :

        conn.execute(command)
        conn.commit()
        command = command.lower()

        if "select" in command:

            command_split = command.split(" ")
            select_command = "SELECT * FROM " + command_split[command_split.index("from")+1]
            df = pd.read_sql(select_command, conn, index_col=None)
            html = df.to_html()

            conn.close()

            return html, 1

        conn.close()

        return True, 1

    except Exception as exception:

        conn.close()

        return False, exception

'''
File upload
'''
@app.route("/index")
def index():
    return render_template('data.html')

@app.route('/dbsql', methods=['POST'])
def sql_processing():
    if request.method == 'POST':

        con = get_db('/' + request.form.get('db_name'))
        sql = request.form.get('sql')
        result_sql, excep = sql_command(con, sql)

        if result_sql == False :
            return render_template('data.html', label="비정상" +  str(excep))

        elif result_sql == True :
            return render_template('data.html', label="정상 작동")

        else :
            result_sql = "<html><body> " + result_sql + "</body></html>"
            return result_sql

if __name__ == '__main__':
    app.run()
```