<template>
  <div>
    <h2>Cena {{ contador + 1 }} con {{ rey }}</h2>
    <h3>Precio: {{ producto.precio }}€</h3>
    <div v-if="producto.precio < 100">
      <div>
        <p>10% de descuento</p>
        <p>Nuevo precio: {{ nuevoPrecio }}€</p>
      </div>
      <img src="/oferta.jpg" alt="Oferta" class="oferta-img">
    </div>
    <img :src="imagen" alt="">
    <button @click="siguiente">Siguiente</button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import datos from './datos.js'

const contador = ref(0)

const producto = computed(() => datos.productos[contador.value])

const rey = computed(() => {
  let nombre = producto.value.nombre.toLowerCase()
  return nombre.charAt(0).toUpperCase() + nombre.slice(1)
})

const imagen = computed(() => {
  return `https://www.html6.es/img/${rey.value.toLowerCase()}.png`
})

const nuevoPrecio = computed(() => {
  return Number((producto.value.precio / 1.1).toFixed(2))
})

const siguiente = () => {
  contador.value++
  if (contador.value >= datos.productos.length) {
    contador.value = 0
  }
}
</script>

<style scoped>
.oferta-img {
  width: 65px;
  margin: 0 0 10px 0;
}
</style>