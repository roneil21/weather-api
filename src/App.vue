<template>
  <div id="app" :class="(typeof weather.main != 'undefined' && weather.main.temp > 30 ? 'warm' : '')">
    <main>
      <div class="search-cont">
        <input type="text" class="search-bar" placeholder="Search a City" v-model="query" @keyup.enter="getWeather" />
      </div>

      <div class="weather-wrap" v-if="(typeof weather.main != 'undefined')">
        <div class="location-cont">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">
            {{ currentDate() }}
          </div>
        </div>
        <div class="weather-cont">
          <div :class="weather.main.temp > 30 ? 'warm-temp' : 'temp'">{{ Math.round(weather.main.temp) }}°C</div>
          <div class="status">{{ weather.weather[0].description }}</div>
        </div>
      </div>
      <footer>Made by: Roneil Algara</footer>
    </main>

  </div>
</template>

<script>


export default {
  name: 'App',

  data() {
    return {
      API_KEY: 'a01620eaf5abbff0d421cf07d4a6b419',
      url: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    getWeather() {
      fetch(`${this.url}weather?q=${this.query}&units=metric&appid=${this.API_KEY}`)
        .then(res => {
          return res.json()
        })
        .then(this.setResults)
    },
    setResults(results) {
      this.weather = results
    },
    currentDate() {
      const date = new Date();

      const options = {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric',
      };
      return date.toLocaleString('en-IN', options)
    }

  }

}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}

#app {
  background-image: url('./assets/cold.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.3s;
}

#app.warm {
  background-image: url('./assets/hot.jpg');
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.location-cont .location {
  margin-top: 50px;
  color: #fff;
  font-size: 32px;
  font-weight: 600;
  text-align: center;
  text-shadow: 2px 3px rgba(0, 0, 0, 0.25);
}

.location-cont .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-cont {
  text-align: center;
}

.weather-cont .temp {
  display: inline-block;
  padding: 10px 25px;
  color: rgb(0, 123, 255);
  font-size: 102px;
  font-weight: 800;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 18px;
  margin: 30px 0;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  ;
}

.warm-temp {
  display: inline-block;
  padding: 10px 25px;
  color: red;
  font-size: 102px;
  font-weight: 800;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 18px;
  margin: 30px 0;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  ;

}

.weather-cont .status {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.date.search-cont {
  width: 100%;
  margin-bottom: 30px;
}

.search-cont .search-bar {

  display: flex;
  position: relative;
  text-align: center;
  left: 40%;
  width: 300px;



  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 18px;
  transition: 0.4s;
}

.search-cont .search-bar:focus {
  box-shadow: 0 0 16px rgba(0, 0, 0, 0.5);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 18px 0px;
}

footer {
  color: #fff;
  position: absolute;
  bottom: 0;
  left: 45%;
  height: 40px;
  margin-top: 700px;

}
</style>
