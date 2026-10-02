<script setup>
import { onMounted, ref } from 'vue';
import { RouterLink, useRoute } from 'vue-router';

// chamando minha useRouter
const route = useRoute();

// Chamando nossa API
const API_URL = 'https://localhost:3000';

//criando as variaveis reativas para armazenar os dados do pet e do tutor
const pet = ref({});
const tutor = ref({});

// função para carregar os dados do pet e do tutor
async function carregandoPet() {
  try {
    const respostaPets = await fetch(`${API_URL}/pets/${route.params.id}`);

    if (!respostaPets.ok) {
      console.log('Ops, Pet não encontrado!');
    }

    pets.value = await respostaPets.json();

    const respostaTutor = await fetch(
      `${API_URL}/tutores/${pet.value.tutorId}`,
    );
    tutor.value = respostaTutor.ok
      ? await respostaTutor.json()
      : { nome: 'Tutor não encontrado' };
  } catch (erro) {
    console.log('Erro ao carregar os dados do pet e do tutor:', erro);
  }
}

onMounted(carregandoPet);
</script>

<template>
  <h1>Nome: {{ pet.nome }}</h1>
  <p>Espécie: {{ pet.especie }}</p>
 <!-- <p>Tutor: {{ nomeDoTutor(pet.tutorId) }}</p>-->
</template>
