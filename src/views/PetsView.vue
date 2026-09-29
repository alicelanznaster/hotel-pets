<script setup>
import { onMounted, ref } from 'vue';

const pets = ref([]);
const tutores = ref([]);

//chamando API geral:
const API_URL = 'http://localhost:3000';

//chamar API para listar todos os pets e tutores;
async function carregarDados() {
    const respostaPets = await fetch(`${API_URL}/pets`);
    pets.value = await respostaPets.json();

    const respostaTutores = await fetch(`${API_URL}/tutores`);
    tutores.value = await respostaTutores.json();
    console.log('PETS - ', pets.value);
    console.log('TUTORES - ', tutores.value);
}

//exibir nome do tutor
function nomeDoTutor(tutorId) {
    for (const tutor of tutores.value) {
        if (tutor.id === tutorId) {
            return tutor.nome;
        }
    }
    return 'Tutor não encontrado!'
}
onMounted(carregarDados)
</script>

<template>
    <div>
        <header class="mb-4">
            <h1 class="text-2xl font-bold">Listagem de Pets</h1>
            <p class="text-body-secondary mb-0">
                Listagem dos Pets cadastrados no sistema.
            </p>
        </header>

        <table class="table table-striped table-hover">
            <thead>
                <th>id</th>
                <th>Nome</th>
                <th>Espécie</th>
                <th>Tutor</th>
            </thead>
            <tbody>
                <tr v-for="pet in pets" :key="pet.id">
                    <td>{{ pet.id }}</td>
                    <td>{{ pet.nome }}</td>
                    <td>{{ pet.especie }}</td>
                    <td>{{ nomeDoTutor(pet.tutorId) }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<style scoped>
</style>