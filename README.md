# Инструкции по работе с репозиторием

## Работа с GIT и подмодулями

### Инициализация и обновление подмодулей

```sh
# В самом начале работы с репозиторием
git submodule update --init --recursive
```

### Обновление подмодуля до последнего коммита

```sh
cd path/to/submodule
git fetch                     # Обновить информацию о подмодулях
git checkout main             # Переключиться на основную ветку
git pull origin main          # Обновить основную ветку
git submodule update --remote # Обновить подмодули до последних коммитов в их репозиториях
```

### Если менялось название проекта

```sh
git rm --cached exchangeBot
git submodule sync
git submodule update --init --recursive
```

### Откат подмодуля

```sh
git submodule update --checkout
```

### Сохранение изменений подмодулей

```sh
git add exchangebot exchangeService feederapp
git commit -m "Update submodules to latest commits"
```

---

## Работа с Docker Compose

### Аутентификация

```sh
docker login
```

### Сборка и загрузка образов

- **Собрать образы (не запускать контейнеры):**
  ```sh
  docker-compose build
  ```
- **Загрузить собранные образы в реестр Docker:**
  ```sh
  docker-compose push
  ```

### Запуск контейнеров

```sh
docker-compose up
```

### Получение последних версий образов и запуск

```sh
docker-compose pull
docker-compose up
```

### Локальный запуск с пересборкой

```sh
docker-compose up --build
```

### Использование флагов

- `--no-deps` — не запускать зависимости указанных сервисов.
- `--detach` или `-d` — запуск в фоновом режиме.
- `--force-recreate` — пересоздать контейнеры даже без изменений образа.
- `--build` — пересобрать образы перед запуском.

#### Пример: перезапуск только изменённых контейнеров

```sh
docker-compose pull
docker-compose up -d --no-deps
```

### Запуск с разными окружениями

- **Dev-окружение:**
  ```sh
  docker-compose -f docker-compose.yaml -f docker-compose.dev.yaml up --build -d
  ```
- **Prod-окружение:**
  ```sh
  docker-compose -f docker-compose.yaml -f docker-compose.prod.yaml up -d
  ```

### Сборка или отправка определённого образа

```sh
docker compose -f docker-compose.yaml -f docker-compose.prod.yaml build feeder_app
docker compose -f docker-compose.yaml -f docker-compose.prod.yaml push feeder_app
```

### Перезапуск одного сервиса

```sh
docker-compose -f docker-compose.yaml -f docker-compose.prod.yaml up -d --force-recreate