# YaMDb_api

## _RESTful API для проекта YaMDb_

> YaMDb это интернет-сервис, где каждый может оставить свой отзыв на книгу,
кино, музыку. Пользователи могут поделиться впечатлениями и обсудить отзыв
в комментариях.

> Проект YaMDb развивается, что стало результатом создания YaMDb_api.
Через этот интерфейс смогут работать мобильное приложение или чат-бот;
через него же можно будет передавать данные в любое приложение или на фронтенд.

## Технологии проекта

- При проектировании API мы придерживались принципов REST, 
  что привело к повышению производительности и упрощению архитектуры проекта в целом.
- Yatube это Django-проект, что позволило подключить библиотеку Django REST Framework,
  которая ускорила разработку REST API. 
- Для обмена данными в API применяется формат JSON.

### Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/BuriloT/yamdb_final.git
```

```
cd api_yamdb
```

Cоздать и активировать виртуальное окружение:

```
python3 -m venv env
```

```
source env/bin/activate
```

Установить зависимости из файла requirements.txt:

```
python3 -m pip install --upgrade pip
```

```
pip install -r requirements.txt
```

Выполнить миграции:

```
python3 manage.py migrate
```

Запустить проект:

```
python3 manage.py runserver
```


## Некоторые примеры запросов к API.


Получение списка всех произведений.


``` 
GET /api/v1/titles/
```

RESPONSE:

```
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "id": 0,
        "name": "string",
        "year": 0,
        "rating": 0,
        "description": "string",
        "genre": [
          {
            "name": "string",
            "slug": "string"
          }
        ],
        "category": {
          "name": "string",
          "slug": "string"
        }
      }
    ]
  }
]
```

Добавление новой публикации в коллекцию публикаций.Права доступа: Администратор.
Нельзя добавлять произведения, которые еще не вышли (год выпуска не может быть больше текущего).
При добавлении нового произведения требуется указать уже существующие категорию и жанр.

```
POST /api/v1/titles/
```

REQUEST:

```
{
  "name": "string",
  "year": 0,
  "description": "string",
  "genre": [
    "string"
  ],
  "category": "string"
}
```

Добавление нового отзыва. Пользователь может оставить только один отзыв на произведение.
Права доступа: Аутентифицированные пользователи.


```
POST /api/v1/titles/{title_id}/reviews/
```

REQUEST:

```
{
  "text": "string",
  "score": 1
}
```

Добавление комментария к отзыву.
Права доступа: Аутентифицированные пользователи.

```
POST /api/v1/titles/{title_id}/reviews/{review_id}/comments/
```

REQUEST:

```
{
  "text": "string"
}
```

![example workflow](https://github.com/BuriloT/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
