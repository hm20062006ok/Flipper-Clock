<template>

  <div>
    <div class="component-wrapper" id="flash-sale">
      <div class="sale-header">
        <div class="countdown-zone">
          <div class="countdown-prefix">限時快搶{{ hou }} || {{ min }} || {{ sec }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      hou: 0,
      min: 0,
      sec: 0,
    }
  },
  created() {
    let that = this
    that.time()
  },
  methods: {
    time() {
      var that = this
      var fromApitime = '12:00'.substring(0, 2);
      //fixme: API返回的是剩余几小时，只能取本地的相对时间
      let date = new Date();
      let endTime = new Date(date.setHours(date.getHours()+ parseInt(fromApitime)))
      setInterval(function timestampToTime() {
        // var date = () - new Date())
        var date = (new Date(endTime)) - (new Date());
        // var date = (new Date() - new Date())
        // console.log(date)
        if (date > 0) {
          let time = date / 1000;
          that.hou = parseInt((time % (60 * 60 * 24)) / 3600) < 10 ? ('0' + parseInt((time % (60 * 60 * 24)) / 3600)) : parseInt((time % (60 * 60 * 24)) / 3600)
          that.min = parseInt(((time % (60 * 60 * 24)) % 3600) / 60) < 10 ? ('0' + parseInt(((time % (60 * 60 * 24)) % 3600) / 60)) : parseInt(((time % (60 * 60 * 24)) % 3600) / 60);
          that.sec = parseInt(((time % (60 * 60 * 24)) % 3600) % 60) < 10 ? ('0' + parseInt(((time % (60 * 60 * 24)) % 3600) % 60)) : parseInt(((time % (60 * 60 * 24)) % 3600) % 60);
          // that.ssec= parseInt(((date % (60 * 60 * 24)) % 3600) / 60)%10
        } else {
          that.day = "00"
          that.hou = "00"
          that.min = "00"
          that.sec = "00"
        }
      }, 1000)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
