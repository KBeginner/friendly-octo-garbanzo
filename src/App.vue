<template>
  <div id="app">
    <h1>{{'基于Vue的组合键盘事件监听组件'}}</h1>
    <p>测试：Ctrl+Enter触发事件</p>
    <ul>
      <li v-for="(item,index) in list" :key="index">{{item}}</li>
    </ul>
    <!-- keyCodes为组合按键的keyCode数组，submit为键盘事件执行的函数 -->
    <Listener :keyCodes="codes" @action="fn"/>
  </div>
</template>

<script>
import Listener from './components/Listener.vue'
export default {
  name: 'app',
  components: {
    Listener,
  },
  data() {
    return {
      codes:[17,13],      // 传入按键的 keyCodde
      list:[]
    }
  },
  methods:{
    fn(){
      this.list.push('aaaaaaaaaaa  ')
    },
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
</style>
