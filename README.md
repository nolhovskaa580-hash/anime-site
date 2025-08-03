# 🎌 Anime Site - Полнофункциональный аниме-сайт

Современный веб-сайт для просмотра аниме с адаптивным дизайном, системой пользователей и интеграцией с внешними API.

## 🚀 Особенности

- **Полная интеграция с AniLiberty API v1** - современный и быстрый источник данных
- **Каталог аниме** с фильтрацией по жанрам, годам и рейтингу
- **Система поиска** с автодополнением
- **Детальные страницы** аниме с полной информацией
- **Кастомный видеоплеер** с поддержкой HLS, адаптивного качества и субтитров
- **Система прогресса просмотра** с сохранением позиции
- **Система комментариев** в реальном времени
- **Пользовательские профили** и списки просмотра
- **Темная и светлая темы** с сохранением состояния
- **Мобильная оптимизация** и адаптивный дизайн
- **Умное кэширование** для быстрой работы без интернета

## 🛠 Технологический стек

### Frontend
- **React 18** - UI библиотека
- **React Router** - маршрутизация
- **Styled Components** - CSS-in-JS
- **React Query** - управление состоянием сервера
- **Socket.io Client** - реальное время

### Backend
- **Node.js** - серверная среда
- **Express.js** - веб-фреймворк
- **MongoDB** - база данных
- **Socket.io** - WebSocket соединения
- **JWT** - аутентификация

### DevOps
- **Docker** - контейнеризация
- **Docker Compose** - оркестрация
- **Nginx** - веб-сервер

## 📋 Требования

- Node.js >= 16.0.0
- npm >= 8.0.0
- MongoDB >= 5.0
- Docker (опционально)

## 🚀 Быстрый старт

### Вариант 1: С Docker (рекомендуется)

1. **Клонирование репозитория**
```bash
git clone <repository-url>
cd anime-site
```

2. **Настройка окружения**
```bash
cp server/.env.example server/.env
# Отредактируйте server/.env с вашими настройками
```

3. **Запуск с Docker**
```bash
docker-compose up -d
```

4. **Доступ к приложению**
- Frontend: http://localhost:3000
- Backend API: http://localhost:5000
- MongoDB: localhost:27017
- Redis: localhost:6379

### Вариант 2: Локальная установка

1. **Установка зависимостей**
```bash
npm run install:all
```

2. **Настройка базы данных**
```bash
# Убедитесь, что MongoDB запущен
mongod
```

3. **Настройка окружения**
```bash
cp server/.env.example server/.env
# Отредактируйте server/.env
```

4. **Запуск в режиме разработки**
```bash
npm run dev
```

## 📁 Структура проекта

```
anime-site/
├── client/                 # React frontend
│   ├── public/
│   ├── src/
│   │   ├── components/     # Компоненты
│   │   ├── pages/         # Страницы
│   │   ├── context/       # Context API
│   │   ├── hooks/         # Кастомные хуки
│   │   ├── services/      # API сервисы
│   │   └── styles/        # Стили
│   └── package.json
├── server/                # Node.js backend
│   ├── config/           # Конфигурация
│   ├── controllers/      # Контроллеры
│   ├── middleware/       # Промежуточное ПО
│   ├── models/          # Модели MongoDB
│   ├── routes/          # API маршруты
│   ├── services/        # Бизнес-логика
│   └── package.json
├── shared/              # Общие типы и утилиты
├── docs/               # Документация
└── docker-compose.yml  # Docker конфигурация
```

## 🔧 Конфигурация

### Переменные окружения

Скопируйте `server/.env.example` в `server/.env` и настройте:

```env
# Основные настройки
NODE_ENV=development
PORT=5000
MONGODB_URI=mongodb://localhost:27017/anime-site

# JWT
JWT_SECRET=your-secret-key
JWT_EXPIRE=30d

# AniLiberty API
ANILIBERTY_API_BASE=https://aniliberty.top/api/v1

# Внешние API (опционально)
MAL_CLIENT_ID=your-mal-client-id
ANILIST_CLIENT_ID=your-anilist-client-id
KITSU_API_KEY=your-kitsu-api-key
```

### Внешние API

Для полной функциональности используется:

1. **AniLiberty API v1** (основной источник данных)
   - Документация: https://aniliberty.top/api/docs/v1
   - Не требует регистрации для базовых функций
   - Поддержка HLS видео и субтитров

2. **Дополнительные API** (опционально):
   - MyAnimeList API: https://myanimelist.net/apiconfig
   - AniList API: https://anilist.co/settings/developer
   - Kitsu API: https://kitsu.docs.apiary.io/

## 📚 API Документация

### Основные эндпоинты

#### Интеграция с AniLiberty API v1
- `GET /api/anime/popular` - популярные аниме
- `GET /api/anime/new-episodes` - новые эпизоды  
- `GET /api/anime/:id` - детали аниме
- `GET /api/episode/:id` - данные эпизода с видео и субтитрами
- `GET /api/anime/search` - поиск аниме
- `GET /api/anime/catalog` - каталог с фильтрацией
- `GET /api/anime/genres` - список жанров
- `GET /api/status` - статус API и сервера

#### Аутентификация
- `POST /api/auth/register` - Регистрация
- `POST /api/auth/login` - Вход
- `GET /api/auth/me` - Текущий пользователь

#### Пользователи
- `GET /api/users/profile` - Профиль
- `PUT /api/users/profile` - Обновление профиля
- `GET /api/users/watchlist` - Списки просмотра

#### Комментарии
- `GET /api/comments/:animeId` - Комментарии к аниме
- `POST /api/comments` - Создание комментария

### Примеры запросов

```bash
# Получить популярные аниме
curl "http://localhost:5000/api/anime/popular?limit=10"

# Поиск аниме
curl "http://localhost:5000/api/anime/search?query=Naruto"

# Получить данные эпизода
curl "http://localhost:5000/api/episode/12345"

# Фильтрация каталога
curl "http://localhost:5000/api/anime/catalog?genres=Action,Adventure&year=2023"
```

## 🧪 Тестирование

```bash
# Запуск всех тестов
npm test

# Тесты с покрытием
npm run test:coverage

# Только серверные тесты
cd server && npm test

# Только клиентские тесты
cd client && npm test
```

## 🚀 Развертывание

### Production с Docker

1. **Сборка образов**
```bash
docker-compose -f docker-compose.prod.yml build
```

2. **Запуск в production**
```bash
docker-compose -f docker-compose.prod.yml up -d
```

### Heroku

1. **Подготовка**
```bash
heroku create your-app-name
heroku addons:create mongolab:sandbox
```

2. **Настройка переменных**
```bash
heroku config:set NODE_ENV=production
heroku config:set JWT_SECRET=your-production-secret
```

3. **Развертывание**
```bash
git push heroku main
```

## 🤝 Разработка

### Установка для разработки

```bash
# Установка зависимостей
npm run install:all

# Запуск в режиме разработки
npm run dev

# Линтинг
npm run lint

# Форматирование кода
npm run format
```

### Структура коммитов

Используйте [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: добавить систему комментариев
fix: исправить ошибку загрузки видео
docs: обновить README
style: форматирование кода
refactor: рефакторинг API аутентификации
test: добавить тесты для пользователей
```

## 📄 Лицензия

MIT License - см. [LICENSE](LICENSE) файл.

## 👥 Команда

- **Frontend Developer** - React, UI/UX
- **Backend Developer** - Node.js, API
- **DevOps Engineer** - Docker, CI/CD

## 🐛 Сообщить об ошибке

Создайте issue в GitHub с описанием:
- Шаги для воспроизведения
- Ожидаемое поведение
- Фактическое поведение
- Скриншоты (если применимо)

## 🎯 Roadmap

### ✅ Завершено
- [x] **Backend интеграция с AniLiberty API v1**
  - [x] Полная замена AniLibria v3 на AniLiberty v1
  - [x] Умное кэширование и fallback система
  - [x] API endpoints для всех функций
  - [x] Поддержка HLS видео и субтитров

### 🚧 В разработке
- [ ] **Кастомный видеоплеер (React)**
  - [ ] HLS поддержка с адаптивным качеством
  - [ ] Прогресс-бар и сохранение позиции
  - [ ] Загрузка субтитров (WebVTT)
  - [ ] Полноэкранный режим и горячие клавиши

- [ ] **Обновленная пользовательская система**
  - [ ] Избранное и история под AniLiberty
  - [ ] Синхронизация прогресса просмотра
  - [ ] Персональные рекомендации

- [ ] **Улучшенная темная тема**
  - [ ] Сохранение в localStorage
  - [ ] Плавные переходы
  - [ ] Автоматическое переключение

### 📋 Планируется
- [ ] Мобильное приложение (React Native)
- [ ] Рекомендательная система на основе ML
- [ ] Социальные функции и чаты
- [ ] Офлайн режим с кэшированием видео
- [ ] Многоязычность (i18next)
- [ ] PWA функциональность

---

**Создано с ❤️ для любителей аниме**

---

## 📝 Changelog

### v2.0.0 (Текущая версия) - AniLiberty Integration
- ✅ **Полная интеграция с AniLiberty API v1**
- ✅ **Умное кэширование** с fallback на локальные данные
- ✅ **Новая архитектура API** с улучшенной производительностью
- ✅ **Поддержка HLS видео** и субтитров из коробки
- ✅ **Обновленная модель данных** под современные стандарты
- 🚧 **Кастомный видеоплеер** (в разработке)
- 🚧 **Улучшенная пользовательская система** (в разработке)

### v1.0.0 - Initial Release  
- ✅ Базовая функциональность с AniLibria v3
- ✅ Система аутентификации и комментариев
- ✅ Темная/светлая тема