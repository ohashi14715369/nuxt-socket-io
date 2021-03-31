<template>
  <div>Component using composition api
    <button @click="getMessage2('hello world')">Get Message</button>
    <div>{{ message2Rxd }}</div>
  </div>
</template>
<script>
// @ts-nocheck
import { computed, defineComponent, useContext, onMounted, onUnmounted, ref, reactive } from '@nuxtjs/composition-api'

export default defineComponent({
  setup(props, context) {
    const ctx = useContext()
    // Using reactive:
    // const data = reactive({
    //   message2Rxd: 'incoming'
    // })
    
    // Using refs:
    const data = {
      message2Rxd: ref('incoming')
    }

    ctx.$data = data
    
    const socket = ctx.$nuxtSocket({
      channel: '/index',
      reconnection: false,
      teardown: false,
      onUnmounted
    })
    ctx.getMessage2('see me??')
    return { 
      // data, // if using reactive, we'd have to use {{ data.message2Rxd }}
      ...data, // if using refs
      getMessage2: ctx.getMessage2
    }
  }
})
</script>
