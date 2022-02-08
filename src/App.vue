<template>
<!-- SuspenseWithError封装的切换路由，页面显示成功内容或错误消息 -->
<!--  #error插槽的名称 -->
<SuspenseWithError>
  <template #error="{err}">
     {{err}}
  </template>
   <template #default>
      <User />
   </template>
    <template #fallback>
      loadding
    </template>
</SuspenseWithError>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import User from '@/components/User.vue';
import SuspenseWithError from '@/components/SuspenseWithError.vue'

export default defineComponent({
  name: 'App',
   components: {
    User,
    SuspenseWithError
  },
  setup(){
  }
});
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>