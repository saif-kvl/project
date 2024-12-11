<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather Forecast App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin: 0;
      padding: 0;
      background: linear-gradient(to bottom, #6db3f2, #1e69de);
      color: white;
    }
    .container {
      padding: 20px;
      max-width: 400px;
      margin: 50px auto;
      background: rgba(0, 0, 0, 0.5);
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
    input {
      padding: 10px;
      width: calc(100% - 20px);
      border: none;
      border-radius: 5px;
      margin-bottom: 20px;
    }
    button {
      padding: 10px 20px;
      background-color: #1e90ff;
      border: none;
      border-radius: 5px;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background-color: #3ea0ff;
    }
    .weather-info {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Weather Forecast App</h1>
    <input type="text" id="city" placeholder="Enter city name">
    <button onclick="getWeather()">Get Weather</button>
    <div class="weather-info" id="weather-info"></div>
  </div>

  <script>
    const API_KEY = 'your_openweather_api_key'; // Replace with your OpenWeather API key

    async function getWeather() {
      const city = document.getElementById('city').value;
      if (!city) {
        alert('Please enter a city name');
        return;
      }

      const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${API_KEY}&units=metric`;

      try {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error('City not found');
        }
        const data = await response.json();

        displayWeather(data);
      } catch (error) {
        alert(error.message);
      }
    }

    function displayWeather(data) {
      const weatherInfo = document.getElementById('weather-info');
      const { name, main, weather } = data;
      weatherInfo.innerHTML = `
        <h2>${name}</h2>
        <p>Temperature: ${main.temp}&#8451;</p>
        <p>Feels Like: ${main.feels_like}&#8451;</p>
        <p>Weather: ${weather[0].description}</p>
      `;
    }
  </script>
</body>
</html>

