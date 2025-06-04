### 1. Запуск RabbitMQ у Docker


```bash
docker compose up
```

* Інтерфейс RabbitMQ буде доступний за адресою: [http://localhost:15672](http://localhost:15672)
* Логін: `user`
* Пароль: `password`

### 2. Створення та активація віртуального середовища

```bash
python -m venv venv
```
```bash
source venv/Scripts/activate
```
### 3. Встановлення залежностей

```bash
pip install -r requirements.txt
```

---

## 🚀 Послідовність запуску

### У двох окремих терміналах:

#### Термінал 1: запуск SenderBot

```bash
source venv/Scripts/activate
```
```bash
python sender_bot.py
```
#### Термінал 2: запуск ReceiverBot

```bash
source venv/Scripts/activate
```
```bash
python receiver_bot.py
```
---

## 🧪 Тестування

1. Відкрий чат із **SenderBot** у Telegram.
2. Надішли будь-яке повідомлення.
3. Перевір чат із **ReceiverBot** — повідомлення має з’явитися там із префіксом:
   `"Викладач <Ім’я> почав віддалену пару і пише: <текст>"`

---

## 📁 Структура проєкту

```
lab7-rabbitmq-telegram/
├── docker-compose.yml
├── requirements.txt
├── sender_bot.py
├── receiver_bot.py
├── get_chat_id.py
└── README.md
```

---

## 🧹 Завершення роботи

Після завершення тестування:
# Зупинити RabbitMQ

```bash
docker compose down
```
# Деактивувати середовище
```bash
deactivate
```


