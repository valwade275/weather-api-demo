# Documentation for Val's Weather API Demo 🌦️
This is a simple weather dashboard built using the [OpenWeatherMap Current Weather API](https://openweathermap.org/current) and [Leaflet.js](https://leafletjs.com) for the precipitation map.

## 🔗 Live Demo

👉 [View my weather application here.](https://valwade275.github.io/weather-api-demo)

## 📌 Purpose

This project demonstrates:
- How to fetch and display real-time weather data using the OpenWeatherMap API
- How to visualize precipitation using Leaflet maps
- How to present data cleanly using HTML, CSS, and JavaScript

## 📡 API Overview

### Endpoint
`GET https://api.openweathermap.org/data/2.5/weather`

### 🔐 Authentication
An API key is required. Pass it as a query parameter:
`appid=YOUR_API_KEY`

#### 🔧 Sample Request
`GET https://api.openweathermap.org/data/2.5/weather?lat=29.7604&lon=-95.3698&units=imperial&appid=YOUR_API_KEY`

#### 📥 Query Parameters
| Name   | Type   | Description                              |
|--------|--------|------------------------------------------|
| lat    | float  | Latitude (Houston = 29.7604)             |
| lon    | float  | Longitude (Houston = -95.3698)           |
| appid  | string | Your API key                             |
| units  | string | Units of measurement (`imperial`, `metric`, or `standard`) |

#### 📥 Sample Response (Truncated)
JSON
```
{
  "weather": [
    { "main": "Clear", "description": "clear sky", "icon": "01d" }
  ],
  "main": {
    "temp": 95.2,
    "feels_like": 103.1,
    "humidity": 57,
    "pressure": 1012
  },
  "wind": { "speed": 5.1, "deg": 150 },
  "visibility": 10000,
  "name": "Houston"
}
```
### 🌐 Supported Fields by Current Weather API

In addition to temperature and description, the `/weather` endpoint returns:
- `main.pressure` — atmospheric pressure (hPa)
- `main.humidity` — relative humidity (%)
- `visibility` — visibility distance (meters)
- `clouds.all` — cloudiness (%)
- `wind.speed` — wind speed
- `wind.deg` — wind direction (degrees)
- Optional fields: `rain.1h`, `snow.1h` (if precipitation data is available)

## 🗺️ Precipitation Map Integration

Precipitation tiles are sourced from OpenWeatherMap:
```
https://tile.openweathermap.org/map/precipitation_new/{z}/{x}/{y}.png?appid=YOUR_API_KEY
```
This map is rendered using [Leaflet.js](https://leafletjs.com/), providing interactive map functionality.

## ⚙️ Error Handling

The app gracefully handles:
- Missing API keys
- Invalid API responses
- Network or rate-limiting errors

## 🧾 Swagger/OpenAPI Integration

This project includes a Swagger UI implementation that documents the API integration.

Highlights:
- Organized tags
- Contact and license
- Sample responses
- Schema components
- API key security scheme

👉 [View the Swagger UI page](https://valwade275.github.io/weather-api-demo/docs) 

## 💻 Technologies Used

- HTML/CSS/JavaScript
- OpenWeatherMap API
- Leaflet.js
- GitHub Pages for deployment
- Swagger UI for interactive API docs 

