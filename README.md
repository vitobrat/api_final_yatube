# Yatube API

Это учебный проект, представляющий собой backend на Django REST Framework для платформы блога Yatube. Основные функциональные возможности включают:

Система публикации постов — создание, редактирование и просмотр сообщений;
Система пользователей — регистрация пользователей и возможность подписываться на других;
Система комментариев — оставление комментариев под постами;

## Установка и запуск

1. Скачайте репозиторий на свой локальный компьютер

```bash
git clone https://github.com/gutsy51/ya-practicum-backend/tree/master/api_yatube2 
cd api_yatube2
```

2. Создайте и активируйте виртуальное окружение

#### Windows
```bash
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```
#### Linux/MacOS
```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

3. Выполните миграции базы данных
```bash
cd api_yatube
python manage.py migrate
```

4. Запустите сервер разработки
```bash
python manage.py runserver
```

## Краткое описание API

Подробное описание API доступно по адресу: http://localhost/redoc/

### JWT Token
```bash
POST /api/v1/jwt/create/
{
  "username": "username",
  "password": "password"
}
```
Ответ:
```bash
{
  "refresh": "refresh_token",
  "access": "access_token"
}
```

### Posts
| Path                  | Method      | Description           | Access        | 
|-----------------------|-------------|-----------------------|---------------|
| `/api/v1/posts/`      | `GET`       | Get posts (paginated) | Anyone        |
| `/api/v1/posts/`      | `POST`      | Create new post       | Auth          |
| `/api/v1/posts/{id}/` | `GET`       | Get post details      | Anyone        |
| `/api/v1/posts/{id}/` | `PUT/PATCH` | Update post           | Auth + Author |
| `/api/v1/posts/{id}/` | `DELETE`    | Delete post           | Auth + Author |

Примеры:
- `GET /api/v1/posts/`
- `GET /api/v1/posts/?limit=15&offset=0`
- `GET /api/v1/posts/?search=hello`

### Comments
| Path                                     | Method      | Description     | Access        | 
|------------------------------------------|-------------|-----------------|---------------|
| `/api/v1/posts/{post_id}/comments/`      | `GET`       | All comments    | Anyone        |
| `/api/v1/posts/{post_id}/comments/`      | `POST`      | New comment     | Auth          |
| `/api/v1/posts/{post_id}/comments/{id}/` | `GET`       | Comment details | Anyone        |
| `/api/v1/posts/{post_id}/comments/{id}/` | `PUT/PATCH` | Update comment  | Auth + Author |
| `/api/v1/posts/{post_id}/comments/{id}/` | `DELETE`    | Delete comment  | Auth + Author |

Примеры:
- `GET /api/v1/posts/1/comments/`
- `POST /api/v1/posts/1/comments/`

### Follows

| Path                   | Method      | Description     | Access        |
|------------------------|-------------|-----------------|---------------|
| `/api/v1/follow/`      | `GET`       | All follows     | Auth          |
| `/api/v1/follow/`      | `POST`      | New follow      | Auth          |
| `/api/v1/follow/{id}/` | `DELETE`    | Delete follow   | Auth          |

Примеры:
- `GET /api/v1/follow/`
- `POST /api/v1/follow/`