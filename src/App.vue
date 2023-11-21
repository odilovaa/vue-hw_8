<script setup>
import {
    ref
  } from 'vue'

  const list = ref('')
  const loading = ref(false)

  async function fetchProducts() {
  const res = await fetch('https://fakestoreapi.com/products')
  const data = await res.json()
  if (!data.length) {
    loading.value = false;
    return
  }
  loading.value = false;
  list.value = data
}

</script>

<template>
<button @click="fetchProducts">Submit</button>

<div>
  <p v-for="product of list">{{ product }}</p>
</div>


</template>

<style scoped>
.loader {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  display: inline-block;
  position: relative;
  border: 3px solid;
  border-color: #FFF #FFF transparent;
  box-sizing: border-box;
  animation: rotation 1s linear infinite;
}
.loader::after {
  content: '';  
  box-sizing: border-box;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  border: 3px solid;
  border-color: transparent #FF3D00 #FF3D00;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  animation: rotationBack 0.5s linear infinite;
  transform-origin: center center;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
} 
    
@keyframes rotationBack {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(-360deg);
  }
}
</style>
