# api_final_yatube
### Описание проекта API для Yatube:

REST API для социальной сети Yatube. 

Позволяет делать запросы к моделям проекта: Посты, Группы, Комментарии, Подписки.

Поддерживает методы GET, POST, PUT, PATCH, DELETE

Предоставляет данные в формате JSON


### Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/viserdi/api_final_yatube.git
```

Cоздать и активировать виртуальное окружение:

```
python -m venv env
```

```
source env/Scripts/activate
```

```
python -m pip install --upgrade pip
```

Установить зависимости из файла requirements.txt:

```
pip install -r requirements.txt
```

Выполнить миграции:

```
python manage.py migrate
```

Запустить проект:

```
python3 manage.py runserver
```

### Примеры запросов:


Получение публикаций GET .../api/v1/posts/:

```
Ответ
```
[
    {
        "id": 1,
        "text": "Первый пост",
        "author": "Ivan",
        "image": null,
        "pub_date": "2021-12-22T08:51:30.910768Z",
        "group": 1,
        "comments": [
            {
                "id": 1,
                "author": "Ivan",
                "post": 1,
                "text": "Коммент 1",
                "created": "2021-12-22T08:53:29.476420Z"
            },
            {
                "id": 2,
                "author": "Ivan",
                "post": 1,
                "text": "Коммент 2",
                "created": "2021-12-22T08:53:39.243944Z"
            }
        ]
    },
    {
        "id": 2,
        "text": "Второй пост",
        "author": "Ivan",
        "image": null,
        "pub_date": "2021-12-22T08:51:48.724264Z",
        "group": 1,
        "comments": []
    }
]
```
Создание публикации POST .../api/v1/posts/:
```
Запрос:
```
{
    "text": "Первый пост",
    "group": 1
}
```
Ответ
```
{
"id": 0,
"author": "Ivan",
"text": "Первый пост",
"pub_date": "2019-08-24T14:15:22Z",
"image": null,
"group": 1
}
```
Получение публикации по id GET .../api/v1/posts/0/
```
Ответ:
```
{
"id": 0,
"author": "Ivan",
"text": "Первый пост",
"pub_date": "2019-08-24T14:15:22Z",
"image": null,
"group": 0
}
```
Получение всех комментариев к публикации GET .../api/v1/posts/{post_id}/comments/
```
Ответ:
```
[
  {
    "id": 0,
    "author": "Ivan",
    "text": "some text",
    "created": "2019-08-24T14:15:22Z",
    "post": 0
  }
]
```
Добавление нового комментария к публикации POST .../api/v1/posts/{post_id}/comments/
```
Запрос:
```
{
"text": "comment"
}
```
Ответ:
```
{
  "id": 0,
  "author": "Ivan",
  "text": "comment",
  "created": "2019-08-24T14:15:22Z",
  "post": 0
}
```
Получение комментария к публикации по id GET .../api/v1/posts/{post_id}/comments/{id}/
```
Ответ:
```
{
  "id": 0,
  "author": "Ivan",
  "text": "comment",
  "created": "2019-08-24T14:15:22Z",
  "post": 0
}
```
Получение списка доступных сообществ GET .../api/v1/groups/
```
Ответ:
```
[
  {
    "id": 0,
    "title": "Hobby",
    "slug": "hobby",
    "description": "some description"
  }
]
```
Получение информации о сообществе по id GET .../api/v1/groups/{id}/
```
Ответ:
```
{
  "id": 0,
  "title": "Hobby",
  "slug": "hobby",
  "description": "some description"
}
```
Все подписки пользователя, сделавшего запрос.
Возможен поиск по подпискам по параметру search GET .../api/v1/follow/
```
Ответ:
```
[
  {
    "id": 1,
    "user": "Vasya",
    "following": "Ivan"
  }
]
```
Подписка пользователя от имени которого сделан запрос на пользователя переданного в теле запроса
POST .../api/v1/follow/
```
Запрос:
```
{
  "following": "Vasya"
}
```
Ответ:
```
{
  "user": "Ivan",
  "following": "Vasya"
}