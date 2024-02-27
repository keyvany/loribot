from spotipy.oauth2 import SpotifyClientCredentials
from io import BytesIO
from datetime import datetime
import os
import requests
import telebot
import spotipy
from spotipy.oauth2 import SpotifyClientCredentials
from telebot.types import InputMediaPhoto
import os
import requests
import telebot
import spotipy
from spotipy.oauth2 import SpotifyClientCredentials
from telebot.types import InputMediaPhoto
from spotipy.oauth2 import SpotifyClientCredentials
from io import BytesIO
from datetime import datetime
import os
import requests
import telebot
import spotipy
from spotipy.oauth2 import SpotifyClientCredentials
from telebot.types import InputMediaPhoto
TOKEN = '7044505333:AAG3fIwXYXnbX8JF7MZyxat5qO7P0IEN1rs'
bot = telebot.TeleBot(TOKEN)

SPOTIFY_CLIENT_ID = '416c3974385a46a9ac7f894710637701'
SPOTIFY_CLIENT_SECRET = '513ebcdc5173437e82f500bb72cf22fd'
sp = spotipy.Spotify(client_credentials_manager=SpotifyClientCredentials(client_id=SPOTIFY_CLIENT_ID, client_secret=SPOTIFY_CLIENT_SECRET))

@bot.message_handler(commands=['start'])
def send_welcome(message):
    bot.reply_to(message, "Welcome to the Spotify downloader bot!\nPlease enter the Spotify URL to download the mp3 and the art cover")
    print(message.text)

@bot.message_handler(func=lambda message: True)
def download_cover_art(message):

       url = message.text
       # print(url)
       # track_id = url.split('/')[-1]
       track = sp.track(url)
       cover_url = track['album']['images'][0]['url']

       response = requests.get(cover_url)
       print(response.status_code)
       with open('cover.jpg', 'wb') as file:
          file.write(response.content)
       with open('cover.jpg', 'rb') as photo:
          bot.send_photo(message.chat.id, photo)

       track_url = url # Extract the Spotify track URL from the message
       track_info = sp.track(track_url)  # Get track information
       track_name = track_info['name']
       track_preview_url = track_info['preview_url']

       if track_preview_url:
          response = requests.get(track_preview_url)


          with open(track_name + '.mp3', 'wb') as f:
            f.write(response.content)

          with open(track_name + '.mp3', 'rb') as audio:
            bio = BytesIO()
            bio.name = track_name + '.mp3'
            bio.write(audio.read())
            bio.seek(0)

            bot.send_audio(chat_id=message.chat.id, audio=bio)

bot.polling()
