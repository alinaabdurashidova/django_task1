# Документация по проекту


## 1. Активация виртуального окружения

Виртуальное окружение создается в папке, где будет реализован проект. Далее необходимо набрать команды на терминале для создания и активации:

```
python3 -m venv venv

. venv/bin/activate
```

## 2. Установка расширений

Для установки сразу нескольких расширений создается текстовый файл **req.txt** и все их наименования прописываются в данном файле. Далее через терминал производится их установка по команде:

```
pip install -r req.txt
```


## 3. Создание базы данных

Для этого необходимо зайти через терминал в PostgreSql и создать базу данных по следующей команде:

```
CREATE DATABASE <Наименование базы данных>
```

(в данном проекте название БД - django_task13)


## 4. Создание самого проекта

На терминале необходимо прописать следующую команду:

```
django-admin startproject config . 
```

После чего в папке нашего будет создан проект **config** со встроенными папками и файлами


## 5. Создания приложения ***Study***

Для создания новых приложений необходимо написать на терминале следующие команды:

```
python3 manage.py startapp Study

```

## 6. Загрузка приложения в файле settings.py

В данном файле необходимо добавить наши приложения в **INSTALLED_APPS**:
```python
INSTALLED_APPS = [
    ...
    'Study',
]
```

Также необходимо соединиться с базой данных, которую мы создали ранее:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'django_task13',
        ...
        'HOST': 'localhost',
        'PORT':5432
    }
}

```
## 7. Создание моделей для приложения

Создание моделей **Student** и **Course** для приложения **Study** в файле models.py (Study/models.py):

```python
from django.db import models

class Student(models.Model):
    first_name = models.CharField(max_length = 50)
    last_name = models.CharField(max_length = 50)
    email = models.EmailField()
    age = models.IntegerField()
    created_at = models.DateTimeField(auto_now_add = True)
    updated_at = models.DateTimeField(auto_now = True)

class Course(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField()
    students = models.ManyToManyField(
        Student, 
        related_name = 'courses'
    )
```




## 8. Миграции

Миграция является способом отслеживания изменений в структуре базы данных. В терминале необходимо будет прописать следующие команды:

```
python manage.py makemigrations
python manage.py migrate
```

## 9. Создание админа (superuser)

Для создания админа необходимо написать в терминале следующую команду:

```
python manage.py createsuperuser
```

## 10. Работа через административный интерфейс Django

После создания админа необходимо запистить проект по команде
```
python3 manage.py runserver
```
Далее проходим на сервер по указанному адресу и заходим на страницу авторизации админа (http://127.0.0.1:8000/admin/)

![Auth](/img/authorization.png "auth")

После авторизации у нас открывается страница с указаниями наших моделей (таблиц)

![Table](/img/tables.png "table")

На данном этапе можно будет совершать весь **CRUD** функционал

***Create***

При нажатии на кнопку **Add+** на соответсвующие таблицы можно написать данные:

![Student](/img/student.png "student")

![Course](/img/course.png "course")

Далее необходимо все внесенные данные сохранить


***Read***

Для получения добавленных данных в таблицах необходимо нажать на саму таблицу:

![St](/img/st.png "student")
![Co](/img/cu.png "course")


***Update и Delete***

Для изменения или удаления данных можно будет сделать по выбранному объекту:

![Student](/img/student_change.png "student")

![Course](/img/course_change.png "course")