<script setup>
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const API_URL = 'http://localhost:3000';
const tutor = ref(null);

async function carregarTutor() {
  //pegando o id do pet que está na url
  const idTutor = route.params.id;

  //chamando API para buscar o pet pelo id
  const respostaTutores = await fetch(`${API_URL}/tutores/${idTutor}`);
  console.log('respostaTutores', respostaTutores);
  // convertendo a resposta da API para JSON
  tutor.value = await respostaTutores.json();
  console.log('tutor', tutor.value);

}

onMounted(carregarTutor);
</script>

<template>
  <section v-if="tutor === null">
    <p>Carregandoo..</p>
  </section>
  <section v-else>
    <h1>Nome do Tutor: {{ tutor.nome }}</h1>
    <p>Id: {{ tutor.id }}</p>
    <h5>Telefone: {{ tutor.telefone }}</h5>
  </section>
</template>
