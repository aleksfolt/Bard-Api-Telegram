<h1 align="center">Hi there, I'm <a href="https://github.com/aleksfolt" target="_blank">AleksFolt</a> 


# Bard-Api-Telegram

**Now we will figure out how to use google bard ai without palm api**

i refer to this repository [Bard Api](https://github.com/dsdanielpark/Bard-API) to show how to use bard in telegram

# Install

<pre>$ pip install bardapi</pre> 
or 
<pre>$ pip install git+https://github.com/dsdanielpark/Bard-API.git</pre>

# Authentication

1. Visit https://bard.google.com/
2. Close all tabs besides https://bard.google.com/
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

Telebot

<pre>
@bot.message_handler(commands=['bard'])
def handle_bard_command(message):
    # Get the user's query
    query = message.text.replace('/bard', '').strip()
    
    # Get the response from bardapi
    response = bard.get_answer(query)
    
    # Send the response to the user
    bot.send_message(message.chat.id, response["content"])
</pre>

[![Typing SVG](https://readme-typing-svg.herokuapp.com?color=%2336BCF7&lines=Bard+do+u+like+python?)](https://github.com/aleksfolt)

Or aiogram

<pre>
@dp.message_handler(commands=['bard'])
async def handle_bard_command(message: types.Message):
    # Get the user's query
    query = message.text.replace('/bard', '').strip()
    
    # Get the response from bardapi
    response = bard.get_answer(query)
    
    # Send the response to the user
    await message.answer(response["content"])
</pre>


# Bard, What is Image?


Simple Usage

<pre>from bardapi import Bard

bard = Bard(token='xxxxxxx')
image = open('image.jpg', 'rb').read() # (jpeg, png, webp) are supported.
bard_answer = bard.ask_about_image('What is in the image?', image)
print(bard_answer['content'])</pre>


TeleBot

<pre>@bot.message_handler(commands=['whatisimage'])
def what_is_image(message):
    if message.reply_to_message and message.reply_to_message.photo:
        file_id = message.reply_to_message.photo[-1].file_id
        file_info = bot.get_file(file_id)
        image = bot.download_file(file_info.file_path)
        bard_answer = bard.ask_about_image('What is in the image?', image)
        bot.reply_to(message, bard_answer['content'])
    else:
        bot.reply_to(message, "Please reply to my post with an image first!")
</pre>

Aiogram

<pre>@dp.message_handler(commands=['whatisimage'])
async def what_is_image(message: types.Message, state: FSMContext):
    if message.reply_to_message and message.reply_to_message.photo:
        file_id = message.reply_to_message.photo[-1].file_id
        file_info = await bot.get_file(file_id)
        image = await bot.download_file(file_info.file_path)
        bard_answer = bard.ask_about_image('What is in the image?', image)
        await message.reply_text(bard_answer['content'])
    else:
        await message.reply_text("Please reply to my post with an image first!")</pre>



Thanks to everyone who watched to the end. Remember that I am not responsible for this library and the actions you perform
