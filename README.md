import telebot
from telebot import types
bot= telebot.TeleBot("8344516531:AAE6zP2w7fsOFwgIo8D_DDF5QjmCAV0ajHQ")


@bot.message_handler(commands=["start"])
def start(message):
    markup = types.ReplyKeyboardMarkup()
    btn1 = types.KeyboardButton("Выбрать цветы")
    markup.row(btn1)
    btn2 = types.KeyboardButton("Написать в личку для покупки")
    markup.row(btn2)
    bot.send_message(message.chat.id, "Привет", reply_markup=markup)
    bot.register_next_step_handler(message, on_click)
def on_click(message):
    if message.text=="Выбрать цветы":
        bot.send_message(message.chat.id,"Цветы в наличии:\n"
                                         "Жасмин 10.000 тенге\n"
                                                   "Монстера 1 ствольный 10.000 тенге\n"
                                                "Монстера 2 ствольный 18.000 тенге")
    elif message.text =="Написать в личку для покупки":
        bot.send_message(message.chat.id, "https://t.me/bolatbekalia ")
    bot.register_next_step_handler(message, on_click)


@bot.message_handler(commands=["Flowers"])
def main(message):
 bot.send_message(message.chat.id, "Привет")




@bot.message_handler(content_types=["photo", "video", "sticker", 'document', 'audio' ])
def get_photo(message):
            markup = types.InlineKeyboardMarkup()

            btn1 = types.InlineKeyboardButton("Выбрать цветы", callback_data="message")
            markup.row(btn1)
            btn2 = types.InlineKeyboardButton("Написать в личку для покупки", url="https://t.me/bolatbekalia")
            markup.row(btn2)
            bot.reply_to(message, "Команды которые я могу выполнить:",
                         reply_markup=markup)






@bot.callback_query_handler(func=lambda callback: True)
def callback_data(callback):
    if callback.data == "message":
        bot.send_message(callback.message.chat.id, "Жасмин 10.000 тенге\n"
                                                   "Монстера 1 ствольный 10.000 тенге\n"
                                                   "Монстера 2 ствольный 18.000 тенге")

bot.infinity_polling()
