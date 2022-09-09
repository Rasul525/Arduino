# Arduino
from pyfirmata import Arduino, util
import telebot
import time
MyDevice = Arduino("COM2")
MyTooken = "5431067635:AAEEA8WSzwRL3ajoPSwZfbRNxuRipaCEVcU"
MyBot = telebot.TeleBot(MyTooken)

print('Bot is online...')

@MyBot.message_handler(commands=['start'])
def Start(message):
    MyBot.reply_to(message,'Salam! Sizin ucun ne ede bilerem')

@MyBot.message_handler(func= lambda message: True)
def UserMessage(message):
    UserData = str(message.text).upper()
    if UserData == 'SALAM':
        for i in range(5):
            MyDevice.digital[13].write(1)
            time.sleep(2)
            MyDevice.digital[13].write(0)
            time.sleep()


MyBot.infinity_polling()
