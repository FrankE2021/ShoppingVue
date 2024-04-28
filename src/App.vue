<template>
<div class="contenedor">
  <h2>Cena {{ contador + 1 }}
    con el rey godo {{ rey }}
  </h2>  
  <h3 class="precio">Precio: {{ productos[contador].precio }} $</h3>
  <div v-if="productos[contador].finDeSemana" class="soloFinesDeSemana dias">(Solo fines de semana)</div>
  <div v-else class="todosLosDias dias">(De lunes a domingo)</div>
  <div v-if="productos[contador].precio<100" class="oferta">
    <div class="dto">Ahora es un 10% dto:
    {{ nuevoPrecio }}$</div>
    <img src="/oferta.jpg" alt="rey godo en descuento"/>
  </div>
  <div>
    <img :src="imagen" alt=""/>
  </div>
  <div>
    <button class="siguiente" @:click="siguiente"> Siguiente ({{contador + 1}}/{{total}})</button>
</div>
</div>  
</template>

<script setup>
  import {computed, ref} from "vue"
  import { productos } from './datos';
  const contador=ref(0)
  const total=productos.length;
  const ruta="https://www.html6.es/img/rey_";
  const siguiente=()=>{
    contador.value++
    if (contador.value>=total){
      contador.value=0;
    }
  }

  const rey=computed(()=>{
    const elNombre=productos[contador.value].nombre.toLowerCase()
    return elNombre.substring(0,1).toUpperCase() + elNombre.substring(1)
  })

  const imagen=computed(()=>{
    return `${ruta}${productos[contador.value].nombre.toLowerCase()}+.png`
  })

  const nuevoPrecio=computed(()=>{
    return Number(productos[contador.value].precio/1.10).toFixed(2)
  })
</script>
  

<style scoped>
  .todosLosDias{
    background-color: green;
  }
  .soloFinesDeSemana{
    background-color: red;
  }
  
  
</style>