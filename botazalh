import telebot
import requests , os
from telebot.types import InlineKeyboardButton as Btn , InlineKeyboardMarkup as Mak

token = "7181810198:AAHNyZLfgdAFYfjHv711iH3YR4nhAheyE3w"
bot = telebot.TeleBot(token)

Key = "PawTQh5RB1AQiqeiW2sS5kpy"
@bot.message_handler(commands=["start"])
def Welcome(message):
 bot.reply_to(message,'ارسل الصوره لازاله الخلفيه منها')

@bot.message_handler(content_types=['photo'])
def handle_photo(message):
    ttxxxn = bot.reply_to(message,'⏳ Removing background...')
    file_info = bot.get_file(message.photo[-1].file_id)
    file = requests.get(f'https://api.telegram.org/file/bot{token}/{file_info.file_path}')
#ttxxxn 
    with open('input_image.png', 'wb') as f:
        f.write(file.content)

    response = requests.post('https://api.remove.bg/v1.0/removebg', files={'image_file': open('input_image.png', 'rb')}, headers={'X-Api-Key': Key})
    
    with open('output_image.png', 'wb') as f:
        f.write(response.content)
    
    bot.delete_message(message.chat.id, ttxxxn.message_id)
    bot.send_photo(message.chat.id, open('output_image.png', 'rb'),reply_to_message_id=message.message_id)

    os.remove('input_image.png')
    os.remove('output_image.png')

bot.polling()
