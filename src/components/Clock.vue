<template>
  <div style="width:120px;height:100px;position:relative;left:58px;top:50px;">
    <div id="dig1" class="dig">1</div>
    <div id="dig2" class="dig">2</div>
    <div id="dig3" class="dig">3</div>
    <div id="dig4" class="dig">4</div>
    <div id="dig5" class="dig">5</div>
    <div id="dig6" class="dig">6</div>
    <div id="dig7" class="dig">7</div>
    <div id="dig8" class="dig">8</div>
    <div id="dig9" class="dig">9</div>
    <div id="dig10" class="dig">10</div>
    <div id="dig11" class="dig">11</div>
    <div id="dig12" class="dig">12</div>

    <div id="hour1" class="hour"></div>
    <div id="hour2" class="hour"></div>
    <div id="hour3" class="hour"></div>
    <div id="hour4" class="hour"></div>

    <div id="min1" class="min"></div>
    <div id="min2" class="min"></div>
    <div id="min3" class="min"></div>
    <div id="min4" class="min"></div>
    <div id="min5" class="min"></div>

    <div id="sec1" class="sec"></div>
    <div id="sec2" class="sec"></div>
    <div id="sec3" class="sec"></div>
    <div id="sec4" class="sec"></div>
    <div id="sec5" class="sec"></div>
    <div id="sec6" class="sec"></div>
  </div>
</template>
<style>
div.dig,
div.hour,
div.min,
div.sec {
  position: absolute;
}
div.hour,
div.min,
div.sec {
  width: 2px;
  height: 2px;
  font-size: 2px;
}
div.dig {
  width: 30px;
  height: 30px;
  font-family: arial, verdana, sans-serif;
  font-size: 10px;
  color: #000000;
  text-align: center;
  padding-top: 10px;
}
div.min {
  background: #0000ff;
}
div.hour {
  background: #000000;
}
div.sec {
  background: #ff0000;
}
</style>
<script>
export default {
  name: 'Clock',
  data () {
    return {
      timer: '',
      H: '....'.split(''),
      M: '.....'.split(''),
      S: '......'.split(''),
      Ypos: 0,
      Xpos: 0,
      Ybase: 8,
      Xbase: 8,
      dots: 12
    }
  },
  created () {
    this.timer = setInterval(this.clock, 200)
  },
  destroyed () {
    clearInterval(this.timer)
  },
  methods: {
    clock () {
      var time = new Date()
      var secs = time.getSeconds()
      var sec = -1.57 + (Math.PI * secs) / 30
      var mins = time.getMinutes()
      var min = -1.57 + (Math.PI * mins) / 30
      var hr = time.getHours()
      var hrs = -1.57 + (Math.PI * hr) / 6 + (Math.PI * parseInt(time.getMinutes())) / 360
      for (var i = 0; i < this.dots; ++i) {
        document.getElementById('dig' + (i + 1)).style.top =
          0 - 15 + 40 * Math.sin(-0.49 + this.dots + i / 1.9).toString() + 'px'
        document.getElementById('dig' + (i + 1)).style.left =
          0 - 14 + 40 * Math.cos(-0.49 + this.dots + i / 1.9).toString() + 'px'
      }
      for (i = 0; i < this.S.length; i++) {
        document.getElementById('sec' + (i + 1)).style.top =
          this.Ypos + i * this.Ybase * Math.sin(sec).toString() + 'px'
        document.getElementById('sec' + (i + 1)).style.left =
          this.Xpos + i * this.Xbase * Math.cos(sec).toString() + 'px'
      }
      for (i = 0; i < this.M.length; i++) {
        document.getElementById('min' + (i + 1)).style.top =
          this.Ypos + i * this.Ybase * Math.sin(min).toString() + 'px'
        document.getElementById('min' + (i + 1)).style.left =
          this.Xpos + i * this.Xbase * Math.cos(min).toString() + 'px'
      }
      for (i = 0; i < this.H.length; i++) {
        document.getElementById('hour' + (i + 1)).style.top =
          this.Ypos + i * this.Ybase * Math.sin(hrs).toString() + 'px'
        document.getElementById('hour' + (i + 1)).style.left =
          this.Xpos + i * this.Xbase * Math.cos(hrs).toString() + 'px'
      }
    }
  }
}
</script>
