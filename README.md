<h1 align="center">Hi there, I'm <a href="https://github.com/aleksfolt" target="_blank">AleksFolt</a> 


# Bard-Api-Telegram

**Now we will figure out how to use google bard ai without palm api**

i refer to this repository [Bard Api](https://github.com/dsdanielpark/Bard-API) to show how to use bard in telegram

# Install

<pre>$ pip install bardapi</pre> or <pre>$ pip install git+https://github.com/dsdanielpark/Bard-API.git</pre>

# Authentication

1. Visit https://bard.google.com/
2. Close all tabs
3. Open F12 Console
4. Session: Application → Cookies → Copy the value of <code>__Secure-1PSID</code> cookie.

Please note that __Secure-1PSID is not an api and to avoid running into a 
<code>Response Error: b')]}\'\n\n39\n["wrb.fr",null,null,null,null,[13]] \n58\n["di",2250,"af.httprm",2250,"6943458119716357375",2]\n25\n["e",4,null,null,134]\n'. Unable to get response. Please double-check the cookie values ​​and verify your network environment or google account.</code>
please create a new google page and do not go to it so as not to cause this error


# Usage

Simple Usage

<pre>from bardapi import Bard
token = 'xxxxxxx'
bard = Bard(token=token)
print(answer["content"])</pre>

Telegram Usage

<pre>
import telebot
from bardapi import Bard

# Replace 'xxxxxxx' with your token
token = 'xxxxxxx'
bot = telebot.TeleBot(token)

# Initialize the Bard object
bard = Bard(token=token)

@bot.message_handler(commands=['bard'])
def handle_bard_command(message):
    # Get the user's query
    query = message.text.replace('/bard', '').strip()
    
    # Get the response from bardapi
    response = bard.get_answer(query)
    
    # Send the response to the user
    bot.send_message(message.chat.id, response["content"])

# Start the bot
bot.polling()</pre>

Or aiogram Usage

<pre>
import logging
from aiogram import Bot, Dispatcher, types
from aiogram.contrib.middlewares.logging import LoggingMiddleware
from bardapi import Bard

# Replace 'xxxxxxx' with your token
token = 'xxxxxxx'

# Initialize the bot and dispatcher
bot = Bot(token=token)
dp = Dispatcher(bot)
bard = Bard(token=token)

# Enable logging
logging.basicConfig(level=logging.INFO)
dp.middleware.setup(LoggingMiddleware())

@dp.message_handler(commands=['bard'])
async def handle_bard_command(message: types.Message):
    # Get the user's query
    query = message.text.replace('/bard', '').strip()
    
    # Get the response from bardapi
    response = bard.get_answer(query)
    
    # Send the response to the user
    await message.answer(response["content"])

if __name__ == '__main__':
    from aiogram import executor
    executor.start_polling(dp, skip_updates=True)</pre>


# Bard What is Image

