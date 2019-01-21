<template>
  <v-layout>
    <div>
      <div id="background" class="wall"></div>
      <div id="midground" class="wall"></div>
      <div id="foreground" class="wall"></div>
      <div id="top" class="wall"></div>
    </div>
    <div class="container">
      <div class="container-title">
        <div>小狐天气</div>
        <div>返回首页</div>
      </div>
      <div class="container-middle">
        <div>form</div>
        <div>img</div>
      </div>
    </div>
  </v-layout>
</template>

<script>
import axios from 'axios'
import config from '~/assets/config.js'
export default {
  data () {
    return {
      imgUrlToday: '',
      dialog: false,
      notifications: false,
      sound: true,
      widgets: false,
      location: '无锡',
      header: [
        {
          text: '逐小时天气',
          sortable: false
        },
        { text: '01:00',
          sortable: false },
        { text: '04:00',
          sortable: false },
        { text: '07:00',
          sortable: false },
        { text: '10:00',
          sortable: false },
        { text: '13:00',
          sortable: false },
        { text: '16:00',
          sortable: false },
        { text: '19:00',
          sortable: false },
        { text: '22:00',
          sortable: false }
      ],
      dessert: [
        {
          value: false,
          name: '天气状况',
          calories: '晴',
          fat: '晴',
          carbs: '晴',
          protein: '晴',
          iron: '晴',
          sss: '晴',
          ddd: '晴',
          fff: '晴'
        },
        {
          value: false,
          name: '温度',
          calories: 215,
          fat: 215,
          carbs: 215,
          protein: 215,
          iron: 215,
          sss: 215,
          ddd: 215,
          fff: 215
        },
        {
          value: false,
          name: '相对湿度',
          calories: 10,
          fat: 10,
          carbs: 10,
          protein: 10,
          iron: 10,
          sss: 10,
          ddd: 10,
          fff: 10
        }
      ],
      headers: [
        {
          text: '未来三天天气预报',
          sortable: false
        },
        { text: '天气',
          sortable: false },
        { text: '最高气温',
          sortable: false },
        { text: '最低气温',
          sortable: false },
        { text: '风向',
          sortable: false },
        { text: '相对湿度',
          sortable: false },
        { text: '降水量',
          sortable: false }
      ],
      desserts: [
        {
          value: false,
          cond_txt_d: '晴',
          date: '2019.01.04',
          tmp_max: 0,
          tmp_min: 0,
          wind_dir: 0,
          pcpn: 0,
          hum: 0,
          vis: 0
        }
      ],
      head: [
        {
          text: '生活指数',
          sortable: false },
        { text: '等级',
          sortable: false },
        { text: '温馨提示',
          sortable: false }
      ],
      content: [
        {
          txt: '',
          brf: '',
          type: ''
        }
      ],
      weatherData: [],
      lifestyle: [],
      daily_forecast: [],
      daily_forecasts: [],

      correspond: {
        comf: '舒适度指数',
        cw: '洗车指数',
        drsg: '穿衣指数',
        flu: '感冒指数',
        sport: '运动指数',
        trav: '旅游指数',
        uv: '紫外线指数',
        air: '空气污染扩散条件指数'
      }
    }
  },
  mounted () {
    this.weatherForecast()
    this.hourWeather()
  },
  methods: {
    // 默认的天气
    weatherForecast () {
      if (this.$route.params.location === undefined) {
        this.location = this.location
      } else {
        this.location = this.$route.params.location
      }
      let locationt = `location=${this.location}&`
      axios.post(`${config.weatherLive}${locationt}${config.key}`)
        .then(response => {
          this.weatherData = response.data.HeWeather6[0].now
          this.lifestyle = response.data.HeWeather6[0].lifestyle
          this.daily_forecast = response.data.HeWeather6[0].daily_forecast[0]
          this.daily_forecasts = response.data.HeWeather6[0].daily_forecast
          this.desserts = this.daily_forecasts
          this.content = response.data.HeWeather6[0].lifestyle
          this.imgUrlToday = require(`~/assets/inco-weather/${this.weatherData.cond_code}.png`)
        })
        .catch(error => {
          console.log(error)
          alert('请检查您的网络情况！sssdadadad')
        })
    },
    hourWeather () {
      if (this.$route.params.location === undefined) {
        this.location = this.location
      } else {
        this.location = this.$route.params.location
      }
      let locationt = `location=${this.location}&`
      axios.post(`${config.hourWeather}${locationt}${config.key}`)
        .then(response => {
          console.log(response)
        })
        .catch(error => {
          console.log(error)
          // alert('请检查您的网络情况！wwwwwwwwwwwwwwwwww')
        })
    }
  }
}
</script>


<style scoped lang="less">
  .wall{
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
  }
    #background{
      background: url("../static/images/preview.jpg")no-repeat;
      -webkit-animation: dd 100s linear infinite;
      -moz-animation: dd 100s linear infinite;
      -o-animation: dd 100s linear infinite;
      animation: dd 100s linear infinite;
      background-size: cover;
  }
  #midground{
      background: url("../static/images/midground.png");
      z-index: 1;
      -webkit-animation: cc 100s linear infinite;
      -moz-animation: cc 100s linear infinite;
      -o-animation: cc 100s linear infinite;
      animation: cc 100s linear infinite;
  }
  #foreground{
      background: url("../static/images/foreground.png");
      z-index: 2;
      -webkit-animation: cc 153s linear infinite;
      -o-animation: cc 153s linear infinite;
      -moz-animation: cc 153s linear infinite;
      animation: cc 153s linear infinite;
  }
  #top{
      background-image: url("../static/images/midground.png");
      z-index: 4;
      -webkit-animation: dd 100s linear infinite;
      -o-animation: dd 100s linear infinite;
      animation: da 100s linear infinite;
  }
  @-webkit-keyframes cc {
      from{
          background-position: 0 0;
          transform: translateY(10px);
      }
      to{
          background-position: 600% 0;
      }
  }
  @-o-keyframes cc {
      from{
          background-position: 0 0;
          transform: translateY(10px);
      }
      to{
          background-position: 600% 0;
      }
  }
  @-moz-keyframes cc {
      from{
          background-position: 0 0;
          transform: translateY(10px);
      }
      to{
          background-position: 600% 0;
      }
  }
  @keyframes cc {
      0%{
          background-position: 0 0;
      }
      100%{
          background-position: 600% 0;
      }
  }
  
  @keyframes da {
      0%{
          background-position: 0 0;
      }
      100%{
          background-position: 0 600%;
      }
  }
  @-webkit-keyframes da {
      0%{
          background-position: 0 0;
      }
      100%{
          background-position: 0 600%;
      }
  }
  @-moz-keyframes da {
      0%{
          background-position: 0 0;
      }
      100%{
          background-position: 0 600%;
      }
  }
  @-ms-keyframes da {
      0%{
          background-position: 0 0;
      }
      100%{
          background-position: 0 600%;
      }
  }
  .container {
    background-image: url('../static/bgc.png');
    z-index: 7;
    height: 380px;
    opacity: 0.7;
    .container-title {
      display: flex;
      flex-flow: row wrap;
      justify-content: space-around;
      line-height: 60px;
    }
    .container-middle {
      display: flex;
      flex-flow: row wrap;
      justify-content: space-around;
      text-align: center;
      height: 280px;
    }
  }
</style>
