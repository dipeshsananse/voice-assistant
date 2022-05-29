# voice-assistant

  #Project jarvis
from asyncio import Task
import ipaddress
from bs4 import BeautifulSoup
from importlib.abc import ExecutionLoader
from multiprocessing import Condition
from operator import ipow, mod
import profile
from playsound import playsound
from re import search
from time import time
from tkinter import E
from winreg import QueryValue, QueryValueEx
import speech_recognition as sr
import datetime
import wikipedia
import pyttsx3
import webbrowser
import random
import os
import subprocess as sp     
import pyjokes
import requests
import wikipedia as googlescrap
import time
import sys
import os.path
import requests
import cv2
import pyautogui
import instadownloader
import instaloader
import pywikihow
import pywhatkit as kit




engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
#print(voices)
engine.setProperty('voice',voices[0].id)
engine.setProperty('rate',200)



def speak(audio):  #here audio is var which contain text
    engine.say(audio)
    engine.runAndWait ()
    engine.setProperty('rate',200)

def wish():
    hour = int(datetime.datetime.now().hour)
    tt = time.strftime("%I:%M %p")  

    if hour >= 0 and hour <= 12:
        speak(f"good morning,its {tt}")
    elif hour >=12 and hour <= 24:
        speak(f"good afternoon, its {tt}") 
    else:
        speak(f"good night,its {tt}")  
    speak("i am jarvis sir, please tell me how can i help you")


def takecommand():
    r = sr.Recognizer()
    with sr.Microphone(device_index=1) as source:
        print("Listning....")
        audio = r.listen(source)
    try:
        print("Recognising.") 
        query = r.recognize_google(audio,language='en-in')
        print(f"user said: {query}")


    except Exception as e:
        
        return "none"    
    query = query.lower()
    return query            #For Error handling
        

    

#for main function                               

if __name__ == "__main__":
    wish()
    while True:
        query = takecommand().lower()

        if "wikipedia" in query:
            speak("searching details....Wait")
            query.replace("wikipedia","")
            results = wikipedia.summary(query,sentences=2)
            print(results)
            speak(results)
            
            
        elif 'open youtube' in query or "open video online" in query:
            webbrowser.open("www.youtube.com")
            speak("opening youtube")



        elif 'open github' in query:
            webbrowser.open("https://www.github.com")
            speak("opening github")  



        elif 'open facebook' in query:
            webbrowser.open("https://www.facebook.com")
            speak("opening facebook")



        elif 'open instagram' in query:
            webbrowser.open("https://www.instagram.com")
            speak("opening instagram") 



        elif 'open google' in query:
            webbrowser.open("https://www.google.com")
            speak("opening google")


            
        elif 'open yahoo' in query:
            webbrowser.open("https://www.yahoo.com")
            speak("opening yahoo")


            
        elif 'open gmail' in query:
            webbrowser.open("https://mail.google.com")
            speak("opening google mail") 


            
        elif 'open snapdeal' in query:
            webbrowser.open("https://www.snapdeal.com") 
            speak("opening snapdeal") 


             
        elif 'open amazon' in query or 'shop online' in query:
            webbrowser.open("https://www.amazon.com")
            speak("opening amazon")



        elif 'open flipkart' in query:
            webbrowser.open("https://www.flipkart.com")
            speak("opening flipkart") 

        elif 'open disney hotstar' in query:
            webbrowser.open("https://www.disneyplus.com")
            speak('ok sir opening disney plus hotstar')

        elif 'open ebay' in query:
            webbrowser.open("https://www.ebay.com")
            speak("opening ebay")



        elif 'music from pc' in query or "music" in query:
            speak("ok i am playing")
            music_dir = 'C:\\Users\\pc\\Desktop\\bass songs'
            music = os.listdir(music_dir)
            os.startfile(os.path.join(music_dir,music[0]))
        elif"send message " in query:
            kit.sendwhatmsg("+919767959978","this is testing",5,15)



        
        elif 'movies from pc' in query or "video" in query:
            speak("ok sir i am showing all movies please play any 1")
            movies_dir = './video'
            npath = "E://movies"
            os.startfile(npath)


            
        elif 'the time' in query:
            strfTime = datetime.datetime.now().strftime("%I:%M:%S")   
            speak(f"Sir, the time is {strfTime}")

        elif "open camera" in query:
            cap = cv2.VideoCapture(0)
            while True:
                RET, IMG = cap.read()
                cv2.imshow( "webcam", IMG)
                k = cv2.waitKey(50)
                if k==27:
                  break; 
            cv2.destroyAllWindows()        

     



        elif "shutdown" in query:
            speak("shutting down")
            os.system('shutdown -s') 

        elif "whatsapp" in query or 'how are you' in query:
            stMsgs = ['Just doing my thing!', 'I am fine!', 'Nice!', 'I am nice and full of energy','i am okey ! How are you']
            ans_q = random.choice(stMsgs)
            speak(ans_q)  
            ans_take_from_user_how_are_you = takecommand()
            if 'fine' in ans_take_from_user_how_are_you or 'happy' in ans_take_from_user_how_are_you or 'okey' in ans_take_from_user_how_are_you:
                speak('okey..')  
            elif 'not' in ans_take_from_user_how_are_you or 'sad' in ans_take_from_user_how_are_you or 'upset' in ans_take_from_user_how_are_you:
                speak('oh sorry..') 
        
        elif 'your developer' in query or 'created you' in query or 'your developer ' in query:
            ans_m = " For your information Created by dipesh sir ! I give Lot of Thannks to Him "
            print(ans_m)
            speak(ans_m)
        
        elif "who are you" in query or "about you" in query or "your details" in query:
            about = "I am J an A I based computer program but i can help you lot like a your close friend ! i promise you ! Simple try me to give simple command ! like playing music or video from your directory i also play video and song from web or online ! i can also entain you i so think you Understand me ! ok Lets Start "
            print(about)
            speak(about)

        elif "hello" in query or "hello Jarvis" in query:
            hel ="hello sir DIPESH"
            print(hel)
            speak(hel)
        
        elif "your name" in query or "sweat name" in query:
            na_me = "Thanks for Asking my name my self ! Jarvis"  
            print(na_me)
            speak(na_me)

        elif "yours feeling" in query:
            print("feeling Very sweet after meeting with you")
            speak("feeling Very sweet after meeting with you") 
        elif query == 'none':
            continue 

        elif"goodbye" in query:
            speak ("tanks for using me sir and have a good day")
            sys.exit()    

        
        elif "open spotify" in query:
            npath = "C:\\Users\\pc\\AppData\\Roaming\\Spotify\\spotify.exe"            
            os.startfile(npath)
        
        
        elif "open command prompt" in query:
            os.system("start cmd")

        if "open notepad" in query:
            npath = "C:\\WINDOWS\\system32\\notepad.exe"
            os.startfile(npath) 

        elif 'timer' in query or 'stopwatch' in query:
            speak("For how many minutes?")
            timing = takecommand()
            timing =timing.replace('minutes', '')
            timing = timing.replace('minute', '')
            timing = timing.replace('for', '')
            timing = float(timing)
            timing = timing * 60
            speak(f'I will remind you in {timing} seconds')

        elif "tell me a joke" in query:
            joke = pyjokes.get_joke()
            speak(joke)

        elif "open asphalt 9" in query:
            npath = "C:\\Users\\pc\\Desktop"            
            os.startfile(npath)

        elif "temperature" in query:    
            search = "temperature in bhusawal"
            url = f"https://www.google.com/search?q={search}"
            r = requests.get(url)
            data = BeautifulSoup(r.text,"html.parser")
            temp = data.find("div",class_="BNeawe").text
            speak(f"current {search} is {temp}")
        
        elif "where i am" in query or "where we are" in query:
            speak("wait sir ! let me scan form satellite")
            speak("sir i am not sure, but i think we are in bhusawal city of jalgoan district from maharashtra in india  ")
            
        elif "instagram profile" in query:
             speak("sir please enter the user name")
             name = input("enter username here :")
             webbrowser.open(f"www.instagram.com/{name}")
             speak(f"sir here is the profile of the user {name}")
             time.sleep(5)
             speak("sir would you like to download pic of profile")
             Condition = takecommand().lower()
             if "yes" in Condition:
                 mod = instadownloader.instaloader()
                 mod.download_profile(name, profile_pic_only=True)
                 speak("i am done sir,profile pic is saved") 
                  

        elif "activate how to do mod" in query:
            from pywikihow import search_wikihow
            speak("how to do mode is activated please tell me what you want to know") 
            how = takecommand()
            max_result = 2
            how_to = search_wikihow(how, max_result)
            assert len(how_to) == 1
            how_to[0].print()
            speak (how_to[0].summary)        
    
        elif "volume up" in query:
            pyautogui.press("volumeup")

        elif "volume down" in query:
            pyautogui.press("volumedown")

        elif "volume mute" in query:
            pyautogui.press("volumemute")

        elif"goodbye" in  query:
            speak ("tanks or using me sir and have a good day ")
            sys.exit()      

        elif"what is your feeling about me my jarvis" in query:
            speak("Baba Re Baba ya !bahut buri !chijj hai ")



        elif "set alarm" in query:  
          speak('sir please tell me the time to set alarm. form example, set alarm to 5:30 a.m')
          tt = takecommand()
          tt = tt.replace("set alarm to ", "")
          tt = tt.replace(".","")
          tt = tt.upper()
          playsound.alarm

        elif 'ok tell'in query:
            query = query.replace("jarvis","")
            query = query.replace("google search","")
            query = query.replace("google","")
            speak("this is what i found on the DATA BASE!")
            kit.search(query)
         
            try:
                results = googlescrap.summary(query,2)
                speak (results)

            except:
                speak("on speakable data available!")


                
if __name__ == "__main__":
    wish()
    while True:
        query = takecommand()
        if"wake up" in query:
           takecommand() 

        elif 'you can sleep now' in query:
            speak("ok sir, you can called any time")
            break

       
