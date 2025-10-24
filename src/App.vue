<template>
  <div class="app">
    <h1>Lista de Tarefas ;) </h1>

    <div class="input-container">
      <input
        class="input-tarefa"
        v-model="novaTarefa"
        @keyup.enter="adicionarTarefa"
        placeholder="Digite uma nova tarefa"
      />
      <button class="btn-adicionar" @click="adicionarTarefa">Adicionar</button>
    </div>

    <ul>
      <li v-for="(tarefa, index) in tarefas" :key="index">
        <input type="checkbox" v-model="tarefa.feito" />
        <span :class="{ feito: tarefa.feito }">{{ tarefa.texto }}</span>
        <button class="remover" @click="removerTarefa(index)">❌</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const novaTarefa = ref("");
    const tarefas = ref([]);

    const adicionarTarefa = () => {
      if (novaTarefa.value.trim() !== "") {
        tarefas.value.push({ texto: novaTarefa.value, feito: false });
        novaTarefa.value = "";
      }
    };

    const removerTarefa = (index) => {
      tarefas.value.splice(index, 1);
    };

    return { novaTarefa, tarefas, adicionarTarefa, removerTarefa };
  },
};
</script>

<style scoped>
.app {
  max-width: 600px;
  margin: 50px auto;
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
}

/* container do input e botão */
.input-container {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}

/* barra de pesquisa */
.input-tarefa {
  flex: 1; /* ❌ Isso não existe. Use flex: 1 */
  height: 48px;
  padding: 0 15px;
  font-size: 1.1em;
  border-radius: 8px;
  border: 2px solid #646cff;
  box-sizing: border-box;
}


/* botão "Adicionar" alinhado com o input */
.btn-adicionar {
  height: 48px; /* ✅ mesma altura do input */
  padding: 0 20px; /* corrigido, estava '30 px' (com espaço e sem unidade válida) */
  border-radius: 8px;
  border: 2px solid #646cff; /* igual ao input */
  background-color: #646cff;
  color: white;
  font-size: 1em;
  cursor: pointer;
  transition: background-color 0.2s, border-color 0.2s;
  box-sizing: border-box;
}

.btn-adicionar:hover {
  background-color: #535bf2;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  margin: 10px 0;
  gap: 10px;
}

li span.feito {
  text-decoration: line-through;
  color: gray;
  flex: 1;
}

li input[type="checkbox"] {
  width: 18px;
  height: 18px;
}

button.remover {
  background-color: transparent;
  color: red;
  padding: 5px;
  font-size: 1.1em;
}

button.remover:hover {
  color: darkred;
}
</style>
