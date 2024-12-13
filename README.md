 Diploma Project

Этот репозиторий содержит три веб-приложения, разработанных с использованием различных фреймворков на Python: Django, Flask и FastAPI. Каждое из приложений реализует функционал для управления списком задач.

 Содержание

- [Django Project](django-project)
- [Flask Project](flask-project)
- [FastAPI Project](fastapi-project)
- [Установка](установка)
- [Запуск приложений](запуск-приложений)

 # Django Project

 Описание

Приложение на Django предоставляет интерфейс для управления списком задач с возможностью создания, обновления и удаления задач.

 Примеры работы кода

 Модель задачи (models.py)
from django.db import models

class Task(models.Model):
    title = models.CharField(max_length=255)
    completed = models.BooleanField(default=False)

    def __str__(self):
        return self.title


 # Flask Project
Описание
Flask-приложение простое и легковесное, позволяет пользователям добавлять, удалять и редактировать задачи в списке.

Примеры работы кода
Создание приложения (app.py)
from flask import Flask, render_template, request, redirect
from models import Task  # Импорт модели

app = Flask(__name__)

@app.route('/')
def index():
    tasks = Task.query.all()
    return render_template('index.html', tasks=tasks)

@app.route('/add', methods=['POST'])
def add_task():
    title = request.form.get('title')
    task = Task(title=title)
    task.save()  # Сохраните в базу
    return redirect('/')

# FastAPI Project
Описание
FastAPI-приложение предназначено для быстрой разработки RESTful API. Оно обеспечивает высокую производительность и простоту использования.

Примеры работы кода
Создание API (main.py)
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Task(BaseModel):
    title: str
    completed: bool = False

tasks = []

@app.get("/tasks/")
def read_tasks():
    return tasks

@app.post("/tasks/")
def create_task(task: Task):
    tasks.append(task)
    return task

# Установка
Перед запуском приложений убедитесь, что у вас установлены необходимые зависимости. Для этого выполните команду:
pip install -r requirements.txt

# Запуск приложений
Перейдите в директорию djangoProject
cd djangoProject

Запустите приложение
python manage.py runserver

Перейдите в директорию FastAPI
cd DiplomaProject/FastAPI

Запустите FastAPI приложение с помощью Uvicorn
uvicorn main:app --reload

Перейдите в директорию Flask
cd DiplomaProject/Flask

Запустите сервер разработки
python app.py


