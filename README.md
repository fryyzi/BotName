# Всім привіт тут краткий опис телеграм бота 'BotName'

**Патерн Команда (Command)**
```Python
@bot.message_handler(commands=['start'])
def handle_start(message):
    handler.handle_start(message)
```
**Функція**
```Python
import telebot
from telebot import types
import pymongo

connect = pymongo.MongoClient("mongodb://localhost:27017")
db = connect["botname"]
Withdraw_collection = db["Withdraw"]
User_collection = db["User"]

class CommandHandler:
    def __init__(self, bot):
        self.bot = bot


    def handle_start(self, message):
        markup = types.InlineKeyboardMarkup()

        Balance = types.InlineKeyboardButton(text="Баланс📍", callback_data="Balance")
        markup.row(Balance)

        Support = types.InlineKeyboardButton("🍰Підтримка", callback_data="Support")
        Comments = types.InlineKeyboardButton("✏️Комментарії", callback_data="Comments")
        markup.row(Support, Comments)

        Subscriptions = types.InlineKeyboardButton("🔥Підписка", callback_data="Subscriptions")
        markup.row(Subscriptions)

        collection = types.InlineKeyboardButton("💰Йде збір", callback_data="collection")
        markup.row(collection)

        help_button = types.InlineKeyboardButton("Навіщо бот❓", callback_data="help")
        markup.row(help_button)
    
        self.bot.send_message(message.chat.id, "Ласкаво просимо до botname!\n\n📌Бот дозволяє монетизувати продаж вашого унікального контенту у групах. Також монетизує коментарі користувачів.🔥", reply_markup=markup)
        add_user = {
            "Name_User": message.chat.first_name,
            "User_name": message.chat.username,
            "Id_User": message.from_user.id,
            "Permission": "User",
            "balanse": 0
        }
        User_collection.insert_one(add_user)

```
**Фабричний Метод (Factory Method)**
```Python
from cogs.start import CommandHandler
from cogs.Withdraw import Withdraw
from cogs.admin import Admin
from cogs.add_balanse import Add_balanse
from cogs.help.help import Help
from cogs.Subcribes.Subcribes import Subcribes
from cogs.Approve.Approve import Approve
from cogs.Author.Author import Author
from cogs.Channel.Channel import Channel
from cogs.Channel_Setting.Message.Message import Message
from cogs.Channel_Setting.Stop.Stop import Stop
from cogs.Channel_Setting.strict_regime.strict import Strict
from cogs.WhileLIst.WhileList import WhileList

handler = CommandHandler(bot)
withdraw_instance = Withdraw(bot)
admins = Admin(bot)
add_balanse = Add_balanse(bot)
help = Help(bot)
Sub = Subcribes(bot)
approve = Approve(bot)
author = Author(bot)
channel = Channel(bot)
message_class = Message(bot)
stop = Stop(bot)
strict = Strict(bot)
W_list = WhileList(bot)
```
**Патерн Наблюдатель (Observer)**
```Python
@bot.message_handler(func=lambda message: True, content_types=['new_chat_members'])
def new_member(message):
    if message_class.new_persone_status == "Вкл":
        try:
            chat_id = message.chat.id
            bot.send_message(chat_id, f"Ласкаво просимо до групи, @{message.from_user.username}!")
        except:
            bot.send_message(chat_id, "Помилка, не вдалося розпізнати користувача!")
```
## Результат роботи
**Start**
### Тут знаходиться стартовий функціонал бота
![Screen](https://i.imgur.com/iJBX11t.png)
___
**Підтримка**
### За допомогою цієї функції користуваю зможе попросити допомогои у тех.Підримки
![Screen](https://i.imgur.com/CLdTI7a.png)
____
**Підписка**
### У розділі підписка користувач зможе купити підписку у бота на свій телеграм канал і йому буде доступно функції для преміум користувача
![Screen](https://i.imgur.com/P02Uq7b.png)
