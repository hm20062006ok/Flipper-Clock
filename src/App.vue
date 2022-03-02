<template>
  <div id="app">
    <router-link to="/">Go to Home</router-link>
    <router-view></router-view>
<!--    <div id="nav">-->
<!--      <router-link to="/">Home</router-link>-->
<!--      |-->

<!--    </div>-->

            <FlipClock></FlipClock>
<!--        牌 外框-->
<!--    <div class="flip down" :class="{'go': isFlipping}">-->
<!--      &lt;!&ndash;      前面的纸牌&ndash;&gt;-->
<!--      <div class="digital front number0" :class="_textClass(frontTextFromData)"></div>-->
<!--      &lt;!&ndash;      后面的纸牌&ndash;&gt;-->
<!--      <div class="digital back number1" :class="_textClass(backTextFromData)"></div>-->
<!--    </div>-->

    <!--<div class="btn-con">-->
    <!--  <button id="btn1" @click="flipDown(1,2)">向下翻+1</button>-->
    <!--</div>-->


  </div>
</template>


<script>
// import draggable from 'vuedraggable'
import FlipClock from "@/components/FlipClock";

export default {
  name: 'app',
  components: { FlipClock },
  data() {
    return {
      item: 1,
      isFlipping: false,
      frontTextFromData: 0,
      backTextFromData: 1,
      flipType: 'down',
      duration: 600
    }
  },
  methods: {
    _textClass(number) {
      return 'number' + number;
    },
    flipDown(front, back) {
      this._flip('down', front, back)
    },
    _flip(type, front, back) {
      if (this.isFlipping) {
        return false;
      }
      this.frontTextFromData = front
      this.backTextFromData = back
      this.flipType = type;
      this.isFlipping = true;
      setTimeout(() => {
        this.isFlipping = false
        this.frontTextFromData = back
      }, this.duration)
    }
  }
}
</script>

<style>

.flip {
  display: inline-block;
  position: relative;
  width: 60px;
  height: 100px;
  line-height: 100px;
  border: solid 1px #000;
  border-radius: 10px;
  background: #ffffff;
  font-size: 66px;
  text-align: center;
  color: #ffffff;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.5);
}

.flip .digital:before,
.flip .digital:after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  background: #000000;
  overflow: hidden;
  box-sizing: border-box;
}

.flip .digital:before {
  top: 0;
  bottom: 50%;
  border-radius: 10px 10px 0 0;
  border-bottom: solid 1px #666;
}

.flip .digital:after {
  top: 50%;
  bottom: 0;
  border-radius: 0 0 10px 10px;
  line-height: 0;
}

/*向下翻的层级关系和初始状态*/
.flip.down .front:before {
  z-index: 3;
}

.flip.down .back:after {
  z-index: 2;
  transform-origin: 50% 0%;
  transform: perspective(160px) rotateX(180deg);
}

.flip.down .front:after,
.flip.down .back:before {
  z-index: 1;
}

/*向下翻动作时的动画*/
/* 1.前面上半部分往下翻时的动画（前面上半部向下翻转180度）*/
.flip.down.go .front:before {
  /*翻转轴的原点：x轴的中间， y轴的最底部*/
  transform-origin: 50% 100%;
  animation: frontFlipDown 0.6s ease-in-out both;
  box-shadow: 0 -2px 6px rgba(255, 255, 255, 0.3);
  /*-webkit-backface-visibility: hidden;*/
  backface-visibility: hidden;
}

/* 前面上半部分往下翻时的动画 --end */

/*2. 后面下半部分往下翻的动画（1字的下半部分从折叠状态恢复展示）*/
.flip.down.go .back:after {
  animation: backFlipDown 0.6s ease-in-out both;
}

/*2. 后面下半部分往下翻的动画（1字的下半部分从折叠状态恢复展示） --end */

/*向下翻动作时的动画 --end */

/*前面上半部分往下翻时的动画*/
@keyframes frontFlipDown {
  0% {
    transform: perspective(160px) rotateX(0deg);
  }
  100% {
    transform: perspective(160px) rotateX(-180deg);
  }
}

/*后面下部分恢复展示时的动画*/
@keyframes backFlipDown {
  0% {
    transform: perspective(160px) rotateX(180deg);
  }
  100% {
    transform: perspective(160px) rotateX(0deg);
  }
}


/*.flip.up .back:after{*/
/*  z-index: 3;*/
/*}*/

/*.flip.up .back:before,*/
/*.flip.up .front:after{*/
/*  z-index: 1;*/
/*}*/

/*.flip.up .front:before{*/
/*  z-index: 2;*/
/*}*/


.flip .number0:before,
.flip .number0:after {
  content: '0';
}

.flip .number1:before,
.flip .number1:after {
  content: '1';
}

.flip .number2:before,
.flip .number2:after {
  content: '2';
}

.flip .number3:before,
.flip .number3:after {
  content: '3';
}

.flip .number4:before,
.flip .number4:after {
  content: '4';
}

.flip .number5:before,
.flip .number5:after {
  content: '5';
}

.flip .number6:before,
.flip .number6:after {
  content: '6';
}

.flip .number7:before,
.flip .number7:after {
  content: '7';
}

.flip .number8:before,
.flip .number8:after {
  content: '8';
}

.flip .number9:before,
.flip .number9:after {
  content: '9';
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
