<template>
  <div>
    Component using composition api
    <button @click="getMessage2('hello world')">Get Message</button>
    <div>{{ message2Rxd }}</div>
  </div>
</template>
<script>
// @ts-nocheck
import {
  computed,
  watch,
  defineComponent,
  useContext,
  onMounted,
  onUnmounted,
  ref,
  toRefs,
  reactive
} from '@nuxtjs/composition-api'

export default defineComponent({
  setup(props, context) {
    const ctx = useContext()
    ctx.$data = toRefs(
      reactive({
        message2Rxd: 'this should change'
      })
    )
    // $watch stub:
    ctx.$watch = (label, cb) => {
      watch(ctx.$data[label], cb)
    }
    ctx.$destroy = () => {
      console.log('run me too')
    }

    ctx.$nuxtSocket({
      channel: '/index',
      reconnection: false,
      onUnmounted
    })
    ctx.$nuxtSocket({
      channel: '/index',
      reconnection: false,
      onUnmounted
    })
    ctx.getMessage2('see me??')
    // ctx.$watch('message2Rxd', (n, o) => {
    //   console.log('message2Rxd changed', n, o)
    // })

    return {
      ...ctx.$data,
      getMessage2: ctx.getMessage2
    }
  }
})
</script>
