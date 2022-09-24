<template >
    <div class="search-box">
    <input type="text" class="search-input" placeholder="Search..." @keypress.enter="fetchWeather" v-model="query" />
  </div>
  <div class="weather-display" v-if="typeof weather.main !='undefined'">
    <div class="country">{{weather.name}}, {{weather.sys.country}}</div>
    <div class="date">
      {{dateBuilder()}}
    </div>
    <div class="display">
      <div class="temp">
        {{Math.round(weather.main.temp)}}°C
      </div>
      <div class="weather">
        {{weather.weather[0].main}}
      </div>
    </div>
  </div>
  
  
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "1e7a86750c78d7bf2c4e07cbe26836ac",
      url:"https://api.openweathermap.org/data/2.5/",
      query:'',
      weather: {}
    };
  },
  methods:{
    fetchWeather(){
      fetch(`${this.url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
      .then(response=>{ 
        return response.json();
      }
      
      ).then(response=>{

        this.weather = response
      }
      )
    },
    dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      
      return `${day} ${date} ${month} ${year}`;
    }

  }
};
</script>

<style>
body {
  margin: 0;
  padding: o;
}
#app {
  background-image: url("./assets/cold.jpg");
  height: 100vh;
}
#app .warm {
  background-image: url("./assets/hot.jpg");
  height: 100vh;
}
.search-box{
  padding: 16px 25px 16px 25px;
   
}
.search-box .search-input{
  border: none;
  background: none;
  color:rgb(205, 199, 199);
  outline: none;
  font-size: 20px;

  background-color:rgba(255, 255, 255, 0.696);
  width: 100%;
  padding: 16px;
  border-radius: 0px 16px 0px 16px;
  box-shadow: 0px 0 5px rgba(53, 52, 52, 0.5);
}
.search-box .search-input:focus{
  border-radius: 16px 0px 16px 0px;
  background-color:rgba(255, 255, 255, 1);
}
.weather-display .country{
  text-align: center;
  color: white;
  font-size: 25px;
  font-weight: 500;
  

  text-shadow: 1px 1px rgba(255, 255, 255, 0.696);
}
.weather-display .date{
  text-align: center;
  color: rgb(189, 189, 189);
  font-size: 18px;
  font-weight: 400;
  padding: 10px;
  font-style: italic;
}
.display{
  text-align: center;
}
.display .temp{
  display: inline-block;
  color: white;
  background: rgb(210, 208, 208);
  padding: 15px 25px;
  font-weight: 900;
  font-size: 80px;
  border-radius: 16px ;
}
.display .weather{

  color: white;
  padding: 15px 25px;
  font-weight: 700;
  font-size: 50px;
  font-style: italic;

}
</style>
