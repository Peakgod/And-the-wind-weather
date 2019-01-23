<template>
  <v-layout>
    <div class="bgi">
    </div>

    <div class="container-bg">
      <div class="container-title">
        <div>当前位置
          <span>
            {{this.location}}
          </span>
        </div>
          <v-btn
            color="info"
            href="/"
          >
            点击这里，返回首页
         </v-btn>
      </div>
      <div class="container-middle">
        <div>更新时间：{{this.dataLoc.loc}}</div>
        <div class="secondLine">
            <span>{{this.weatherData.tmp_min}}~{{this.weatherData.tmp_max}}</span>
            ℃
        </div>
        
        <div class="weather-icon">
          <img :src="imgUrlToday">
          <div>
            <span>日出：</span>
            <span>日落：</span>
          </div>
        </div>

        <div class="weather-three">
          <img src="~/static/select.png"/>
          <span class="margin-span">{{this.weatherData.wind_dir}}<span>&nbsp;&nbsp;&nbsp;</span>{{this.weatherData.wind_sc}}级</span>
          <span class="margin-span">湿度<span>&nbsp;&nbsp;&nbsp;</span>{{this.weatherData.hum}}%</span>
          <span class="margin-span">气压<span>&nbsp;&nbsp;&nbsp;</span>{{this.weatherData.pres}}hPa</span>
        </div>
        <div class="clues">提示语：{{this.lifestyle}}</div>
      </div>
    </div>

    <div class="container-table">
      <span>
        <v-data-table
          :headers="head"
          :items="dessertItem"
          class="elevation-1"
          light
        >
          <template slot="items" slot-scope="props">
            <td class="text-xs-content" >{{ props.item.time }}</td>
            <td class="text-xs-content" >{{ props.item.cond_txt }}</td>
            <td class="text-xs-content" >{{ props.item.tmp }}℃</td>
            <td class="text-xs-content" >{{ props.item.wind_deg }}°</td>
            <td class="text-xs-content" >{{ props.item.wind_dir }}</td>
            <td class="text-xs-content" >{{ props.item.wind_sc }}km/h</td>
            <td class="text-xs-content" >{{ props.item.wind_spd }}km/h</td>
            <td class="text-xs-content" >{{ props.item.hum }}%</td>
            <td class="text-xs-content" >{{ props.item.pres }}pHa</td>
            <td class="text-xs-content" >{{ props.item.pop }}%</td>
            <td class="text-xs-content" >{{ props.item.dew }}℃</td>
            <td class="text-xs-content" >{{ props.item.cloud }}</td>
          </template>
        </v-data-table>
      </span>

      <div class="tables-img">
        <div>
          <v-data-table
            :headers="headers"
            :items="dessert"
            hide-actions
            light
          >
            <template slot="items" slot-scope="props">
              <td>{{ props.item.date }}</td>
              <td>{{ props.item.cond_txt_d }}</td>
              <td>{{ props.item.tmp_max }}</td>
              <td>{{ props.item.tmp_min }}</td>
              <td>{{ props.item.wind_dir }}</td>
              <td>{{ props.item.hum }}</td>
              <td>{{ props.item.pcpn }}</td>
              <td>{{ props.item.pres }}</td>
            </template>
          </v-data-table>
        </div>
        <div class="chartmain">
          <img src="https://api.heweather.net/s6/map/cloudmap?&key=bba03ec977704452bb0fcf9907cb6a82"/>
        </div>
      </div>

      <span>
        <v-data-table
          :headers="header"
          :items="desser"
          class="elevation-1"
          hide-actions
          light
        >
          <template slot="items" slot-scope="props">
            <td class="text-xs-content" >{{ correspond[props.item.type] }}</td>
            <td class="text-xs-content" >{{ props.item.brf }}</td>
            <td class="text-xs-content" >{{ props.item.txt }}</td>
          </template>
        </v-data-table>
      </span>
      
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

      headers: [
        {
          text: '未来七天天气预报',
          sortable: false
        },
        { text: '天气',
          sortable: false },
        { text: '最高气温 ℃',
          sortable: false },
        { text: '最低气温 ℃',
          sortable: false },
        { text: '风向',
          sortable: false },
        { text: '相对湿度 %',
          sortable: false },
        { text: '降水量 ㎡',
          sortable: false },
        { text: '大气压强 kPa',
          sortable: false }
      ],
      dessert: [
        {}
      ],
      head: [
        {
          text: '逐小时预报',
          sortable: false },
        {
          text: '天气状况',
          sortable: false },
        { text: '温度',
          sortable: false },
        { text: '风向360角度',
          sortable: false },
        { text: '风向',
          sortable: false },
        { text: '风力',
          sortable: false },
        { text: '风速，公里/小时',
          sortable: false },
        { text: '相对湿度',
          sortable: false },
        { text: '大气压强',
          sortable: false },
        { text: '降水概率%',
          sortable: false },
        { text: '露点温度',
          sortable: false },
        { text: '云量',
          sortable: false }
      ],
      dessertItem: [
        {}
      ],

      header: [
        {
          text: '类型',
          sortable: false
        },
        { text: '简介',
          sortable: false },
        { text: '详述',
          sortable: false }
      ],
      desser: [
        {
          txt: '',
          brf: '',
          type: ''
        }
      ],

      weatherData: [],
      lifestyle: '',
      daily_forecast: {},
      dataLoc: {},

      correspond: {
        comf: '舒适度指数',
        cw: '洗车指数',
        drsg: '穿衣指数',
        flu: '感冒指数',
        sport: '运动指数',
        trav: '旅游指数',
        uv: '紫外线指数',
        air: '空气污染扩散条件指数',
        ac: '空调开启指数',
        ag: '过敏指数',
        gl: '太阳镜指数',
        mu: '化妆指数',
        airc: '晾晒指数',
        ptfc: '交通指数',
        fsh: '钓鱼指数',
        spi: '防晒指数'
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
      axios.post(`${config.weather}${locationt}${config.key}`)
        .then(response => {
          this.weatherData = response.data.HeWeather6[0].daily_forecast[0]
          this.lifestyle = response.data.HeWeather6[0].lifestyle[0].txt
          this.daily_forecast = response.data.HeWeather6[0].daily_forecast[0].date
          this.dessert = response.data.HeWeather6[0].daily_forecast
          this.dessertItem = response.data.HeWeather6[0].hourly
          this.dataLoc = response.data.HeWeather6[0].update
          this.imgUrlToday = require(`~/assets/inco-weather/${this.weatherData.cond_code_d}.png`)
          this.desser = response.data.HeWeather6[0].lifestyle
        })
        .catch(error => {
          console.log(error)
          alert('请检查您的网络情况！')
        })
    },
    hourWeather () {
      axios.post(`${config.img}${config.key}`)
        .then(response => {
        })
        .catch(error => {
          console.log(error)
          alert('请检查您的网络情况！')
        })
    }
  }
}
</script>


<style scoped lang="less">
  .bgi {
    background-image: url('../static/bgc.png');
    position: fixed;
    height: 500px;
    width: 100%;
  }
    .container-title {
      display: flex;
      flex-flow: row wrap;
      justify-content: space-around;
      line-height: 60px;
      font-size: 18px;
      margin-top: 30px;
      span {
        font-size: 30px;
        margin-left: 15px;
      }
    }
    .container-middle { 
      height: 280px;
      margin-left: 20%;
      margin-top: 20px;
      .secondLine {
        font-size: 40px;
        span{
          font-size: 90px;
        }
      }
      .weather-icon {
        position: absolute;
        top: 120px;
        right: 500px;
        text-align: center;
        img {
          width: 150px;
        }
      }
      .weather-three {
        display: flex;
        align-items: center;
        font-size: 18px;
        img {
          width: 25px;
        }
        .margin-span {
          margin-left: 15px;
        }
      }
      .clues {
        margin-top: 15px;
      }
    }
    .container-bg {
      position:absolute;
      width: 100%;
      z-index: 9;
    }
    .container-table {
      position: absolute;
      top: 400px;
      display: flex;
      flex-flow: row wrap;
      justify-content: center;
      span {
        box-shadow: 2px -1px 8px #5e5d5d;
        width: 80%;
        margin-top: 15px;
      }
    }
    .tables-img {
      display: flex;
      flex-flow: row wrap;
      justify-content: center;
      margin-top: 15px;
      div {
        box-shadow: 2px -1px 8px #5e5d5d;
      }
      .chartmain {
        width: 600px;
        height: 393px;
        margin-left: 40px;
        img {
          width: 600px;
          height: 393px;
        }
      }
    }
    .v-table {
      background-color: #4dd3a6;
    }
</style>
