# 📘 Tutorial: How to Build Val's Weather App

## 🧭 Step 1: Define the Project Goal

**Goal:** Create a single-page weather dashboard that pulls live weather data for Houston, TX (or another location of your choice).  
**Tools:** OpenWeatherMap, Leaflet.js, HTML, CSS, JavaScript, Swagger UI, GitHub Pages

## 🔌 Step 2: Obtain Your API Key

Go to [OpenWeather](https://openweathermap.org/api) and register for a free account. After creating your account, an API key will be generated for you.

*Note:* It may be helpful to open the [OpenWeather API documentation](https://openweathermap.org/api/one-call-3) in a separate browser tab for reference.

## 💻 Step 3: Write the HTML Code

Begin a new `.html` file. [Click here for HTML basics](https://www.w3schools.com/html/html_basic.asp).  
*Note:* You can add your CSS code within the same document or link to a separate stylesheet. [Click here for CSS basics](https://www.w3schools.com/html/html_css.asp).

## ⚙️ Step 4: Write the JavaScript Code

Place your JavaScript code inside `<script>` tags within your `.html` file. This code instructs the application to connect to the API, add the precipitation map, and pull the appropriate information.

*Note:* Replace `<YOUR_API_KEY_HERE>` with your actual API key. Also, you can change the map’s location by modifying the latitude and longitude values.

```html
<script>
const apiKey = 'YOUR_API_KEY_HERE';
const lat = 29.7604, lon = -95.3698;
const units = 'imperial'; // use 'metric' for Celsius

const url = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${apiKey}&units=${units}`;

fetch(url)
  .then(res => res.json())
  .then(data => {
    const { temp, feels_like, pressure, humidity } = data.main;
    const visibility = data.visibility;
    const { speed: windSpeed, deg: windDeg } = data.wind;
    const cloudiness = data.clouds?.all;
    const description = data.weather[0].description;
    const icon = data.weather[0].icon;
    const iconUrl = `https://openweathermap.org/img/wn/${icon}@2x.png`;

    document.getElementById('weather').innerHTML = `
      <h2>${data.name}</h2>
      <img src="${iconUrl}" alt="${description}">
      <p><strong>Condition:</strong> ${description}</p>
      <p><strong>Temperature:</strong> ${temp}&deg; (Feels like ${feels_like}&deg;)</p>
      <p><strong>Humidity:</strong> ${humidity}%</p>
      <p><strong>Pressure:</strong> ${pressure} hPa</p>
      <p><strong>Visibility:</strong> ${(visibility / 1609.34).toFixed(1)} mi</p>
      <p><strong>Cloudiness:</strong> ${cloudiness}%</p>
      <p><strong>Wind:</strong> ${windSpeed} mph (from ${windDeg}&deg;)</p>
    `;
  })
  .catch(err => {
    document.getElementById('weather').innerText = 'Unable to fetch weather data.';
    console.error(err);
  });

// Map Initialization
const map = L.map('map').setView([lat, lon], 7);

// Base map layer
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
  attribution: '&copy; OpenStreetMap contributors'
}).addTo(map);

// Precipitation overlay
L.tileLayer(
  `https://tile.openweathermap.org/map/precipitation_new/{z}/{x}/{y}.png?appid=${apiKey}`,
  {
    opacity: 0.6,
    attribution: '&copy; OpenWeatherMap'
  }
).addTo(map);
</script>
```

## 📊 Step 5: Display the Data

Once you've successfully fetched weather data from the API, the next step is to extract and display it in your HTML.  
You will typically work with the `main`, `weather`, `wind`, and other objects in the JSON response.

For example, after calling `fetch()` and parsing the JSON, you can target specific values like this:

```js
const { temp, feels_like, pressure, humidity } = data.main;
const { speed: windSpeed, deg: windDeg } = data.wind;
const cloudiness = data.clouds?.all;
const description = data.weather[0].description;
const icon = data.weather[0].icon;
```

Then, update a section of your HTML to include this data using `innerHTML`:

```js
document.getElementById('weather').innerHTML = `
  <h2>${data.name}</h2>
  <img src="https://openweathermap.org/img/wn/${icon}@2x.png" alt="${description}">
  <p><strong>Condition:</strong> ${description}</p>
  <p><strong>Temperature:</strong> ${temp}&deg; (Feels like ${feels_like}&deg;)</p>
  <p><strong>Humidity:</strong> ${humidity}%</p>
  <p><strong>Pressure:</strong> ${pressure} hPa</p>
  <p><strong>Wind:</strong> ${windSpeed} mph (from ${windDeg}&deg;)</p>
  <p><strong>Cloudiness:</strong> ${cloudiness}%</p>
`;
```

## 🌐 Step 6: Deploy to GitHub Pages

Push your project files to a public GitHub repository.  
Then, go to your repository's **Settings** and scroll to the **Pages** section.  
Choose the `main` branch and the `/ (root)` folder, then save.  
Your site will be published at a GitHub Pages URL.

For help, refer to the [GitHub Pages documentation](https://pages.github.com/).

## 🎯 Result

You now have a live weather application with a map and icon support. It is deployed with a shareable link.

---

© 2025 Valerie Wade. All rights reserved.  
[![License](https://img.icons8.com/?size=45&id=yLuI6PMA_a0O&format=png&color=000000)](https://creativecommons.org/licenses/by-nc-sa/4.0/)  
[![Website](https://img.icons8.com/bubbles/50/000000/web.png)](https://vcwade.com/)  
[![Gmail](https://img.icons8.com/bubbles/50/000000/gmail.png)](mailto:valwade275@gmail.com)  
[![LinkedIn](https://img.icons8.com/bubbles/50/000000/linkedin.png)](https://linkedin.com/in/vcwade)  
[![GitHub](https://img.icons8.com/bubbles/50/000000/github.png)](https://valwade275.github.io/)
