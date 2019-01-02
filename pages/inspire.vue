<template>
  
  <v-container grid-list-md text-xs-center>
    <v-layout row wrap justify-center>
      <v-flex xs12>
        <v-card dark color="primary">
          <v-card-text class="px-0">天气详情</v-card-text>
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

              <div class="airQuality">
                <div>空气质量：<span>良</span></div>
                <div>PM2.5：<span>25</span></div>
              </div>

              <div class="temperature">
                <a><span>56</span>℃</a>
                <img src="~/assets/inco-weather/100.png"/>
                <a class="weatherIcon">晴天</a>
              </div>
      
              <div class="firstRow">
                <div class="humidity">
                  <div>湿度：40</div>
                  <div class="PrecipitationRate">降水率：0</div>
              </div>
        
              <div class="windDirection">
                <div>风向：东南</div>
                <div class="windSpeed">风速：千米每小时</div>
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
          <v-card-text class="px-0">撒旦</v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      dialog: false,
      notifications: false,
      sound: true,
      widgets: false,

      headers: [
        {
          text: '日期',
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
        },
        {
          value: false,
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: '1%'
        },
        {
          name: 'Eclair',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: '7% '
        }
      ]
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
    width: 50%;
    .airQuality{
      display: flex;
      flex-flow: row wrap;
      justify-content: flex-end;
    }
    .temperature {
      margin-left: 25%;
      .weatherIcon {
        font-size: 18px;
      }
    }
    .temperature-right {
      margin-right: auto;
      div {
        height: 55%;
      }
    }
    .firstRow {
      margin-left: 25%;
      display: flex;
      justify-content: space-between;
      .humidity {
        display: flex;
      }
      .PrecipitationRate {
        margin-left: 15px;
      }
      .windDirection {
        display: flex;
        margin-right: 205px;
        .windSpeed {
          margin-left: 20px;
        }
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
      margin-left: 25%;
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
