<script>
import axios from 'axios'
export default {
  data(){
    return {
      city:"",
      error:"",
      info:null
    }
  },
  methods:{
    getWeather(){
      if (this.city.trim().length<2){
        this.error="The city name cannot be less than 2 characters."
        return false
      }
      this.error=""

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=3d9de74844d28377e81415151cbe6a66`)
          .then(res=>(this.info = res.data))
    }
  },
  computed:{
    temperature(){
      return this.info.main.temp + "°C"
    },
    minTemperature(){
      return this.info.main.temp_min + "°C"
    },
    maxTemperature(){
      return this.info.main.temp_max + "°C"
    },
    feelsLike(){
      return this.info.main.feels_like +"°C"
    }
  }
}


</script>

<template>
  <div class="wrapper">
    <h1 class="title">Weather app</h1>
    <p class="city">Find out the weather in {{city === "" ? "..." : city}}</p>
    <input type="text" placeholder="Enter city name" v-model="city"/>
    <button v-if="city !== '' " @click="getWeather()">Get the weather</button>
    <button disabled v-else>Enter the city name</button>
    <p class="error">{{error}}</p>

    <div class="info" v-if="info != null">
      <p>Temperature: {{temperature}}</p>
      <p>Feels like: {{feelsLike}}</p>
      <p>Minimal temperature today: {{minTemperature}}</p>
      <p>Maximum temperature today: {{maxTemperature}}</p>
    </div>
  </div>

</template>

<style scoped>
.wrapper{
  @import url('https://fonts.googleapis.com/css2?family=M+PLUS+Rounded+1c:wght@100;300;400;500;700;800;900&display=swap');
  font-family: "M PLUS Rounded 1c", sans-serif;
  font-style: normal;
  font-weight: 300;
  border-radius: 40px;
  border: #001A29 solid 7px;
  color: white;
  display: flex;
  flex-direction: column;
  background: #002C4A;
  width: 900px;
  height: 500px;
  align-items: center;
  padding: 40px;
}
.wrapper h1{
  margin-bottom: 10px;
  font-size: 40px;
}
.city{
  font-size: 20px;
}
.wrapper input{
  margin: 50px 0 20px 0;
  font-family: "M PLUS Rounded 1c", sans-serif;
  font-style: normal;
  font-weight: 300;
  font-size: 16px;
  border-radius: 25px;
  width: 70%;
  height: 20px;
  outline: none;
  border: none;
  padding: 15px;
}
.wrapper button{
  cursor: pointer;
  font-family: "M PLUS Rounded 1c", sans-serif;
  font-style: normal;
  font-weight: 300;
  border: none;
  outline: none;
  background: RGBA(179, 233, 255, 1);
  width: 19.5%;
  height: 40px;
  border-radius: 12px;
  transition: transform 500ms ease;
}
.wrapper button:hover{
  transform: scale(1.1);
}
.wrapper button:disabled{
  font-family: "M PLUS Rounded 1c", sans-serif;
  font-style: normal;
  font-weight: 300;
  cursor: not-allowed;
  color: black;
}
.error{
  margin-top: 10px;
  color: #d03939;
  font-size: 15px;
}
.info{
  border: #001A29 solid 3px;
  padding: 10px;
  border-radius: 10px;
  color: black;
  background: RGBA(179, 233, 255, 1);
  font-size: 18px;
  margin-top: 30px;
  display: flex;
  flex-direction: column;

}
</style>
