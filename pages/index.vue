<template>
  <v-layout>
    <div>
      <video class="content-video" autoplay="autoplay" loop="loop">
        <source src="http://cdn.moji.com/websrc/video/winter20181129.mp4" type="video/mp4">
      </video>

      <div class="content-left">
        <p>
          懂天气, 更懂生活!
        </p>
        <span>
          &nbsp;
          Understand the weather, more life!
        </span>
      </div>

      <div class="content-right">
        <div class="content-right-top">
          <div class="content-address" slot="activator" color="primary" dark>
            <img src="~/static/inco-location.png"/>
            <span>{{this.location}}</span>
              <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
              <v-btn slot="activator" color="primary" dark>选择地址</v-btn>
              <v-card>
                <v-toolbar dark color="primary">
                  <v-btn icon dark @click="dialog = false">
                    <v-icon>close</v-icon>
                  </v-btn>
                  <v-toolbar-title>选择地址</v-toolbar-title>
                  <v-spacer></v-spacer>
                  <v-toolbar-items>
                    <v-btn dark flat @click="dialog = false">Save</v-btn>
                  </v-toolbar-items>
                </v-toolbar>
                <v-list three-line subheader>
                  <v-subheader>热门城市</v-subheader>
                  <v-list-tile avatar>
                    <div v-for="(item, index) in hoCity" :key="index">
                      <v-btn v-on:click='selectCityWay(item.location)'>{{item.location}}</v-btn>
                    </div>
                  </v-list-tile>
                </v-list>
                <v-divider></v-divider>
                <v-list three-line subheader>
                  <v-subheader>查询城市</v-subheader>
                    <v-list-tile avatar>
                      <div class="citySearchBtn">
                        <input placeholder="请输入中文城市名查询" v-model="message"/>
                        <v-btn v-on:click="citySearchWay()">查询城市</v-btn>
                      </div>
                    </v-list-tile>
                </v-list> 

                <v-divider></v-divider>
                <v-list three-line subheader>
                  <v-subheader>全国城市</v-subheader>
                    <v-list-tile avatar>
                      <div v-for="(item, index) in citySearchList" :key="index">
                        <v-btn v-on:click='selectCityWay(item.location)'>{{item.location}}</v-btn>
                      </div>
                    </v-list-tile>
                </v-list>

              </v-card>
            </v-dialog>
          </div>

          <div class="content-address-icon">
            温馨提示：{{clues}}
          </div>
        </div>

        <div class="content-right-middle">
          <div class="middle-left middle-style">

            <h3>{{this.weatherDataOne.date}}</h3>
            <img src="~/static/inco-weather/100.png"/>
            <p><span>{{this.weatherDataOne.tmp_min}}</span>℃~<span>{{this.weatherDataOne.tmp_max}}</span>℃</p>
            <div>{{this.weatherDataOne.cond_txt_d}}~{{this.weatherDataOne.cond_txt_n}}</div>

          </div>
          <div class="middle-middle middle-style">

            <h3>{{this.weatherDataTow.date}}</h3>
            <img src="~/static/inco-weather/310.png"/>
            <p><span>{{this.weatherDataTow.tmp_min}}</span>℃~<span>{{this.weatherDataTow.tmp_max}}</span>℃</p>
            <div>{{this.weatherDataTow.cond_txt_d}}~{{this.weatherDataTow.cond_txt_n}}</div>

          </div>
          <div class="middle-right middle-style">

            <h3>{{this.weatherDataThree.date}}</h3>
            <img src="~/static/inco-weather/200.png"/>
            <p><span>{{this.weatherDataThree.tmp_min}}</span>℃~<span>{{this.weatherDataThree.tmp_max}}</span>℃</p>
            <div>{{this.weatherDataThree.cond_txt_d}}~{{this.weatherDataThree.cond_txt_n}}</div>

          </div>
        </div>

        <div class="content-right-btn">
          <v-btn color="#fff" flat nuxt to="/inspire">更多+</v-btn>
        </div>
        
      </div>

      <div id="prompt-r">
        <img src="~/static/tu1.png" class="prompt"/>
        <div class='is-animate style3'>
          <p class="prompt-text">小狐提醒您</p>
          <p class="prompt-text">时刻注意天气哟！</p>
        </div>
      </div>

    </div>
  </v-layout>
</template>

<script>
import axios from 'axios'
// import moment from 'moment'
import config from '~/assets/config.js'
export default {
  data () {
    return {
      clues: '天气变凉注意保暖',
      location: '无锡',
      str: '',

      dialog: false,
      notifications: false,
      sound: true,
      widgets: false,

      hoCity: [],
      citySearchList: [],
      weatherDataOne: [],
      weatherDataTow: [],
      weatherDataThree: [],
      message: ''
    }
  },
  components: {
  },
  mounted () {
    this.hotCitySearchWay()
    this.weatherForecastWay()
  },
  methods: {
    // 热门城市
    hotCitySearchWay () {
      axios.post(`${config.hotCity}${config.group}${config.key}`)
        .then(response => {
          this.hoCity = response.data.HeWeather6[0].basic
        })
        .catch(error => {
          console.log(error)
        })
    },

    // 获取时间(moment)
    // getDate () {
    //   this.today = moment().format('YYYY-' + 'MM-' + 'DD')
    //   this.tomorrow = moment().add(1, 'days').format('YYYY-' + 'MM-' + 'DD')
    //   this.afterTomorrow = moment().add(2, 'days').format('YYYY-' + 'MM-' + 'DD')
    // },

    //  搜索城市
    citySearchWay () {
      let location = `location=${this.message}&`
      axios.get(`${config.searchCity}${location}${config.group}${config.key}`)
        .then(response => {
          this.citySearchList = response.data.HeWeather6[0].basic
        })
        .catch(error => {
          console.log(error)
        })
    },

    // 传值
    selectCityWay (item) {
      this.location = item
      this.dialog = false
      this.weatherForecastWay()
    },
    // 天气预报
    weatherForecastWay () {
      let location = `location=${this.location}&`
      axios.post(`${config.weather}${location}${config.key}`)
        .then(response => {
          console.log(response.data.HeWeather6[0].daily_forecast)
          this.weatherDataOne = response.data.HeWeather6[0].daily_forecast[0]
          this.weatherDataTow = response.data.HeWeather6[0].daily_forecast[1]
          this.weatherDataThree = response.data.HeWeather6[0].daily_forecast[2]
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>
<style scoped lang="less">
  @padding: 0;
  @margin: 0;
  .content-left{
    position: fixed;
    top: 35%;
    left: 27%;
    p {
      font-size: 4.5em;
      font-weight: bold;
      padding: @padding;
      margin: @margin;
    }
    span {
      padding: @padding;
      margin: @margin;
      font-size: 30px;
    }

  }
  .content-video {
    position: fixed;
    width: 100%;
    height: 100%;
    object-fit: cover;
    z-index: -10;
  }
  .content-right {
    position: fixed;
    width: 30%;
    height: 300px;
    top: 80px;
    right: 5%;
    background-color: rgba(143, 143, 143, 0.479);
      .content-right-top {
      padding: 20px 20px 5px;
      display: flex;
      flex-flow: row;
      justify-content: space-around;
      align-items: center;
        .content-address {
          display: flex;
          flex-flow: row;
          justify-content: space-around;
          align-items: center;
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
      }
  }
  .content-right-middle{
    height: 165px;
    margin: 0 60px;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    .middle-style{
      padding: 8px;
      position: relative;
      text-align: center;
      img {
        width: 73%;
      }
      div {
        position: absolute;
        bottom: 0.5%;
        right: 5%;
      }
    }
    .middle-left{
      background-color: rgba(41, 41, 41, 0.6);
    }
    .middle-middle{
      background-color: rgba(41, 41, 41, 0.4);
    }
    .middle-right{
      background-color: rgba(41, 41, 41, 0.3);
    }
  }
  .content-right-btn {
    position: absolute;
    bottom: 3%;
    right: 3%;
  }

  @media all and (-webkit-min-device-pixel-ratio:0) and (min-resolution: .001dpcm) { 
      .content-left{
          background-image: -webkit-linear-gradient(left, rgb(17, 17, 17), rgb(240, 240, 240) 25%, rgb(15, 15, 15) 50%, rgb(248, 248, 248) 75%, rgb(29, 29, 29));
          -webkit-text-fill-color: transparent;
          -webkit-background-clip: text;
          -webkit-background-size: 200% 100%;
          -webkit-animation: content-left-animation 4s infinite linear;
      }
  }
  @-webkit-keyframes content-left-animation {
    100%  { background-position: 0 0;}
    0% { background-position: 100% 0%;}
  }
    
  #prompt-r{
    position: fixed;
    bottom: 10px;
    left: 10px;
  	width:156px;
  	height:156px;
  	margin:50px;
  	background: url('../static/images/foxtail.png') no-repeat 0 0;
    animation:animate-tail 3.75s steps(44) infinite;
    p {
      margin: 0;
      text-align: center;
      position: relative;
      color: rgb(212, 101, 101);
      left: 170px;
    }
  }
  @keyframes animate-tail{
  	0%{background-position:-6864px 0;}
  	100%{background-position:0 0;}
  }
  .prompt {
    position: absolute;
    bottom: 80px;
    left: 160px;
    width: 170px;
  }
  .citySearchBtn {
    input {
      height: 36px;
      border: solid 1px rgb(179, 72, 72);
    }
  }
</style>
