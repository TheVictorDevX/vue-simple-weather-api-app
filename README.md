# Vue Simple Weather App ✨

A simple, responsive weather application built with Vue 3 Composition API and Tailwind CSS, fetching data from the OpenWeatherMap API. ☀️☁️☔

## Project Description

This project is a basic single-page application that allows users to get current weather information for a specified city. It demonstrates the use of Vue 3's Composition API for state management and logic, and Tailwind CSS for a clean and responsive user interface. Weather data is fetched from the OpenWeatherMap API.

## Features 🚀

* Fetch current weather data by city name.
* Display temperature, weather description, "feels like" temperature, humidity, wind speed, and pressure.🌡️💧🌬️
* Show a weather icon based on the current conditions. 🖼️
* Responsive design using Tailwind CSS.📱💻

## Technologies Used 🛠️

* Vue 3 (with Composition API)
* Tailwind CSS
* OpenWeatherMap API

## Setup and Installation ⚙️

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/TheVictorDevX/vue-simple-weather-api-app.git](https://github.com/TheVictorDevX/vue-simple-weather-api-app.git)
    ```
2.  **Navigate to the project directory:**
    ```bash
    cd vue-simple-weather-api-app
    ```
3.  **Install dependencies:**
    ```bash
    npm install
    ```
    ```bash
    # or using yarn
    # yarn install
    ```
4.  **Get an OpenWeatherMap API Key:**
    Sign up for a free API key at [https://openweathermap.org/api](https://openweathermap.openweathermap.org/api). 🔑
5.  **Add your API Key:**
    Open the `WeatherApp.vue` file (or wherever you placed the component) and replace `'YOUR_API_KEY'` with your actual OpenWeatherMap API key:
    ```javascript
    const apiKey = 'YOUR_API_KEY'; // Replace with your API key
    ```
    *Note: For a production application, it's recommended to use environment variables to manage API keys.* 🔒
6.  **Run the development server:**
    ```bash
    npm run dev
    ```
    ```bash
    # or using yarn
    # yarn dev
    ```
    The app should now be running locally, usually at `http://localhost:5173/` (or a similar address).

## Usage 🖱️

1.  Enter the name of a city in the input field. 🏙️
2.  Click the "Get Weather" button or press Enter.
3.  The weather information for the city will be displayed below. 👇

## License 📄

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details. ❤️
