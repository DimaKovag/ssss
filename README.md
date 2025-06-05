### 1. Запуск Лабораторної №3 Docker

Спочатку перейти в директорію:
```bash
cd C:\Users\Дмитро\Desktop\Lab3\docker_lab03
```
Запустити команду для побудови і запуску контейнерів у фоновому режимі:
```bash
docker compose up -d
```
Перевірити, що всі сервіси працюють:
```bash
docker compose ps
```
frontend має бути доступний щоб перевірити в браузері:
```bash
http://localhost:1125
```
показує сторінку з Nginx
```bash
backend: http://localhost:8080
```
 API-відповідь з Flask (JSON)


Якщо Виникли проблеми потрібно з нуля:
```bash
docker compose down
```
```bash
docker compose up --build -d
```
І тоді перевірка в браузері.

Щоб зупинити сервіси:
```bash
docker compose down
```

### 1. Запуск Лабораторної №7 RabbitMQ через Docker
Спочатку перейти в директорію:
```bash
cd C:\Users\Дмитро\Desktop\lab7_event_architecture
```
Запустити докер:
```bash
docker compose up
```

* Інтерфейс RabbitMQ доступний за адресою: [http://localhost:15672](http://localhost:15672)
* Дані для входу:

  * **Логін:** `user`
  * **Пароль:** `password`

---

### 2. Створення та активація віртуального середовища

```bash
python -m venv venv
```

```bash
source venv/Scripts/activate
```

---

### 3. Встановлення необхідних залежностей

```bash
pip install -r requirements.txt
```

---

## 🚀 Запуск проєкту

Запускай два окремі термінали — для кожного з ботів.

---

### Термінал 1 — запуск **message\_sender.py** (бот: `EventPublisherBot`)

```bash
source venv/Scripts/activate
```
```bash
python message_sender.py
```

---

### Термінал 2 — запуск **message\_receiver.py** (бот: `EventListenerBot`)

```bash
source venv/Scripts/activate
```
```bash
python message_receiver.py
```

---

## 🧪 Перевірка роботи системи

1. Відкрий Telegram та знайди бота **EventPublisherBot**.
2. Надішли йому будь-яке повідомлення.
3. У чаті з **EventListenerBot** має з'явитися відповідь у вигляді:

```
Користувач <Ім’я> надіслав: <текст повідомлення>
```

> Щоб отримати `chat_id` для вставлення у `message_receiver.py`, спочатку запусти `fetch_chat_id.py` і надішли повідомлення боту.

---

## 📁 Структура проєкту

```
lab7-event-architecture/
├── docker-compose.yml
├── requirements.txt
├── message_sender.py      # бот-відправник
├── message_receiver.py    # бот-отримувач
├── fetch_chat_id.py       # допоміжний бот для отримання chat_id
└── README.md
```

---

## 🧹 Завершення роботи

### Зупинка RabbitMQ

```bash
docker compose down
```


   docker compose down
   ```

   > Це безпечно завершить роботу всіх компонентів (Elasticsearch, Fluentd, Kibana) і видалить контейнери, зберігаючи при цьому дані у volume-ах.

---

````markdown
# 📡 Моніторинг із Prometheus + Grafana + Telegram Bot

Цей репозиторій демонструє, як запустити моніторинг системи за допомогою **Prometheus**, **Grafana** та **Telegram-бота**, який видає метрики на `/metrics`.

---

## 🔧 1. Запуск Prometheus + Grafana

1. Перейдіть у директорію з `docker-compose.yml`:

   ```bash
   cd ./prometheus-lab/PrometheusLab
````

2. Запустіть контейнери:

   ```bash
   docker compose up
   

3. Переконайтесь, що сервіси доступні:

   * 🔗 Prometheus: [http://127.0.0.1:9090](http://127.0.0.1:9090)
   * 📊 Grafana: [http://127.0.0.1:3000](http://127.0.0.1:3000)

---

## 🤖 2. Запуск Telegram-бота з метриками

1. Перейдіть у директорію бота:

   
Bash

   cd ./telegram_bot
   

2. Якщо ще немає віртуального середовища, створіть і активуйте його:

   
Bash

   python -m venv venv
   source venv/Scripts/activate  # або source venv/bin/activate на Linux/macOS
   pip install -r requirements.txt
   

3. Запустіть бота:

   
Bash

   python bot.py
   

4. Перевірте метрики:

   * 📈 Відкрий у браузері: [http://127.0.0.1:9091/metrics](http://127.0.0.1:9091/metrics)
   * Ви побачите щось на кшталт:

     

     # HELP received_messages_total Total number of received Telegram messages
     # TYPE received_messages_total counter
     received_messages_total 5.0
     

---

## 📊 3. Налаштування Grafana

1. Відкрий Grafana: [http://127.0.0.1:3000](http://127.0.0.1:3000)

   * Логін: admin
   * Пароль: admin

2. Додай джерело даних (Data Source):

   * Натисни: ☰ → Connections → Data Sources

   * Обери: Add data source

   * Тип: Prometheus

   * URL:

     

     http://prometheus:9090
     

   * Натисни: Save & test

---

## 📈 4. Створення Dashboard у Grafana

1. У Grafana натисни: Dashboards → New → Explore

2. У полі Metrics введи:

   

   received_messages_total
   

3. Натисни Run Query, після цього:

   * Add to dashboard → New panel
   * Дай назву панелі
   * Збережи Dashboard

---

## 🛑 5. Зупинка всіх сервісів

### Зупинити Prometheus + Grafana

Bash

cd ./prometheus-lab/PrometheusLab
docker compose down

### Зупинити Telegram-бота

* Натисни Ctrl + C у терміналі
* Деактивуй середовище:

  
Bash

  deactivate
  

---

## 📎 Корисні посилання

* 🔍 Prometheus: [http://127.0.0.1:9090](http://127.0.0.1:9090)
* 📊 Grafana: [http://127.0.0.1:3000](http://127.0.0.1:3000)
* 📈 Метрики бота: [http://127.0.0.1:9091/metrics](http://127.0.0.1:9091/metrics)
