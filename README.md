#Бібліотеки:
from speech_recognition import *
import pyttsx3
import webbrowser
import datetime
import wikipedia
#Голос:
def speak(audio):
    rate=engine.getProperty('rate') 
    engine.setProperty('rate',rate-17)
    engine.say(audio)
    engine.runAndWait()
engine=pyttsx3.init('sapi5')
voices=engine.getProperty('voices')
engine.setProperty('voice',voices[1].id)
hourd=datetime.datetime.now()
#Функція Привітання:
def wishme():
    hour=int(datetime.datetime.now().hour)
    if hour>=7 and hour<13:
        speak('Good morning!')
    elif hour>=13 and hour<18:
        speak('Good afternoon!')
    else:
        speak('Good evening!')
#Розпізнавання:
def rcom():
    UROD=Recognizer()
    with Microphone() as source:
        print('Listening...')
        UROD.pause_threshold=1.0
        audio=UROD.listen(source)
        try:
            print('Listen...')
            query=UROD.recognize_google(audio,language='en-in')
            print('Runing...')
        except:
            print('Say again please...')
            return 'None'
        return query
#Розпізнавання для Вікіпедії:
def rcom():
    UROD=Recognizer()
    with Microphone() as source:
        print('Listening...')
        UROD.pause_threshold=1.0
        audio=UROD.listen(source)
        try:
            print('Listen...')
            querya=UROD.recognize_google(audio,language='en-in')
            print('Runing...')
        except:
            print('Say again please...')
            return 'None'
        return querya
#Функції:
if __name__=='__main__':
    wishme()
    speak('What can I help you?')
    while True:
        query=rcom().lower()
        if 'wikipedia' in query:
            print("I'm listening'")
            querya=rcom().lower()
            speak('Searching wikipedia...')
            results=wikipedia.summary(querya,sentences=5)
            speak('According to Wikipedia')
            print(results)
            speak (results)
        if 'open youtube' in query:
            webbrowser.open('youtube.com')
        elif 'what time is it' in query:
            speak(hourd)
        elif 'open browser' in query:
            webbrowser.open('google.com')
        elif 'stop' in query:
            speak('Goodbye,have a nice day!')
            break
