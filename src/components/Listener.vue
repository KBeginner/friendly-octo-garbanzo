<template>
  <div id="Key_Listener">
    {{`基于Vue的组合键盘监听事件 封装组件`}}
  </div>
</template>

<script>
import Vue from 'vue'
export default {
  name: 'Listener',
  props:{
    // 按键的keyCode
    keyCodes:{
      type: Array,
      default: ()=>{
        return []
      }
    }
  },
  data() {
    return {
      keys:{}     // 辅助对象，一个按键对应一个key，值为true或false，true表示按下 false表示弹起
    }
  },
  mounted(){
    this.setKey()
    this.addListener()
  },
  beforeDestroy() {
    this.removeListener()    
  },
  methods:{
    // 每个按键设置一个key
    setKey(){
      this.keyCodes.forEach((element,index) => {
        Vue.set(this.keys, 'key'+index, false)
      });
    },
    // 监听器
    addListener(){
      document.addEventListener('keydown',this.keyDown)
      document.addEventListener('keyup', this.keyUp)
    },
    // 移除监听器
    removeListener(){
      document.removeEventListener('keydown', this.keyDown)
      document.removeEventListener('keyup', this.keyUp)
    },
    // 按键按下执行
    keyDown(e){
      this.keyCodes.forEach((element,index) => {
        e.keyCode == element ? Vue.set(this.keys,'key'+index, true) : ''
      });
    },
    // 按键弹起执行
    keyUp(e){
      this.keyCodes.forEach((element,index) => {
        e.keyCode == element ? Vue.set(this.keys,'key'+index, false) : ''
      });
    },
    // 组合按键触发函数
    emit(){
      let keyArr = []
      for(let val in this.keys){
        keyArr.push(this.keys[val])
      }
      const isAllKey = keyArr.every(element=>element == true)
      isAllKey ? this.$emit('action') : ''
    }
  },
  watch: {
    keys:{
      handler(){
        this.emit()
      },
      deep: true
    },
  }
}
</script>

<style scoped>
#Key_Listener{
  display: none;
}
</style>
