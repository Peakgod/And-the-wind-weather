<template>
  <v-container grid-list-md text-xs-center>
    <v-layout row wrap justify-center>
      <v-flex xs12>
        <v-card dark color="lighten-1">
          <div class="content-right-btn">
            <v-btn color="#fff" flat nuxt to="/">返回主页面</v-btn>
          </div>
        </v-card>
      </v-flex>

      <v-flex xs6>
        <v-card dark color="secondary">
          <v-card-text class="px-0">
            
            <div class="content-right-top-left">
              <div class="content-address" slot="activator" color="primary" dark>
                <img src="~/static/inco-location.png"/>
                <span>{{this.location}}</span>
              </div>

              <div class="airQuality">
                <div>
                  <div>空气质量：<span>良</span></div>
                  <div>PM2.5：<span>25</span></div>
                </div>

                <div>
                  <div>降水量<span>{{this.weatherData.pcpn}}</span></div>
                  <div>降水率：<span>{{this.daily_forecast.pop}}%</span></div>
                </div>
              </div>

              <div class="temperature">
                <a><span>{{this.weatherData.tmp}}</span>℃</a>
                <div>
                  <img :src="imgUrlToday"/>
                  <a class="weatherIcon">{{this.weatherData.cond_txt}}天</a>
                </div>
              </div>
      
              <div class="firstRow">
                <div class="humidity">
                  <div>湿度：{{this.weatherData.hum}}</div>
                  <div class="pressure PrecipitationRate">大气压强：{{this.weatherData.pres}}</div>
                </div>
                <div class="windDirection">
                  <div>风向：{{this.weatherData.wind_dir}}东南</div>
                  <div class="windSpeed">风速：{{this.weatherData.wind_spd}}千米每小时</div>
                </div>
              </div>

              <div class="firstRow">
                <div class="humidity">
                  <div>日出</div>
                  <div class="sunrise PrecipitationRate">12：00</div>
                </div>
                <div class="windDirection">
                  <div>日落</div>
                  <div class="windSpeed">16：00</div>
                </div>
              </div>

              <div class="secondRow leftContentLayout">
              </div>
            </div>
          </v-card-text>
        </v-card>
      </v-flex>

      <v-flex xs6>
        <v-card dark color="secondary">
          <v-card-text class="px-0">
            <div class="right-table"> 
              <v-data-table
                :headers="header"
                :items="dessert"
                class="elevation-1"
                hide-actions
              >
                <template slot="items" slot-scope="props">
                  <td>{{ props.item.name }}</td>
                  <td class="text-xs-right">{{ props.item.calories }}</td>
                  <td class="text-xs-right">{{ props.item.fat }}</td>
                  <td class="text-xs-right">{{ props.item.carbs }}</td>
                  <td class="text-xs-right">{{ props.item.protein }}</td>
                  <td class="text-xs-right">{{ props.item.iron }}</td>
                  <td class="text-xs-right">{{ props.item.sss }}</td>
                  <td class="text-xs-right">{{ props.item.ddd }}</td>
                  <td class="text-xs-right">{{ props.item.fff }}</td>
                </template>
              </v-data-table>
            </div>

            <div class="right-table-bottom">
              <v-data-table
                :headers="headers"
                :items="desserts"
                class="elevation-1"
                hide-actions
              >
                <template slot="items" slot-scope="props">
                  <td>{{ props.item.name }}</td>
                  <td class="text-xs-right">{{ props.item.calories }}</td>
                  <td class="text-xs-right">{{ props.item.fat }}</td>
                  <td class="text-xs-right">{{ props.item.carbs }}</td>
                  <td class="text-xs-right">{{ props.item.protein }}</td>
                  <td class="text-xs-right">{{ props.item.iron }}</td>
                </template>
              </v-data-table>
            </div>

          </v-card-text>
        </v-card>
      </v-flex>

    </v-layout>
  </v-container>
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
        { text: '气温',
          sortable: false },
        { text: '风向',
          sortable: false },
        { text: '相对湿度',
          sortable: false },
        { text: '能见度',
          sortable: false }
      ],
      desserts: [
        {
          value: false,
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: '1%'
        }
      ],
      weatherData: [],
      lifestyle: [],
      daily_forecast: [],
      daily_forecasts: []
    }
  },
  mounted () {
    this.weatherForecast()
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
          this.imgUrlToday = require(`~/assets/inco-weather/${this.weatherData.cond_code}.png`)
          console.log(this.WeatherData)
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>


<style scoped lang="less">
  .content-right-btn {
    text-align: initial;
    padding-top: 15px;
    margin-left: 15%;
  }
  .content-right-top-left {
    .airQuality{
      display: flex;
      flex-flow: row wrap;
      justify-content: space-around;
      margin-top: 5%;
      div {
        display: inline;
      }
    }
    .temperature {
      display: flex;
      flex-flow: row wrap;
      justify-content: center;
      margin-bottom: 5%;
      div {
        display: flex;
        align-items: flex-end;
      }
      a {
         font-size: 3em;
      }
      span {
        font-size: 4em;
      }
      .weatherIcon {
        font-size: 18px;
      }
    }
    .firstRow {
      display: flex;
      justify-content: space-around;
      .humidity {
        display: inherit;
      }
      .PrecipitationRate {
        margin-left: 15px;
      }
      .windDirection {
        display: inherit;
        .windSpeed {
          margin-left: 20px;
        }
      }
    }
  }
  .right-table {
    padding: 0 10px;
    height: 190px;
    v-data-table {
      padding: 0 10px;
    }
  }
  .right-table-bottom {
    padding: 0 10px;
    margin-top: 59px;
  }


    .content-right-bottom {
      width: 80%;
      margin-left: 10%;
      margin-top: 15px;
      display: flex;
      flex-flow: row wrap;
      justify-content: space-around;
    }
    .content-address {
      display: flex;
      flex-flow: row;
      align-items: center;
      margin-left: 10%;
      span {
        font-size: 25px;
        margin-right: 5px;
      }
      img {
        margin-right: 5px;
        margin-left: 5px;
        padding: 4px;
        width: 38px;
      }
    }
    .right-form {
      margin-right: 10%;
      margin-left: 10%;
      width: 50%;
    }

</style>
