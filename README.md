import requests

def get_weather(api_key, city):
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    params = {
        'q': city,
        'appid': api_key,
        'units': 'metric',  # You can use 'imperial' for Fahrenheit
    }

    response = requests.get(base_url, params=params)
    weather_data = response.json()

    return weather_data

def display_weather(weather_data):
    if weather_data['cod'] == '404':
        print("City not found. Please check the spelling.")
    else:
        main_info = weather_data['main']
        weather = weather_data['weather'][0]

        print(f"Weather in {weather_data['name']}, {weather_data['sys']['country']}:")
        print(f"Temperature: {main_info['temp']}°C")
        print(f"Description: {weather['description']}")

if __name__ == "__main__":
    api_key = "Add you're own api_key"
    city = "Brooklyn,New York"  # Changed the city name to Brooklyn,New York

    weather_data = get_weather(api_key, city)
    display_weather(weather_data)
