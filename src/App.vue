<template>
  <img class="horn" src="./assets/horn.png" alt="">
  <div class="container">
    <h1 class="title">we seek for...</h1>
    <div class="input">
      <h5>weather in</h5> <p>:</p>
      <input type="text" ref="inputDOM" v-model="city" @input="catched = false; stopTimeout(); requestTimeout()" placeholder="Enter city">
    </div>

    <DataComp :data="data" :catched="catched"/>

    <img class="wingRight" src="./assets/float.png" alt="">
    <img class="wingLeft" src="./assets/float.png" alt="">
  </div>
  <img class="tail" src="./assets/rabbit-tail.png" alt="">
</template>

<script>
import DataComp from './components/DataComp.vue';

export default {
  components: { DataComp },
  data() {
    return {
      city: '',
      api: '248a090b940a977dc5d798a5dedb301e',
      weather: '',
      data: {},
      catched: false,

      placeholder: 'enter city',
      placeholderError: 'not correct',

      timeoutRequest: null,
      requestDelay: 1500
    }
  },
  methods: {
    async getData() {
      this.$refs.inputDOM.placeholder =  this.placeholder

      let cityName = this.city.replace(' ', '+')

      let response = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${cityName}&appid=${this.api}&units=metric`)

      if (response.ok) {
        let data = await response.json()
        this.catched = true

        let city = {}

        city = { 
          weather: data.weather[0].main,
          temp: data.main.temp,
          feelsLike: data.main.feels_like,
          pressure: data.main.pressure,
          tempMax: data.main.temp_max,
          tempMin: data.main.temp_min 
        }

        this.data = city
      } else if (this.city != '') {
        this.city = ''
        this.$refs.inputDOM.placeholder = this.placeholderError
      }
    },
    requestTimeout() {
      this.timeoutRequest = setTimeout(() => {
        this.getData()
      }, this.requestDelay)
    },
    stopTimeout() {
      clearTimeout(this.timeoutRequest)
    }
  }
}
</script>

<style lang="scss">
$input-text-color:rgb(38, 28, 30);

.horn {
  width: 70px;
  transform: translateY(5px);
}

.wingRight {
  position: absolute;
  width: 150px;
  right: -145px;
  top: 35%;
}

.wingLeft {
  position: absolute;
  transform: scalex(-1);
  width: 150px;
  left: -145px;
  top: 35%;
}

.tail {
  width: 90px;
  transform: translateY(-25px);
}

.container {
  border: 1px solid black;
  border-radius: 40px;
  padding: 40px;
  position: relative;
}

.title {
  text-transform: uppercase;
  font-size: 50px;
}

.input {
  margin-top: 20px;
  display: flex;
  text-align: end;
  align-items: center;
  gap: 5px;
  line-height: 15px;
  font-weight: 500;
  color: $input-text-color;

  input {
    width: 300px;
    background: transparent;
    outline: 0;
    border: 0;
    text-transform: uppercase;
    font-size: 40px;
    font-weight: 700;
    font-family: 'Times New Roman', Times, serif;
    color: $input-text-color;
    text-decoration: underline;
    text-align: end;
  }
  
  input::placeholder {
    font-weight: 400;
    opacity: 1;
    color: rgb(85, 64, 68);
    text-decoration: underline;
  }

  h5 {
    font-size: 25px;
    font-weight: 500;
    color: $input-text-color;
  }

  p {
    font-size: 35px;
  }

  button {
    background: transparent;
    border: 1px solid black;
    outline: 0;
    padding: 20px;
    cursor: pointer;

    &:hover {
      transform: scale(1.05);
    }
  }
}
</style>