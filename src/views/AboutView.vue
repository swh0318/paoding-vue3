<script setup lang="ts">
import { ref, watch, watchEffect, computed, onMounted, onUnmounted } from 'vue'
import { useCounter } from './compositeAPIs/useCounter.js'

const { count, increment, decrement } = useCounter(10)

// 计算属性
const price = ref(100)
const discount = ref(0.1)
const finalPrice = computed(() => {
  return price.value * (1 - discount.value)
})
// 监听属性
watch(count, (newValue, oldValue) => {
  console.log(`count changed from ${oldValue} to ${newValue}`)
})

watchEffect(() => {
  console.log(`Price after discount: ${price.value * (1 - discount.value)}`)
})

onMounted(() => {
  console.log('组件挂载完毕')
})
onUnmounted(() => {
  console.log('组件已卸载')
})
</script>

<template>
  <p>Final Price: {{ finalPrice }}</p>
  <p>Count: {{ count }}</p>
  <button @click="increment">Increment</button>
  <button @click="decrement">Decrement</button>
</template>

<style scoped>

</style>