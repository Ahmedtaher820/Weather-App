<template>
  <div id="app">
    <div class="input-box">
      <input
        type="text"
        class="input-field"
        placeholder="Serach..."
        v-model="query"
        @keypress="fetchweather"
      />
    </div>
    <div class="weather-box" v-if="typeof weather.main !='undefined'">
      <div class="weather-content">
        <h3>{{weather.name}},{{weather.sys.country}}</h3>
        <span class="date">{{ date() }}</span>
      </div>
      <div class="weather-degree">
        <span class="degree">{{Math.round(weather.main.temp)}}°c</span>
      </div>
      <div class="weather-state">
        <span>{{weather.weather[0].main}}</span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      apiKey: "c578cc36cbec850fbfa17598355a74c9",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    date() {
      const nowDate = new Date();
      const mm = nowDate.getMonth();
      const yy = nowDate.getFullYear();
      const dd = nowDate.getDay();
      const day = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      const Month = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      return `${day[dd]} ${dd} ${Month[mm]} ${yy}`;
    },
    fetchweather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.apiKey}`
        )
          .then((resolve) => {
            return resolve.json();
          })
          .then((result) => {
            this.weather = result;
            console.log(this.weather);
          });
      }
    },
  },
  created() {},
};
</script>
<style>
* {
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
}
#app {
  background-image: url("./assets/wallpapersden.com_mountains-in-clouds.jpg");
  background-size: cover;
  background-position: center;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.input-box {
  padding: 20px;
}
.input-box input {
  width: 380px;
  padding: 15px;
  border: none;
  outline: none;
  -webkit-appearance: none;
  font-size: 17px;
  background-color: rgba(255, 255, 255, 0.739);
  border-radius: 16px 0px 16px 0px;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  transition: 0.4s;
}
.input-box input:focus {
  background-color: rgba(255, 255, 255, 0.8);
  border-radius: 0px 16px 0px 16px;
}
.weather-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;
  text-align: center;
}
.weather-box .weather-content h3 {
  font-size: 32px;
  box-shadow: 1px 3px rgba(0, 0, 0, 0.15);
  font-weight: 600;
}
.weather-content span.date {
  font-style: italic;
  font-weight: 300;
  font-size: 24px;
  display: block;
  margin: 10px 0px;
}
.weather-box .weather-degree {
  padding: 15px;
  background-color: rgba(255, 255, 255, 0.349);
  border-radius: 16px;
  transition: 0.4s;
}
.weather-box .weather-degree:hover {
  background-color: rgba(255, 255, 255, 0.5);
}
.weather-box .weather-degree span.degree {
  font-size: 80px;
  font-weight: 900;
  margin: 30px 0px;
}
.weather-box .weather-state span {
  font-weight: 600;
  font-size: 48px;
  text-transform: capitalize;
  margin-top: 10px;
  display: block;
}
</style>
