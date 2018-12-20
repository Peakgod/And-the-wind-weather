<template>
  <v-layout>
    <div>
      <video autoplay="autoplay" height="100%" width="100%" loop="loop" object-fit="fill">
        <source src="http://cdn.moji.com/websrc/video/winter20181129.mp4" type="video/mp4">
      </video>
      <!-- <div class="content-left">
        <p>
          <pre>
    懂生活
      更懂你
          </pre>
        </p> -->
      <!-- </div> -->
      <div class="content-right">
        <div class="content-right-top">
          <span>地址</span>
          <button v-on:click ='getCurrentWeather()'>查询</button>
          <span>温度</span>
          <span>天气</span>
        </div>
        <div class="content-right-middle">
          <div><p>sada</p></div>
          <div><p>sada</p></div>
          <div><p>sada</p></div>
          <div><p>sada</p></div>
          <div><p>sada</p></div>
          <div><p>sada</p></div>
          <div><p>sada</p></div>
        </div>
        <button>asda</button>
        
      </div>

    </div>
  </v-layout>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      str: ''
    }
  },
  components: {
  },
  mounted () {
    this.getCurrentWeather()
  },
  methods: {
    getCurrentWeather () {
      axios.get('https://search.heweather.net/find?key=bd1e1c4008c547719209ee4c7ca9866c&cityid=CN101010100')
        .then(response => {
          console.log(response)
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>
<style scoped lang="less">
.content-right {
  position: fixed;
  width: 35%;
  height: 300px;
  top: 70px;
  right: 5%;
  background-color: rgba(143, 143, 143, 0.479);
}
.content-right-top{
  padding: 20px;
  display: flex;
  flex-flow: row;
  justify-content: space-around;
}
.content-right-top{
  span{
    background: url('~/static/inco-location.png') no-repeat left center;
    background-color: #6666;
  }
}
.content-right-middle {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
</style>
