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

### Запуск Лабораторної №10 Docker EFK-стек і Telegram-бота

## 🚀 1. Як запустити EFK-стек

1. Перейдіть у директорію з конфігурацією `docker-compose.yml`:

   ```bash
   cd ./EFK-stack
   ```

2. Запустіть усі сервіси у фоновому режимі:

   ```bash
   docker compose up
   ```

3. Відкрийте Kibana у браузері:

   ```
   http://localhost:5601
   ```

4. **ЯКЩО У ТЕБЕ У ВКЛАДЦІ Discover НЕМАЄ ІНДЕКСУ, ЯКИЙ ЩОСЬ ВІДОБРАЖАЄ
   то потрібно додати шаблон індексу (index pattern) у Kibana:

   * Перейдіть до **Stack Management → Index Patterns**

   * Натисніть **Create index pattern**

   * У полі шаблону (pattern) введіть:

     ```
     fluentd-*
     ```

   * Натисніть **Next step**

   * У полі вибору часу оберіть:

     ```
     @timestamp
     ```

   * Натисніть **Create index pattern**

---

## 🤖 2. Як запустити Telegram-бота

1. Перейдіть у директорію з ботом:

   ```bash
   cd telegram_bot
   ```

2. Активуйте віртуальне середовище:

   ```bash
   source venv/Scripts/activate
   ```

   > Якщо середовище ще не створене, виконайте:

   ```bash
   python -m venv venv
   source venv/Scripts/activate
   pip install -r requirements.txt
   ```

3. Запустіть бота:

   ```bash
   python bot.py
   ```

4. Надішліть повідомлення боту в Telegram, щоб протестувати його.

---

## ✅ 3. Перевірка логів у Kibana

1. Відкрийте Kibana:

   ```
   http://localhost:5601
   ```

2. Переконайтесь, що після відправки повідомлення боту, у Kibana з'являються нові логи (на вкладці **Discover**).

---

## 🛑 4. Як зупинити Telegram-бота

1. У терміналі, де працює бот, натисніть `Ctrl + C`.
2. Деактивуйте віртуальне середовище:

   ```bash
   deactivate
   ```

---

## 🧯 5. Як безпечно зупинити EFK-стек

1. Перейдіть у директорію з `docker-compose.yml`:

   ```bash
   cd ./EFK-stack
   ```

2. Зупиніть усі сервіси:

   ```bash
   docker compose down
   ```

   > Це безпечно завершить роботу всіх компонентів (Elasticsearch, Fluentd, Kibana) і видалить контейнери, зберігаючи при цьому дані у volume-ах.

---
