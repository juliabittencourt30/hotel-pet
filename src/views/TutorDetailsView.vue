<script setup>
import { onMounted, ref } from 'vue';
import { useRoute, RouterLink } from 'vue-router';


const route = useRoute();
const API_URL = 'http://localhost:3000';


const tutor = ref({});


async function carregarTutor() {
 const resposta = await fetch(
   `${API_URL}/tutores/${route.params.id}`,
 );


 if (resposta.ok) {
   tutor.value = await resposta.json();
 }
}


onMounted(carregarTutor);
</script>


<template>
 <div>
   <h1 class="text-2xl font-bold mb-4">Detalhes do Tutor</h1>


   <p><strong>ID:</strong> {{ tutor.id }}</p>
   <p><strong>Nome:</strong> {{ tutor.nome }}</p>
   <p><strong>Telefone:</strong> {{ tutor.telefone }}</p>


   <RouterLink to="/tutores" class="btn btn-secondary">
     Voltar
   </RouterLink>
 </div>
</template>


