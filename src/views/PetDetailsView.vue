
<script setup>
import { onMounted, ref } from 'vue';
import { useRoute, RouterLink } from 'vue-router';

const route = useRoute();
const API_URL = 'http://localhost:3000';

const pet = ref({});
const tutor = ref({});

async function carregandoPet() {
  try {
    const respostaPets = await fetch(
      `${API_URL}/pets/${route.params.id}`,
    );

    if (!respostaPets.ok) {
      console.log('Ops, Pet não encontrado!');
      return;
    }

    pet.value = await respostaPets.json();

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
  <div>
    <h1 class="text-2xl font-bold mb-4">Detalhes do Pet</h1>

    <p><strong>Nome:</strong> {{ pet.nome }}</p>
    <p><strong>Espécie:</strong> {{ pet.especie }}</p>
    <p><strong>Tutor:</strong> {{ tutor.nome }}</p>

    <RouterLink to="/pets" class="btn btn-secondary">
      Voltar
    </RouterLink>
  </div>
</template>
