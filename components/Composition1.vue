<template>
  <div>Component using composition api
    <button @click="getMessage2('hello world')">Get Message</button>
    <div>{{ message2Rxd }}</div>
  </div>
</template>
<script>
// @ts-nocheck
import { computed, defineComponent, useContext, onMounted, onUnmounted, ref, toRefs, reactive } from '@nuxtjs/composition-api'

export default defineComponent({
  setup(props, context) {
    const ctx = useContext()
    ctx.$data = toRefs(reactive({
      message2Rxd: 'this should change'    
    }))
    
    const socket = ctx.$nuxtSocket({
      channel: '/index',
      reconnection: false,
      teardown: false,
      onUnmounted
    })
    ctx.getMessage2('see me??')
    return { 
      ...ctx.$data,
      getMessage2: ctx.getMessage2
    }
  }
})
</script>
