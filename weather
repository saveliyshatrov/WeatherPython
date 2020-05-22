import requests
import telebot

bot = telebot.TeleBot('API_TOKEN')

def takeWeaterInCity(city: str):
    API = 'API_TOKEN'
    url = 'http://api.openweathermap.org/data/2.5/weather?q={}&appid={}'.format(city, API)
    print(url)
    r = requests.get(url=url)
    data = r.json()
    weather = {
        'temperature': round(int(data['main']['temp']) - 273.15),
        'feels': round(int(data['main']['feels_like']) - 273.15),
        'minimal': round(int(data['main']['temp_min']) - 273.15),
        'maximal': round(int(data['main']['temp_max']) - 273.15),
    }
    return weather


print(takeWeaterInCity('Moscow'))

@bot.message_handler(content_types=['text'])
def send_text(message):
    if message.text != '':
        try:
            a = takeWeaterInCity(message.text)
            bot.send_message(message.chat.id, "Температура: {}\nОщущается: {}\nМинимальная температура: {}\nМаксимальная температура: {}".format(a['temperature'], a['feels'], a['minimal'], a['maximal']))
        except Exception:
            bot.send_message(message.chat.id, "Попробуйте еще раз")

bot.polling(none_stop=True)
