<template>
  <div>Component using composition api
  </div>
</template>
<script>
// @ts-nocheck
import { defineComponent, useContext, onUnmounted } from '@nuxtjs/composition-api'

export default defineComponent({
  setup() {
    const ctx = useContext()
    const socket = ctx.$nuxtSocket({
      channel: '/index',
      reconnection: false,
      onUnmounted
    })
    ctx.getMessage2('hi')
    .then((r) => console.log('resp one way', r))

    socket.emit('getMessage2', 'some msg', (resp) => {
      console.log('also rxd', resp)
    })
    return {}

  }
})
</script>
