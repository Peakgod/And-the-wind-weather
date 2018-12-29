<template>
  <v-layout class="container">
    <div class="container-content">
      <div class="content-right-btn">
        <v-btn color="#fff" flat nuxt to="/">返回主页面</v-btn>
      </div>
      
      <div class="content-right-top">
        <div class="content-right-top-left">
           <div class="content-address" slot="activator" color="primary" dark>
             <img src="~/static/inco-location.png"/>
             <span>{{this.location}}dasdadd</span>
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

           <div class="airQuality leftContentLayout">
             <div>空气质量：<span>良</span></div>
             <div>PM2.5：<span>25</span></div>
           </div>

           <div class="leftContentLayout">
             <div class="temperature">
               <a><span>sd</span>℃</a>
               <p>体感温度:  ℃</p>
             </div>

             <div class="temperature-right">
               <div></div>
                <img src="~/assets/inco-weather/100.png"/>
                <span>晴天</span>
             </div>
           </div>

           <div class="firstRow leftContentLayout">
             <div class="humidity">湿度：40</div>
             <div class="PrecipitationRate">降水率：0</div>
           </div>

           <div class="secondRow leftContentLayout">
             <div class="wind">
               <div class="lanren">
	              <ul>
	       	        <li><img src="~/static/images/main5-pic1.png"> </li>
	       	        <li><img src="~/static/images/main5-pic2.png"> </li>
	       	        <li><img src="~/static/images/main5-pic3.png"> </li>
	              </ul>
               </div>
             </div>
             <div class="windDirection">风向</div>
             <div class="windSpeed">风速</div>
           </div>

          </div>

          <div>
            kong
          </div>
      </div>
  
    </div>
  </v-layout>
</template>

<script>
export default {
  data () {
    return {
      dialog: false,
      notifications: false,
      sound: true,
      widgets: false

    }
  }
}
</script>


<style scoped lang="less">
.container {
  padding-top: 10px;
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
}
.container-content {
  width: 80%;
  background-color: #666;
}

.lanren {
  -webkit-transition: All 1s 0s;
  -moz-transition: All 1s 0s;
  -ms-transition: All 1s 0s;
  margin-top: 20px;
  ul{ 
    margin: 0;
    padding: 0;
    -webkit-transform: translateX(0px) translateY(0px) translateZ(0px) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1);
    -moz-transform: translateX(0px) translateY(0px) translateZ(0px) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1);
    -ms-transform: translateX(0px) translateY(0px) translateZ(0px) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1);
    li {
      list-style: none;
      position: absolute;
      width: 80px;
      height: 80px;
      img {
        width: 80px;
        height: 80px;
        -webkit-transform-style: preserve-3d;
        -moz-transform-style: preserve-3d;
        -ms-transform-style: preserve-3d;
        transform-style: preserve-3d;
      }
    }
  }
  }

  .lanren ul li:nth-of-type(1) {
    -webkit-transition: All 1.2s 0s;
    -moz-transition: All 1.2s 0s;
    -ms-transition: All 1.2s 0s;
    transition: All 1.2s 0s;
    -webkit-transform: translateX(0) translateY(0) translateZ(0px) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1);
    -moz-transform: translateX(0) translateY(0) translateZ(0px) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1);
    -ms-transform: translateX(0) translateY(0) translateZ(0px) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1);
    transform: translateX(0) translateY(0) translateZ(0px) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1);
    img {
      -webkit-animation: z 5s linear 0s infinite;
      -moz-animation: z 5s linear 0s infinite;
      -ms-animation: z 5s linear 0s infinite;
      animation: z 5s linear 0s infinite;
    }
  }
  .lanren ul li:nth-of-type(2) {
    -webkit-animation: y 20s linear 0s infinite;
    -moz-animation: y 20s linear 0s infinite;
    -ms-animation: y 20s linear 0s infinite;
    animation: y 20s linear 0s infinite;
  }
  .lanren ul li:nth-of-type(3) {
    -webkit-animation: z 10s linear 0s infinite;
    -moz-animation: z 10s linear 0s infinite;
    -ms-animation: z 10s linear 0s infinite;
    animation: z 10s linear 0s infinite;
  }
  @-webkit-keyframes z {
	  from { -webkit-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1); -moz-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1); -ms-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1); transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1); }
	  to { -webkit-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(360deg) scaleX(1) scaleY(1) scaleZ(1); -moz-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(360deg) scaleX(1) scaleY(1) scaleZ(1); -ms-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(360deg) scaleX(1) scaleY(1) scaleZ(1); transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(360deg) scaleX(1) scaleY(1) scaleZ(1); }
  }
  @-webkit-keyframes y {
	  from { -webkit-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1); -moz-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1); -ms-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1); transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(0deg) scaleX(1) scaleY(1) scaleZ(1); }
	  to { -webkit-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(-360deg) scaleX(1) scaleY(1) scaleZ(1); -moz-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(-360deg) scaleX(1) scaleY(1) scaleZ(1); -ms-transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(-360deg) scaleX(1) scaleY(1) scaleZ(1); transform: translateX(0) translateY(0) translateZ(0) rotateX(0deg) rotateY(0deg) rotateZ(-360deg) scaleX(1) scaleY(1) scaleZ(1); }
  }
  .content-right-top {
    padding: 20px 20px 5px;
    display: flex;
    flex-flow: row;
    justify-content: space-between;
    align-items: center;
    .content-right-top-left {
      width: 50%;
      .leftContentLayout {
        display: flex;
        flex-flow: row wrap;
        justify-content: space-around;
        margin: 15px;
        .temperature {
          margin-left: 50px;
        }
        .temperature-right {
          margin-right: auto;
          div {
            height: 55%;
          }

        }
      }
      .temperature {
        a {
          font-size: 3em;
        }
        span {
          font-size: 4em;
        }
      }
    }
    .content-address {
      display: flex;
      flex-flow: row;
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

</style>
