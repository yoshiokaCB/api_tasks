# ダウンロード

```
git clone https://github.com/yoshiokaCB/api_tasks.git
cd api_tasks
```

# Docker imageのビルド

```
docker build -t pythone-api .
```

# Docker Imageの起動とログイン

以下のコマンドを実行してコンテナを起動＆Bashでログインする。

```
docker run -it --rm -v "$PWD":/code -w /code -p 8000:8000 pythone-api:latest /bin/bash
```

# DB作成と初期設定

dockerを起動後・ログイン後、以下のコマンドを実行してDBの作成とスーパーユーザーの登録を行う。

```
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

以下サンプル。
Emailは空の状態でエンターでOK。
passwordは入力値によっては警告が出るが、無視して（Y）でOK。
```
Username (leave blank to use 'root'): admin
Email address: 
Password: 
Password (again): 
The password is too similar to the username.
This password is too short. It must contain at least 8 characters.
This password is too common.
Bypass password validation and create user anyway? [y/N]: y
Superuser created successfully.
```

上記設定が終わったら、`exit` でコンテナを終了する。

# サーバー起動

設定終了後以下のコマンドでサーバー起動

```
docker run -it --rm -v "$PWD":/code -w /code -p 8000:8000 pythone-api:latest \
/bin/bash -c "python manage.py runserver 0.0.0.0:8000"
```

http://localhost:8000/admin にアクセスして先ほど作成した superuser でログインできることを確認する。
