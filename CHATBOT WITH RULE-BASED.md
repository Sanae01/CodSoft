```python
import nltk
nltk.download('punkt')
import requests
```

    [nltk_data] Downloading package punkt to
    [nltk_data]     C:\Users\sanae\AppData\Roaming\nltk_data...
    [nltk_data]   Package punkt is already up-to-date!
    


```python
!pip install nltk
```

    Requirement already satisfied: nltk in c:\users\sanae\anaconda3\lib\site-packages (3.7)
    Requirement already satisfied: click in c:\users\sanae\anaconda3\lib\site-packages (from nltk) (8.0.4)
    Requirement already satisfied: joblib in c:\users\sanae\anaconda3\lib\site-packages (from nltk) (1.2.0)
    Requirement already satisfied: regex>=2021.8.3 in c:\users\sanae\anaconda3\lib\site-packages (from nltk) (2022.7.9)
    Requirement already satisfied: tqdm in c:\users\sanae\anaconda3\lib\site-packages (from nltk) (4.65.0)
    Requirement already satisfied: colorama in c:\users\sanae\anaconda3\lib\site-packages (from click->nltk) (0.4.6)
    


```python
from nltk.tokenize import word_tokenize
```


```python
#This program is a designated chat-bot with rule based responses
```


```python
api_endpoint = "http://api.openweathermap.org/data/2.5/weather"
api_key = "b3d8c75c6a0342f3007bd6735614a55b"
```


```python
answers = {
    "hello":"hi there! how can i help you today?",
    "how are you?":"Im good, how about you?",
    " I need help with this assignment": " sure, give me a clear query and i will work on it"
    }
```


```python
def get_weather(city):
    params = {
        "q": city,
        "appid": api_key,
        "units": "metric"  # You can change this to "imperial" for Fahrenheit
    }
    response = requests.get(api_endpoint, params=params)
    data = response.json()

    if response.status_code == 200:
        main = data['main']
        temperature = main['temp']
        description = data['weather'][0]['description']
        return f"The weather in {city} is {description} with a temperature of {temperature}°C."
    else:
        return "Sorry, I couldn't retrieve the weather information at the moment."
```


```python
def chatbot_response (user_input):
 # tokens= word_tokenize(user_input)
 # for word in tokens:
    if  user_input.lower()in answers :
      return answers[user_input]
    if "weather" in user_input:
      city= input ("Which city's weather would you like to know?")
      weather_response = get_weather(city)
      return weather_response
    return "I'm sorry, I didn't get that."
```


```python
while True:
    user_input = input("You: ")
    if user_input.lower() == "exit":
        break
    response = chatbot_response(user_input)
    print("Bot:", response)
```

    You: hello
    Bot: hi there! how can i help you today?
    You: how are you
    Bot: I'm sorry, I didn't get that.
    You: how are you?
    Bot: Im good, how about you?
    You: whats the weather today?
    Which city's weather would you like to know?casablanca
    Bot: The weather in casablanca is light rain with a temperature of 18.15°C.
    You: exit
    
