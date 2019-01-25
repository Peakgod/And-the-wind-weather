<template>
  <v-layout>
    <div class="slideshow">
	    <div class="slideshow-image" id="slideshow-image-noe"></div>
	    <div class="slideshow-image" id="slideshow-image-tow"></div>
	    <div class="slideshow-image" id="slideshow-image-three"></div>
	    <div class="slideshow-image" id="slideshow-image-four"></div>
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
          <img :src="imgUrlToday"/>
          <p><span>{{this.weatherDataOne.tmp_min}}</span>℃~<span>{{this.weatherDataOne.tmp_max}}</span>℃</p>
          <div>{{this.weatherDataOne.cond_txt_d}}~{{this.weatherDataOne.cond_txt_n}}</div>
        </div>
        <div class="middle-middle middle-style">
          <h3>{{this.weatherDataTow.date}}</h3>
          <img :src="imgUrlTom"/>
          <p><span>{{this.weatherDataTow.tmp_min}}</span>℃~<span>{{this.weatherDataTow.tmp_max}}</span>℃</p>
          <div>{{this.weatherDataTow.cond_txt_d}}~{{this.weatherDataTow.cond_txt_n}}</div>
        </div>
        <div class="middle-right middle-style">
          <h3>{{this.weatherDataThree.date}}</h3>
          <img :src="imgUrlAft"/>
          <p><span>{{this.weatherDataThree.tmp_min}}</span>℃~<span>{{this.weatherDataThree.tmp_max}}</span>℃</p>
          <div>{{this.weatherDataThree.cond_txt_d}}~{{this.weatherDataThree.cond_txt_n}}</div>
        </div>
      </div>
      <div class="content-right-btn">
        <v-btn color="#fff" flat nuxt><nuxt-link  :to="{name: 'inspire', params: {location: this.location}}">更多+</nuxt-link></v-btn>
      </div>
      
    </div>
<!-- 
    <div id="prompt-r">
      <img src="~/static/tu1.png" class="prompt"/>
      <div class='is-animate style3'>
        <p class="prompt-text">小狐提醒您</p>
        <p class="prompt-text">时刻注意天气哟！</p>
      </div>
    </div> -->

  </v-layout>
</template>

<script>
import axios from 'axios'
import config from '~/assets/config.js'
export default {
  data () {
    return {
      imgUrlToday: '',
      imgUrlTom: '',
      imgUrlAft: '',
      clues: '天气变凉注意保暖',
      location: '无锡',
      str: '',

      dialog: false,
      notifications: false,
      sound: true,
      widgets: false,

      hoCity: [],
      citySearchList: [],
      weatherData: [],
      weatherDataOne: [],
      weatherDataTow: [],
      weatherDataThree: [],
      message: ''
    }
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
    //  搜索城市
    citySearchWay () {
      let location = `location=${this.message}&`
      axios.get(`${config.searchCity}${location}${config.group}${config.key}`)
        .then(response => {
          if (location === '' || response.data.HeWeather6[0].status === 'param invalid' || response.data.HeWeather6[0].status === 'unknown location') {
            alert('未找到地址，请重新输入')
          } else {
            this.citySearchList = response.data.HeWeather6[0].basic
          }
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
          this.weatherData = response.data.HeWeather6[0].daily_forecast
          this.weatherDataOne = this.weatherData[0]
          this.weatherDataTow = this.weatherData[1]
          this.weatherDataThree = this.weatherData[2]
          this.imgUrlToday = require(`~/assets/inco-weather/${this.weatherDataOne.cond_code_d}.png`)
          this.imgUrlTom = require(`~/assets/inco-weather/${this.weatherDataTow.cond_code_d}.png`)
          this.imgUrlAft = require(`~/assets/inco-weather/${this.weatherDataThree.cond_code_d}.png`)
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
  .content-right {
    position: fixed;
    width: 540px;
    height: 300px;
    top: 40px;
    right: 5%;
    z-index: 5;
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
      margin: 8px;
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

  #prompt-r{
    position: fixed;
    bottom: 10px;
    left: 10px;
  	width:156px;
  	height:156px;
    margin:50px;
    z-index: 6;
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
  audio{
    z-index: 5;
    position: absolute;
    bottom: 0;
    opacity: 0.1;
    -webkit-transition: all 2s;
    -moz-transition: all 2s;
    -ms-transition: all 2s;
    -o-transition: all 2s;
    transition: all 2s;
  }
  audio:hover{
    opacity: 1;
  }

  .slideshow {
    position: absolute;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  }
  
  #slideshow-image-noe {
   background-image: url('../static/images/1.jpg')
  }
  #slideshow-image-tow {
    background-image: url('../static/images/2.jpg')
  }
  #slideshow-image-three {
    background-image: url('../static/images/3.jpg')
  }
  #slideshow-image-four {
    background-image: url('../static/images/4.jpg')
  }
  .slideshow-image {
    position: absolute;
    width: 100%;
    height: 100%;
    background: no-repeat 50% 50%;
    background-size: cover;
    -webkit-animation-name: kenburns;
            animation-name: kenburns;
    -webkit-animation-timing-function: linear;
            animation-timing-function: linear;
    -webkit-animation-iteration-count: infinite;
            animation-iteration-count: infinite;
    -webkit-animation-duration: 16s;
            animation-duration: 16s;
    opacity: 1;
    -webkit-transform: scale(1.2);
            transform: scale(1.2);
  }
  .slideshow-image:nth-child(1) {
    -webkit-animation-name: kenburns-1;
            animation-name: kenburns-1;
    z-index: 3;
  }
  .slideshow-image:nth-child(2) {
    -webkit-animation-name: kenburns-2;
            animation-name: kenburns-2;
    z-index: 2;
  }
  .slideshow-image:nth-child(3) {
    -webkit-animation-name: kenburns-3;
            animation-name: kenburns-3;
    z-index: 1;
  }
  .slideshow-image:nth-child(4) {
    -webkit-animation-name: kenburns-4;
            animation-name: kenburns-4;
    z-index: 0;
  }
  
  @-webkit-keyframes kenburns-1 {
    0% {
      opacity: 1;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
    1.5625% {
      opacity: 1;
    }
    23.4375% {
      opacity: 1;
    }
    26.5625% {
      opacity: 0;
      -webkit-transform: scale(1);
              transform: scale(1);
    }
    100% {
      opacity: 0;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
    98.4375% {
      opacity: 0;
      -webkit-transform: scale(1.21176);
              transform: scale(1.21176);
    }
    100% {
      opacity: 1;
    }
  }
  
  @keyframes kenburns-1 {
    0% {
      opacity: 1;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
    1.5625% {
      opacity: 1;
    }
    23.4375% {
      opacity: 1;
    }
    26.5625% {
      opacity: 0;
      -webkit-transform: scale(1);
              transform: scale(1);
    }
    100% {
      opacity: 0;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
    98.4375% {
      opacity: 0;
      -webkit-transform: scale(1.21176);
              transform: scale(1.21176);
    }
    100% {
      opacity: 1;
    }
  }
  @-webkit-keyframes kenburns-2 {
    23.4375% {
      opacity: 1;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
    26.5625% {
      opacity: 1;
    }
    48.4375% {
      opacity: 1;
    }
    51.5625% {
      opacity: 0;
      -webkit-transform: scale(1);
              transform: scale(1);
    }
    100% {
      opacity: 0;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
  }
  @keyframes kenburns-2 {
    23.4375% {
      opacity: 1;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
    26.5625% {
      opacity: 1;
    }
    48.4375% {
      opacity: 1;
    }
    51.5625% {
      opacity: 0;
      -webkit-transform: scale(1);
              transform: scale(1);
    }
    100% {
      opacity: 0;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
  }
  @-webkit-keyframes kenburns-3 {
    48.4375% {
      opacity: 1;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
    51.5625% {
      opacity: 1;
    }
    73.4375% {
      opacity: 1;
    }
    76.5625% {
      opacity: 0;
      -webkit-transform: scale(1);
              transform: scale(1);
    }
    100% {
      opacity: 0;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
  }
  @keyframes kenburns-3 {
    48.4375% {
      opacity: 1;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
    51.5625% {
      opacity: 1;
    }
    73.4375% {
      opacity: 1;
    }
    76.5625% {
      opacity: 0;
      -webkit-transform: scale(1);
              transform: scale(1);
    }
    100% {
      opacity: 0;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
  }
  @-webkit-keyframes kenburns-4 {
    73.4375% {
      opacity: 1;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
    76.5625% {
      opacity: 1;
    }
    98.4375% {
      opacity: 1;
    }
    100% {
      opacity: 0;
      -webkit-transform: scale(1);
              transform: scale(1);
    }
  }
  @keyframes kenburns-4 {
    73.4375% {
      opacity: 1;
      -webkit-transform: scale(1.2);
              transform: scale(1.2);
    }
    76.5625% {
      opacity: 1;
    }
    98.4375% {
      opacity: 1;
    }
    100% {
      opacity: 0;
      -webkit-transform: scale(1);
              transform: scale(1);
    }
  }
  
  
  h1 {
    position: absolute;
    top: 50%;
    left: 50%;
    -webkit-transform: translate3d(-50%, -50%, 0);
            transform: translate3d(-50%, -50%, 0);
    z-index: 99;
    text-align: center;
    font-family: Raleway, sans-serif;
    font-weight: 300;
    text-transform: uppercase;
    background-color: rgba(255, 255, 255, 0.75);
    box-shadow: 0 1em 2em -1em rgba(0, 0, 0, 0.5);
    padding: 1em 2em;
    line-height: 1.5;
  }
  h1 small {
    display: block;
    text-transform: lowercase;
    font-size: .7em;
  }
  h1 small:first-child {
    border-bottom: 1px solid rgba(0, 0, 0, 0.25);
    padding-bottom: .5em;
  }
  h1 small:last-child {
    border-top: 1px solid rgba(0, 0, 0, 0.25);
    padding-top: .5em;
  }
  @media (max-width: 600px) {
    .content-right{
      left: 5%;
      max-width: 540px;
    }
    .content-right
    .content-right-top {
      justify-content: end;
    }
    .content-right-btn{
      top: 6.5%
    }
    .content-address-icon{
      display: none;
    }
    .content-right-middle{
      justify-content: center;
      margin: 0;
      .middle-right{
        display: none;
        width: auto;
        left: 5%;
        right: 5%;
      }
    }
  }
</style>
