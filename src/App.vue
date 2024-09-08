<script setup>
import { ref } from "vue"

const genUuids = ref([])
for (let index = 0; index < 10; index++) {
  genUuids.value[index] = self.crypto.randomUUID()
}
const regenerate = ()=>{
  genUuids.value = []
  for (let index = 0; index < 10; index++) {
    genUuids.value[index] = self.crypto.randomUUID()
  }
}
</script>

<template>
  <main>
    <button @click="regenerate">regenerate</button>
    <li v-for="(item, index) in genUuids" :key="index">{{ item }}</li>
  </main>
</template>

<style scoped>
</style>
