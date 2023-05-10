# chatgpt-telegram-bot
Personal ChatGPT Telegram bot

Бот отправляет сообщение пользователя по OpenAI API в ChatGPT и возвращает обратно текст ответа.  

Используемая модель - `gpt-3.5-turbo`, лимит токенов на один запрос - 3000

### Подготовка к работе

Для работы необходимо создать и заполнить файл `.env` в директории скрипта своими значениями следующим образом:
```env
OPENAI_API_KEY = yourapikey  
TELEGRAM_API_KEY = yourbottoken  
ADMIN_CHAT_ID = 123456789
```

В данном файле:  
1. `OPENAI_API_KEY` - API-ключ от OpenAI
2. `TELEGRAM_API_KEY` - API-токен от бота в Telegram
3. `ADMIN_CHAT_ID` - ID админа в Telegram

`example.env` - это образец `.env` файла. 
Достаточно заполнить его своими значениями и переименовать, чтобы не создавать файл самостоятельно.  

### Запуск бота
`python main.py`  

При первом запуске в директории скрипта будет автоматически создан файл `data.json`, 
в котором будут храниться все необходимые данные.  

При каждом последующем запуске скрипт будет читать данные из ранее созданного файла. 
Обновление файла происходит по мере работы.  

При общении в личных сообщениях бот отправляет ответы в диалог, а 
при общении в групповых чатах - отвечает на конкретное сообщение.

Каждому новому пользователю по умолчанию выдается 30к токенов, 
которые можно использовать в сообщениях боту для запросов по API.

#### Структура файла `data.json`
```json
{
  "global": {
    "requests": 0,
    "tokens": 0
  },
  "admin_id": {
    "requests": 0,
    "tokens": 0,
    "balance": 777777,
    "last_request": "2021-01-01 00:00:00"
  },
  "user1": {
    "123456789": {
      "requests": 0,
      "tokens": 0,
      "balance": 30000,
      "name": "John",
      "username": "@johndoe",
      "last_request": "2021-01-01 00:00:00"
    }
  }
}
```
1. `"global"` - общая статистика бота о количестве запросов и использованных токенов  
2. Статистика админа: число запросов, использованных токенов, несгораемый баланс и дата последнего обращения  
3. Статистика каждого из пользователей: число запросов, использованных токенов, баланс, имя, @юзернейм и дата последнего обращения

### Команды бота  
`/start` - начало работы: регистрация в системе и получение стартового баланса токенов  
`/stats` - выводит статистику по количеству запросов, числу использованных токенов и дате последнего обращения в бота  
`/balance` - выводит текущий баланс токенов  
`/stop` - полностью останавливает бота, доступно только админу
