<template>
  <div id="app">
    <div class="box-container">
      <Box 
           :width="width"
           :height="height"
           :length="length"
           :perspective="perspective"
           :boxStyle="boxStyle"
           :frontStyle="frontStyle" 
           :backStyle="backStyle"
           :leftStyle="leftStyle"
           :rightStyle="rightStyle"
           :topStyle="topStyle"
           :bottomStyle="bottomStyle"
      >
        <div slot="front">
          front
        </div>
        <div slot="back">
          back
        </div>
        <div slot="left">
          left
        </div>
        <div slot="right">
          right
        </div>
        <div slot="top">
          top
        </div>
        <div slot="bottom">
          bottom
        </div>
      </Box>
    </div>
  </div>
</template>

<script>
import Box from './components/Box.vue'

export default {
  name: 'app',
  data: () => ({
    width: 100,
    height: 100,
    length: 300,
    perspective: 600,
    boxStyle: {
      transition: 'transform 1s'
    },
    frontStyle: {
      'background-color': 'rgba(255, 208, 181, 0.5)'
    },
    backStyle: {
      'background-color': 'rgba(240, 178, 124, 0.5)'
    },
    leftStyle: {
      'background-color': 'rgba(207, 112, 63, 0.5)'
    },
    rightStyle: {
      'background-color': 'rgba(172, 233, 231, 0.5)'
    },
    topStyle: {
      'background-color': 'rgba(87, 128, 205, 0.5)'
    },
    bottomStyle: {
      'background-color': 'rgba(255, 191, 23, 0.5)'
    }
  }),
  methods: {
    setBoxStyle() {
      // eslint-disable-next-line
      console.log('box style gets exec');
      const transforms = [
        `translateZ(-${this.width/2}px) rotateY(0deg)`, // front
        `translateZ(-${this.width/2}px) rotateY(-180deg)`, // back
        `translateZ(-${this.length/2}px) rotateY(-90deg)`, // right
        `translateZ(-${this.length/2}px) rotateY(90deg)`, // left
        `translateZ(-${this.height/2}px) rotateX(-90deg)`, // top
        `translateZ(-${this.height/2}px) rotateX(90deg)` // bottom
      ];
      const transform = transforms[Math.floor(Math.random() * transforms.length)];
      this.$set(this.boxStyle, 'transform', transform);
      // console.log('boxStyle', this.boxStyle);
    }
  },
  mounted() {
    this.interval = setInterval(this.setBoxStyle, 2000);
  },
  beforeDestroy() {
    clearInterval(this.interval);
  },
  components: {
    Box
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.box-container {
  padding-left: 50px;
}
</style>
