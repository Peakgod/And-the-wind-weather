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
          <div class="content-address" v-on:click ='getCurrentWeather()'>
            <img src="~/static/inco-location.png"/>
          <span>地址</span>
          </div>

          <div class="content-address-icon">
            温馨提示：{{clues}}
          </div>
        </div>

        <div class="content-right-middle">
          <div class="middle-left middle-style">

            <h3>{{today}}</h3>
            <img src="~/static/inco-weather/100.png"/>
            <p><span>摄氏度</span>℃</p>
            <div>晴天</div>

          </div>
          <div class="middle-middle middle-style">

            <h3>{{tomorrow}}</h3>
            <img src="~/static/inco-weather/310.png"/>
            <p><span>摄氏度</span>℃</p>
            <div>雨天</div>

          </div>
          <div class="middle-right middle-style">

            <h3>{{afterTomorrow}}</h3>
            <img src="~/static/inco-weather/200.png"/>
            <p><span>摄氏度</span>℃</p>
            <div>有风</div>

          </div>
        </div>

        <div class="content-right-btn">
          <v-btn color="#fff" flat nuxt to="/inspire">更多+</v-btn>
        </div>
        
      </div>
    </div>
  </v-layout>
</template>

<script>
import axios from 'axios'
import moment from 'moment'
export default {
  data () {
    return {
      clues: '天气变凉注意保暖',
      str: '',
      today: '',
      tomorrow: '',
      afterTomorrow: ''
    }
  },
  components: {
  },
  mounted () {
    this.getCurrentWeather()
    this.getDate()
  },
  methods: {
    getCurrentWeather () {
      axios.get('http://zhwnlapi.etouch.cn/Ecalender/api/v2/weather?date=20160105&citykey=101010100')
        .then(response => {
          console.log(response)
        })
        .catch(error => {
          console.log(error)
        })
    },

    // 获取时间(moment)
    getDate () {
      this.today = moment().format('YYYY-' + 'MM-' + 'DD')
      this.tomorrow = moment().add(1, 'days').format('YYYY-' + 'MM-' + 'DD')
      this.afterTomorrow = moment().add(2, 'days').format('YYYY-' + 'MM-' + 'DD')
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
  }
  .content-right {
    position: fixed;
    width: 30%;
    height: 300px;
    top: 80px;
    right: 5%;
    background-color: rgba(143, 143, 143, 0.479);
      .content-right-top {
      padding: 20px;
      display: flex;
      flex-flow: row;
      justify-content: space-around;
      align-items: center;
        .content-address {
          cursor: pointer;
          display: flex;
          flex-flow: row;
          justify-content: space-around;
          align-items: center;
          span {
            margin-right: 5px;
          }
          img {
            margin-right: 5px;
            margin-left: 5px;
            padding: 4px;
            width: 35px;
          }
        }
        .content-address:hover {
          width: 90px;
          border-radius: 20px;
          background-color: rgba(63, 63, 63, 0.616);
        }
      }
  }
  .content-right-middle{
    height: 160px;
    margin: 0 60px;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    .middle-style{
      padding: 8px;
      position: relative;
      text-align: center;
      img {
        width: 80%;
      }
      div {
        position: absolute;
        bottom: 3%;
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
          background-image: -webkit-linear-gradient(left, rgb(54, 54, 54), rgb(209, 209, 205) 25%, rgb(52, 54, 54) 50%, rgb(216, 216, 216) 75%, rgb(54, 54, 54));
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
</style>
