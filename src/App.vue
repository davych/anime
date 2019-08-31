<template>
  <div id="app">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  },
  mounted() {
    this.$nextTick(()=>{
      this.resizeFontSize()
    })
  },
  methods: {
    resizeFontSize(){
      //获取根元素
      const docEl = document.documentElement;
      //获取设备宽度
      const {clientWidth} = docEl;
      //若未获取到设备宽度，则终止函数执行
      if (!clientWidth) return ;
      //计算rem基础配置：设计图以750px为准时，px rem比例为1：100
      const fs= 100*(clientWidth/750) ;
      //为根元素字体赋值
      docEl.style.fontSize = `${fs}px`;
    }
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
body {
  height: 100%;
    position: fixed;
}
</style>
