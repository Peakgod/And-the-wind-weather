<template>
  <v-layout class="container">

    <div class="container-content">
      <div class="lanren">
	      <ul>
	      	<li><img src="~/static/images/main5-pic1.png"> </li>
	      	<li><img src="~/static/images/main5-pic2.png"> </li>
	      	<li><img src="~/static/images/main5-pic3.png"> </li>
	      </ul>
     </div>

      <div class="content-right-btn">
      <v-btn color="#fff" flat nuxt to="/">返回</v-btn>
    </div>
    <div class="content-right-btn">
      <v-btn color="#fff" flat nuxt to="/">返回</v-btn>
    </div>
    <div class="content-right-btn">
      <v-btn color="#fff" flat nuxt to="/">返回</v-btn>
    </div>
    <div class="content-right-btn">
      <v-btn color="#fff" flat nuxt to="/">返回</v-btn>
    </div>
    <div class="content-right-btn">
      <v-btn color="#fff" flat nuxt to="/">返回</v-btn>
    </div>

    </div>
  </v-layout>
</template>

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

</style>
