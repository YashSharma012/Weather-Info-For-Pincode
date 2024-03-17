# Weather Info Backend 

## Overview:
This project implements a REST API to retrieve weather information for a specific pincode and date. The retrieved data is stored in a relational database for optimized future API calls. Additionally, caching using Redis is implemented to enhance performance.

## Endpoints:
- **GET /weather:** 
  - Parameters:
    - `pincode`: The pincode for the location.
    - `date`: The date for which weather information is requested.
  - Returns: Weather information for the specified pincode and date.

## Data Storage:

1. **Pincode Lat-Long:**
Pincode and its corresponding latitude-longitude coordinates are saved separately in a relational database. This information allows for efficient retrieval of weather data based on pincode.

2. **Weather Information:**
Weather information for each pincode and date is stored in the relational database. This data includes temperature, humidity, weather condition, etc. Storing this information enables quick access to historical weather data.

3. **Caching with Redis:**
Redis is utilized for caching weather information to optimize future API calls. Cached data includes weather information for specific pincode-date combinations. Redis caching improves response time by eliminating the need to fetch data from the database repeatedly.



## API Call Optimization:
1. Convert pincode to lat-long using OpenWeather Geocoding API.
2. Fetch weather information based on lat-long using the OpenWeather API.
3. Cache weather data using Redis for optimized subsequent API calls.

## Project Structure:
- **Controller:**
  - `WeatherController`: Handles HTTP requests and delegates to the service layer.
- **Service:**
  - `WeatherService`: Business logic for fetching weather information.
- **Repository:**
  - `LatLonRepository`: Interface for CRUD operations on pincode lat-long data.
  - `WeatherDataRepository`: Interface for CRUD operations on weather information.
  - `CacheRepository`: Interface for caching weather data using Redis.
- **Model:**
  - `LatLonData`: Entity to store pincode and its corresponding lat-long.
  - `WeatherData`: Entity to store weather information.
- **Config:**
  - `WeatherApiClient`: Configuration for accessing external weather APIs.
  - `RedisConfig`: Configuration for Redis connection and template setup.

## Testing:
- Used JUnit and Mockito for unit testing.

## Setup Instructions:
1. Clone the repository from GitHub.
2. Set up the database configurations in `application.properties`.

 **Ensure the following properties are configured in the `application.properties` file of your Spring Boot application:**
```properties
spring.datasource.username= DB_USERNAME
spring.datasource.password= DB_PASSWORD

openweathermap.api.key= OPENWEATHER_API_KEY

# Redis Configuration
redis.host.url= REDIS_URL
redis.host.port= REDIS_PORT
redis.host.password= REDIS_PASSWORD
```
3. Install any required dependencies specified in the `pom.xml`.
4. Build and run the application.

## Usage:
1. Make a GET request to `/weather` endpoint with `pincode` and `date` parameters.
2. Receive weather information in the response.

## Sample Request:
http://localhost:8080/weather?pincode=411014&date=2024-03-17

## Sample Response:
```json
{
    "name": "Viman Nagar",
    "date": "2024-03-17",
    "main": {
        "temp": 33.98001,
        "temp_min": 33.98001,
        "temp_max": 33.98001,
        "pressure": 1011,
        "humidity": 18
    },
    "weather": [
        {
            "main": "Clear",
            "description": "clear sky",
            "icon": "01d"
        }
    ],
    "wind": {
        "speed": 1.12,
        "deg": 175,
        "gust": 4.55
    }
}
```
## Contact
For any inquiries or issues, please contact yashsh662@gmail.com .


