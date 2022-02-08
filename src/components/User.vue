<template>
  <div>
    {{ msg }}
    {{ msgRef }}
    <h3>Ecosystem</h3>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
export default defineComponent({ //setup是同步的，这里模拟异步数据
  async setup() { //setup是整个组件渲染完成前执行的，所以异步的setup里面的方法不会渲染到页面上来(页面是空白的),然后在父级组件App.vue加了<Suspense>,页面才显示内容

      //const promise:Promise<string>= new Promise((resolve,reject) => {
    const promise = new Promise((resolve,reject) => {
      setTimeout(() => {
         resolve("success message!");
        // reject("error message!"); //reject没有使用到会报eslint的错，加了vue.config.js
      }, 2000);
    });

    const msgRef = ref("abc");
    console.log("setup -> msgRef", msgRef);//有打印，页面是空白的

    const msg = await promise;
    console.log("setup -> msg", msg);//resolve打印的，页面是空白的，reject不会走这里，没有这句打印的，reject也会报错：Uncaught (in promise) error message!

    return {
      msg,
      msgRef,
    };
  },
});
</script>