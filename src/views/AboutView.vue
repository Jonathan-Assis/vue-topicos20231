<script setup lang="ts">
import { ref, onMounted } from 'vue';
import axios from 'axios';

const nome = ref('Nome');
const senha = ref('123');
const contador = ref(1);
const usuarios = ref();
const erro = ref('');

function incrementar(){
  contador.value++
}
async function atualizar() {
  try {
    usuarios.value = (await axios.get('usuario')).data;
    erro.value = '';
  } catch (e) {
    erro.value = (e as Error).message;
  }
}
async function cadastrar() {
  try {
    await axios.post('usuario', {
      nome: nome.value,
      senha:senha.value
    });
    erro.value = '';
    atualizar();
  } catch (e) {
    erro.value = (e as Error).message;
  }
}


onMounted (() => {
  atualizar();
}) 

</script>
<template>
  <div class="about">
    <h1>Bem vindo {{nome}}</h1>
    <p><input type="text" v-model="nome"/></p>
    <p><input type="password" v-model="senha"/></p>
    <button @click="cadastrar">Cadastrar</button>
    <p v-if="nome.length > 5">Nome Longo</p>
    <p v-else>Nome curto</p>
    <p>{{ contador }}<button @click="incrementar">Incrementador</button></p>
    <p v-if="erro">{{ erro }}</p>
    <table>
      <thead>
        <td>Id</td>
        <td>nome</td>
      </thead>
      <tr v-for="(dado) in usuarios" :key="dado.id">
        <td>{{ dado.id }}</td>
        <td>{{ dado.nome }}</td>
      </tr>
    </table>
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
