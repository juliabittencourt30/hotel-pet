
<script setup>
import { ref } from 'vue';
import { useRouter, RouterLink } from 'vue-router';

const API_URL = 'http://localhost:3000';
const router = useRouter();

const novoTutor = ref({
  nome: '',
  telefone: '',
});

async function salvarTutor() {
  try {
    console.log('Salvando tutor...');

    const resposta = await fetch(`${API_URL}/tutores`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(novoTutor.value),
    });

    if (!resposta.ok) {
      console.log('Erro ao salvar:', resposta.status);
      alert('Não foi possível salvar o tutor.');
      return;
    }

    alert('Tutor cadastrado com sucesso!');
    router.push('/tutores');
  } catch (erro) {
    console.log('Erro na requisição:', erro);
    alert('Erro ao conectar com o JSON Server. Verifique se ele está ligado.');
  }
}
</script>

<template>
  <div>
    <header class="mb-4">
      <h1 class="text-2xl font-bold">Cadastro de Tutor</h1>
      <p class="text-body-secondary mb-0">
        Cadastro de tutores no sistema.
      </p>
    </header>

    <form @submit.prevent="salvarTutor">
      <div class="col-md-6 mb-3">
        <label for="nome" class="form-label">Nome do Tutor:</label>
        <input
          id="nome"
          v-model="novoTutor.nome"
          type="text"
          class="form-control"
          required
        />
      </div>

      <div class="col-md-6 mb-3">
        <label for="telefone" class="form-label">Telefone:</label>
        <input
          id="telefone"
          v-model="novoTutor.telefone"
          type="tel"
          class="form-control"
          required
        />
      </div>

      <button type="submit" class="btn btn-success me-2">
        Salvar Tutor
      </button>

      <RouterLink to="/tutores" class="btn btn-secondary">
        Cancelar
      </RouterLink>
    </form>
  </div>
</template>
