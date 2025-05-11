<script setup>
import { ref } from "vue";

// Replace with your actual OpenWeatherMap API key
const apiKey = "7171f1bf3d1cc83378f7d2b2f5bf48a4";
const city = ref("");
const weatherData = ref(null);
const error = ref(null);
const isLoading = ref(false);

const fetchWeather = async () => {
    if (!city.value) {
        error.value = "Please enter a city name.";
        weatherData.value = null;
        return;
    }

    isLoading.value = true;
    error.value = null;
    weatherData.value = null; // Clear previous data

    const url = `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&appid=${apiKey}&units=metric`; // Use units=imperial for Fahrenheit

    try {
        const response = await fetch(url);
        if (!response.ok) {
            // Handle HTTP errors
            if (response.status === 404) {
                throw new Error("City not found.");
            }
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json();
        weatherData.value = data;
        console.log("Weather Data:", data); // Log data to console for inspection
    } catch (err) {
        error.value = err.message || "Failed to fetch weather data.";
        console.error("Fetch Error:", err);
    } finally {
        isLoading.value = false;
    }
};

// Helper function to get weather icon URL
const getWeatherIcon = (iconCode) => {
    if (!iconCode) return "";
    return `https://openweathermap.org/img/w/${iconCode}.png`;
};

// Helper function to capitalize the first letter of a string
const capitalizeFirstLetter = (string) => {
    if (!string) return "";
    return string.charAt(0).toUpperCase() + string.slice(1);
};
</script>

<template>
    <div
        class="container mx-auto p-4 max-w-sm bg-gradient-to-br from-blue-400 to-blue-600 rounded-lg shadow-xl text-white"
    >
        <h1 class="text-2xl font-bold mb-4 text-center">Weather App</h1>

        <div class="flex items-center mb-4">
            <input
                type="text"
                v-model="city"
                @keyup.enter="fetchWeather"
                placeholder="Enter city name"
                class="flex-grow p-2 rounded-l-md border-none focus:outline-none text-gray-800"
            />
            <button
                @click="fetchWeather"
                :disabled="isLoading"
                class="bg-blue-700 hover:bg-blue-800 text-white p-2 rounded-r-md transition duration-300 ease-in-out disabled:opacity-50 disabled:cursor-not-allowed"
            >
                {{ isLoading ? "Loading..." : "Get Weather" }}
            </button>
        </div>

        <div v-if="isLoading" class="text-center">Loading...</div>

        <div v-if="error" class="text-red-200 text-center mb-4">
            {{ error }}
        </div>

        <div v-if="weatherData" class="weather-info text-center">
            <h2 class="text-3xl font-semibold mb-2">{{ weatherData.name }}</h2>
            <div class="flex justify-center items-center mb-2">
                <img
                    v-if="weatherData.weather[0].icon"
                    :src="getWeatherIcon(weatherData.weather[0].icon)"
                    :alt="weatherData.weather[0].description"
                    class="w-16 h-16"
                />
                <p class="text-5xl font-bold">
                    {{ Math.round(weatherData.main.temp) }}°C
                </p>
            </div>
            <p class="text-xl mb-2">
                {{ capitalizeFirstLetter(weatherData.weather[0].description) }}
            </p>
            <div class="grid grid-cols-2 gap-2 text-left text-sm">
                <p>
                    <strong>Feels like:</strong>
                    {{ Math.round(weatherData.main.feels_like) }}°C
                </p>
                <p>
                    <strong>Humidity:</strong> {{ weatherData.main.humidity }}%
                </p>
                <p>
                    <strong>Wind:</strong>
                    {{ Math.round(weatherData.wind.speed * 3.6) }} km/h
                </p>
                <p>
                    <strong>Pressure:</strong>
                    {{ weatherData.main.pressure }} hPa
                </p>
            </div>
        </div>
    </div>
</template>

<style scoped>
/* Add any component-specific styles here if needed,
   but Tailwind utility classes are used for most styling. */
</style>
