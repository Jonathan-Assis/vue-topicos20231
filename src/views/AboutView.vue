<script setup lang="ts">
import { ref } from 'vue';

const nome = ref('Nome')
const contador = ref(1)

function incrementar(){
  contador.value++
}

</script>
<template>
  <div class="about">
    <h1>Bem vindo {{nome}}</h1>
    <p><input type="text" v-model="nome"/></p>
    <p v-if="nome.length > 5">Nome Longo</p>
    <p v-else>Nome curto</p>
    <p>{{ contador }}<button @click="incrementar">Incrementador</button></p>
  </div>
</template>

<!-- <style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style> -->
