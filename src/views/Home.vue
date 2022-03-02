<template>
  <div class="home">
    <div class='M-Flipper' :class="[flipType, {'go': isFlipping}]">
      <div class='digital front' :class='_textClass(frontTextFromData)'></div>
      <div class='digital back' :class='_textClass(backTextFromData)'></div>
    </div>
    <button @click='isFlipping = !isFlipping'>翻转</button>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data () {
    return {
      flipType: 'down',
      isFlipping: false,
      frontTextFromData: 0,
      backTextFromData: 1
    }
  },
  methods:{
    _textClass(number){
      return 'number'+number
    }
  }
}
</script>
<style scoped>
/* 整个翻牌组件容器 */
.M-Flipper{
  display: inline-block;;
  position: relative;
  width: 60px;
  height: 100px;
  line-height: 100px;
  border: solid 1px #000;
  background-color: #ffffff;
  font-size: 66px;
  color: #ffffff;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.5%);
  text-align: center;
}

/* 数字 */
.M-Flipper .digital:before,
.M-Flipper .digital:before {
  content: "";
  position: absolute;
  left: 0;
  right: 0;
  background: #000000;
  overflow: hidden;
  box-sizing: border-box;
}
/* 数字上部分 */
.M-Flipper .digital:before {
  top: 0;
  bottom: 50%;
  border-radius: 10px 10px 0 0;
  border-bottom: solid 1px #666;
}

/* 数字下部分 */
.M-Flipper .digital:after {
  top: 50%;
  bottom: 0;
  border-radius: 0 0 10px 10px;
  line-height: 0;
}

.M-Flipper.down .front:before {
  z-index: 3;
}
.M-Flipper.down .front:after,
.M-Flipper.down .back:before{
  z-index: 1;
}
.M-Flipper.down .back:after {
  z-index: 2;
  transform-origin: 50% 0%;
  transform: perspective(160px) rotateX(180deg);
}

/* down下翻  go进行中， 前牌的样式*/
.M-Flipper.down.go .front:before{
  /* 旋转原点定位到x轴的50%， y轴的100%。 也就是底边中点*/
  transform-origin: 50% 100%;
  box-shadow: 0 -2px 6px rgba(255,255,255, 0.3);
  /*          动画名称        时长  缓动函数    animation-fill-mode（动画结束后，样式如何应用于元素）*/
  animation: frontFlipDown 0.6s ease-in-out both;
  /*  元素的背面是其正面的镜像，backface-visibility指示背面的可见性*/
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
}

@keyframes frontFlipDown {
  0% {
    /* perspective（透视距离 近大远小） 围绕x轴旋转 0度 */
    transform: perspective(160px) rotateX(0deg);
  }
  100% {
    /* perspective（透视距离 近大远小） 围绕x轴旋转 0度 */
    transform: perspective(160px) rotateX(-180deg);
  }
}

.M-Flipper .number0:before,
.M-Flipper .number0:after {
  content: '0';
}
</style>
