<template>
<!-- :err="error"，作用域插槽 -->
<!-- name="fallback"，具名插槽 -->
  <slot v-if="error" name="error" :err="error">
     {{error}}
  </slot>
  <Suspense v-else>
   <template #default>
      <slot name="default"></slot>
   </template>
    <template #fallback>
      <slot name="fallback"></slot>
    </template>
  </Suspense>
</template>
<script lang="ts">
import { defineComponent, onErrorCaptured, ref } from "vue";
export default defineComponent({
  setup(){
const error=ref('')

onErrorCaptured((err)=>{
//  console.log('setup=>err',err)
     error.value=err as unknown as string //课程是这样写的，error.value=err as string,因为error.value报错了，所以转成字符串
      return true
    })

    return{
      error
    }

  }
});
</script>