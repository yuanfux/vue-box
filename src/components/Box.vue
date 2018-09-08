<template>
  <div :style="sceneStyle">
    <div :style="boxContainerStyle">
      <div :style="frontFaceStyle">
        <slot name="front"></slot>
      </div>
      <div :style="backFaceStyle">
        <slot name="back"></slot>
      </div>
      <div :style="topFaceStyle">
        <slot name="top"></slot>
      </div>
      <div :style="bottomFaceStyle">
        <slot name="bottom"></slot>
      </div>
      <div :style="rightFaceStyle">
        <slot name="right"></slot>
      </div>
      <div :style="leftFaceStyle">
        <slot name="left"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Box',
  props: {
    boxStyle: {
      type: Object
    },
    frontStyle: {
      type: Object
    },
    backStyle: {
      type: Object
    },
    rightStyle: {
      type: Object
    },
    leftStyle: {
      type: Object
    },
    topStyle: {
      type: Object
    },
    bottomStyle: {
      type: Object
    },
    width: {
      type: Number,
      default: 100
    },
    height: {
      type: Number,
      default: 200
    },
    length: {
      type: Number,
      default: 300
    },
    perspective: {
      type: Number,
      default: 0
    }
  },
  computed: {
    sceneStyle: function() {
      return {
        width: `${this.length}px`,
        height: `${this.height}px`,
        perspective: `${this.perspective}px`
      }
    },
    boxContainerStyle: function() {
      return {
        ...this.boxStyle,
        width: '100%',
        height: '100%',
        position: 'relative',
        'transform-style': 'preserve-3d'
      }
    },
    frontFaceStyle: function() {
      return {
        ...this.frontStyle,
        position: 'absolute',
        width: `${this.length}px`,
        height: `${this.height}px`
      }
    },
    backFaceStyle: function() {
      return {
        ...this.backStyle,
        position: 'absolute',
        width: `${this.length}px`,
        height: `${this.height}px`,
        transform: `translateZ(-${this.width/2}px) rotateY(180deg)`
      }
    },
    topFaceStyle: function() {
      return {
        ...this.topStyle,
        position: 'absolute',
        width: `${this.length}px`,
        height: `${this.width}px`,
        transform: `translateY(-${this.width/2}px) rotateX(90deg)`
      }
    },
    bottomFaceStyle: function() {
      return {
        ...this.bottomStyle,
        position: 'absolute',
        width: `${this.length}px`,
        height: `${this.width}px`,
        transform: `translateY(${this.height-this.width/2}px) rotateX(-90deg)`
      }
    },
    leftFaceStyle: function() {
      return {
        ...this.leftStyle,
        position: 'absolute',
        width: `${this.width}px`,
        height: `${this.height}px`,
        transform: `translateX(-${this.width/2}px) rotateY(-90deg)`
      }
    },
    rightFaceStyle: function() {
      return {
        ...this.rightStyle,
        position: 'absolute',
        width: `${this.width}px`,
        height: `${this.height}px`,
        transform: `translateX(${this.length-this.width/2}px) rotateY(90deg)`
      }
    }
  }
}
</script>
