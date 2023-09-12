# VirtuAI
AI program created by AI 
```python
import random
import pyttsx3
from tkinter import *
import requests

text_to_speech_engine = pyttsx3.init()

def translate_english_to_polish(text):
    
    
    return "Przetłumaczony tekst z angielskiego na polski."


def translate_polish_to_english(text):
    

    return "Przetłumaczony tekst z polskiego na angielski."


def generate_answer(question):
    
    return "Przykładowa odpowiedź na pytanie."


def text_to_speech(text):

    text_to_speech_engine.say(text)
    text_to_speech_engine.runAndWait()

def change_background_color():
    colors = ['lightblue', 'lightgreen', 'lightpink', 'lightyellow']
    root.configure(bg=random.choice(colors))


def check_weather(city):
    try:
        response = requests.get(f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid=YOUR_API_KEY")
        weather_data = response.json()
        temperature_kelvin = weather_data["main"]["temp"]
        temperature_celsius = temperature_kelvin - 273.15
        description = weather_data["weather"][0]["description"]
        return f"Pogoda w {city}: {description}, temperatura: {temperature_celsius:.2f}°C"
    except Exception as e:
        print(f"Błąd podczas sprawdzania pogody: {str(e)}")
        return "Nie udało się sprawdzić pogody."


def convert_units(unit_from, unit_to, value):
    try:
        response = requests.get(f"https://api.exchangerate-api.com/v4/latest/{unit_from}")
        exchange_rates = response.json()["rates"]
        if unit_to in exchange_rates:
            converted_value = value * exchange_rates[unit_to]
            return f"{value} {unit_from} to {unit_to} = {converted_value} {unit_to}"
        else:
            return "Nie można przeliczyć jednostek."
    except Exception as e:
        print(f"Błąd podczas przeliczania jednostek: {str(e)}")
        return "Nie udało się przeliczyć jednostek."

def display_meme(text):
    try:
        response = requests.get(f"https://api.imgflip.com/get_memes")
        memes = response.json()["data"]["memes"]
        if memes:
            meme = random.choice(memes)
            meme_url = meme["url"]
            return f"Oto mem pasujący do twojego zapytania:\n{meme_url}"
        else:
            return "Nie udało się znaleźć memu."
    except Exception as e:
        print(f"Błąd podczas wyszukiwania memu: {str(e)}")
        return "Nie udało się znaleźć memu."


root = Tk()
root.title("Aplikacja Chatu")
root.geometry("400x300")
root.configure(bg='lightblue')  # Domyślne tło


def communicate_with_user():
    while True:
        label = Label(root, text="Wybierz opcję:")
        label.pack()

        translate_button = Button(root, text="Tłumacz tekst", command=translate_text)
        translate_button.pack()

        answer_button = Button(root, text="Generuj odpowiedź", command=generate_response)
        answer_button.pack()

        speech_button = Button(root, text="Konwertuj na mowę", command=convert_to_speech)
        speech_button.pack()

        weather_button = Button(root, text="Sprawdź pogodę", command=check_current_weather)
        weather_button.pack()

        unit_converter_button = Button(root, text="Przelicz jednostki", command=convert_units_ui)
        unit_converter_button.pack()

        meme_button = Button(root, text="Wyświetl mem", command=display_meme_ui)
        meme_button.pack()

        background_button = Button(root, text="Zmień tło", command=change_background_color)
        background_button.pack()

        exit_button = Button(root, text="Wyjdź", command=root.quit)
        exit_button.pack()

        root.mainloop()

def translate_text():
    text = input("Wpisz tekst do tłumaczenia:
 ")
    lang = input("Wybierz język tłumaczenia (1 - angielski na polski, 2 - polski na angielski): ")
    if lang == "1":
        translated_text = translate_english_to_polish(text)
    elif lang == "2":
        translated_text = translate_polish_to_english(text)
    else:
        print("Nieprawidłowy wybór języka.")
        return
    print(f"Tłumaczenie: {translated_text}")

def generate_response():
    question = input("Wpisz pytanie: ")
    response = generate_answer(question)
    print(f"Odpowiedź: {response}")

def convert_to_speech():
    text = input("Wpisz tekst do konwersji na mowę: ")
    text_to_speech(text)
    print("Odtworzono tekst jako mowę.")

def check_current_weather():
    city = input("Podaj miasto, dla którego chcesz sprawdzić pogodę: ")
    weather_result = check_weather(city)
    print(weather_result)

def convert_units_ui():
    unit_from = input("Podaj jednostkę źródłową: ")
    unit_to = input("Podaj jednostkę docelową: ")
    value = float(input("Podaj wartość do przeliczenia: "))
    result = convert_units(unit_from, unit_to, value)
    print(result)

def display_meme_ui():
    text = input("Podaj tekst, a znajdziemy mem dla Ciebie: ")
    meme_result = display_meme(text)
    print(meme_result)

# Rozpoczęcie komunikacji z użytkownikiem
print("Rozpoczęto komunikację.")
communicate_with_user()
```
