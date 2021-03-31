<template>
  <div>Component using composition api
    <button @click="getMessage2('hello world')">Get Message</button>
    <br/>
    {{ message2Rxd }}
  </div>
</template>
<script>
// @ts-nocheck
import { computed, defineComponent, useContext, onMounted, onUnmounted, ref, reactive } from '@nuxtjs/composition-api'

export default defineComponent({
  setup(props, context) {
    const ctx = useContext()
    const data = {
      message2Rxd: ref('incoming?')
    }
    Object.assign(ctx, { ...data })
    const socket = ctx.$nuxtSocket({
      channel: '/index',
      reconnection: false,
      teardown: false,
      onUnmounted
    })
    
    return { 
      ...data, 
      getMessage2: ctx.getMessage2, 
    }
  }
})
</script>
